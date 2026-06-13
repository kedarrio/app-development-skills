---
name: auth-and-access
description: Handle login, signup, logout, sessions, protected routes, onboarding gates, roles, permissions, and safe redirects. Use this skill for any task touching authentication or authorization — adding/changing login flows, protecting routes/screens, role-based UI or access control, session handling, or redirect logic after auth events. Treat changes in this area as higher-risk: confirm before changing existing auth behavior.
---

# Auth and Access Skill

## Purpose
Implement or modify authentication and authorization correctly and safely — protecting routes, handling sessions, and applying role/permission logic without introducing security gaps or breaking existing access.

## When to Use
- Adding/modifying login, signup, logout, or session handling.
- Protecting a route/screen so only authenticated/authorized users can access it.
- Implementing role- or permission-based UI/behavior.
- Adding onboarding gates (e.g. "complete profile before accessing dashboard").
- Handling redirects related to auth state (e.g. redirect to login, redirect after login).

## When Not to Use
- Pure UI styling of an existing, unchanged auth screen.
- Tasks with no relation to authentication, sessions, roles, or protected access.

## Required Inputs
- The existing auth setup: provider/library (NextAuth, Clerk, Supabase Auth, custom JWT, Expo SecureStore-based sessions, etc.), session storage method, and existing protected-route pattern.
- The specific requirement: new protected route, new role/permission check, new auth flow step, etc.
- Roles/permissions model if relevant (from Database and Backend Logic or existing types).

## Assumptions
- An existing auth system is in place unless explicitly told this is a from-scratch setup.
- Changes here can affect access to the entire app — treat as high-impact by default.

## Step-by-Step Workflow
1. **Identify the existing auth mechanism**: provider/library, where session/token is stored (cookies, secure storage, context), and how routes are currently protected (middleware, layout-level checks, HOC, hook-based guard).
2. **Identify the existing role/permission model** (if any): where roles are defined, how checks are performed (`user.role === 'admin'`, permission arrays, claims, etc.).
3. **For new protected routes/screens**: apply the same protection pattern already used elsewhere (e.g. same middleware/layout guard), rather than inventing a new check.
4. **For new roles/permissions**: extend the existing model (add a role/permission value) rather than creating a parallel system.
5. **For redirects**:
   - Unauthenticated users attempting protected routes → redirect to login, preserving intended destination if the existing pattern supports it.
   - Post-login redirect → return to intended destination or default landing page per existing convention.
   - Onboarding gates → redirect incomplete-profile users to onboarding until complete, without creating redirect loops.
6. **For login/signup/logout flows**: follow existing form, validation, and error-handling patterns; ensure logout clears session state fully (client state, tokens/cookies) per existing convention.
7. **Check edge cases**: expired sessions, invalid tokens, role changes mid-session, direct URL access to protected routes, and concurrent tabs/devices if relevant.
8. **Test both allowed and denied access** for each new/changed check (a user who should have access, and one who shouldn't).

## Rules and Best Practices
- Reuse the existing auth provider, session pattern, and route-protection mechanism — don't introduce a second auth system.
- Apply permission checks on the backend as well as the front-end; front-end checks alone are not security (see Database and Backend Logic Skill for backend validation).
- Never hard-code credentials, tokens, or secrets in code.
- Keep role/permission logic centralized (e.g. a shared helper/hook) rather than scattering ad-hoc checks across components.
- Ensure redirect logic can't create infinite loops (e.g. login page itself must not be behind the same guard that redirects to login).
- Default to the most restrictive reasonable behavior when access rules are ambiguous, and flag the ambiguity.

## Safety Checks
- Treat any change to auth, session handling, route protection, or roles/permissions as high-impact — confirm scope with the user before broad changes (per Clarify the Request / Risk Review Skills).
- Don't weaken or remove existing protection on a route/screen as a side effect of unrelated work.
- Don't expose user data or admin-only UI/data to unauthorized roles, even temporarily during development (e.g. behind a flag that could ship enabled).

## Validation Checks
- Confirm protected routes redirect unauthenticated users correctly.
- Confirm role/permission checks correctly allow intended roles and block others.
- Confirm logout fully clears session state (no stale access after logout).
- Confirm no redirect loops are introduced.
- Confirm no secrets/tokens are exposed in front-end code or logs.

## Common Mistakes to Avoid
- Creating a new, separate auth check pattern instead of reusing the existing one.
- Relying only on front-end checks without backend validation.
- Hard-coding roles/permissions as ad-hoc string comparisons scattered across the codebase.
- Breaking existing protected routes while adding a new one.
- Creating redirect loops between login and protected pages.
- Leaving debug bypasses (e.g. "skip auth in dev") that could accidentally ship.

## Output Rule
Do not invent a custom final response format for this skill. Follow the Global Agent Output and Reporting Skill. Only include skill-specific reporting details when necessary for understanding the completed work.
