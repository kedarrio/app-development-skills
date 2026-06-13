---
name: plan-the-feature
description: Turn a feature idea or request into a concrete, buildable plan — requirements, affected files, components, data needs, edge cases, and build order. Use this skill before writing any code for a non-trivial feature, when a request describes a goal rather than exact implementation steps, or when multiple files/areas of the app will be touched. Skip it for one-line fixes or single-file tweaks.
---

# Plan the Feature Skill

## Purpose
Convert a feature request into a clear, ordered implementation plan so coding proceeds with minimal rework, conflicts, or missed edge cases.

## When to Use
- The request describes a feature, flow, or capability rather than a specific code edit.
- The feature will touch multiple files, layers (UI, data, state), or screens.
- The build order matters (e.g. data layer before UI, or types before components).

## When Not to Use
- The task is a small, single-file change with an obvious implementation.
- A plan already exists (from a previous turn) and is still valid/unchanged.

## Required Inputs
- The feature request (clarified via the Clarify the Request Skill if needed).
- Project context from the Understand the Project Skill (framework, structure, conventions).

## Assumptions
- The plan should follow existing project conventions and the default architecture rule of thumb only where no stronger convention exists.
- The plan may be adjusted later via the Rethink or Reframe Skill if it proves too complex or wrong.

## Step-by-Step Workflow
1. **Restate the goal** in one or two sentences: what should the user be able to do after this feature ships?
2. **List requirements**: functional requirements (what it must do) and constraints (performance, permissions, platforms).
3. **Identify affected areas**:
   - Screens/routes involved.
   - Components to create or extend.
   - Data/API needs (new endpoints, existing endpoints to reuse, new types).
   - State changes (local, shared, global, server/cache state).
   - Backend/database changes if any.
4. **List edge cases**: empty states, error states, permission/role differences, slow network, no data, max/min values, concurrent actions.
5. **Map files**: for each affected area, name the specific file(s) to create or modify, following existing structure (or the default rule of thumb if none exists).
6. **Determine build order**: typically types/data layer → state/hooks → components → page/screen assembly → polish (loading/error/empty states) → tests/validation. Adjust based on dependencies.
7. **Flag risks**: anything touching auth, schema, shared components used elsewhere, or config — note for the Risk Review Skill.
8. **Confirm scope is appropriate**: if the plan reveals the feature is much larger or more complex than expected, surface this before starting (see Rethink or Reframe Skill).

## Rules and Best Practices
- Keep the plan proportional — a 2-file feature doesn't need a 10-step plan.
- Reuse existing components, services, and types before planning new ones.
- Plan for loading, error, empty, and success states from the start, not as an afterthought.
- Order steps so that types and data contracts come before UI that depends on them.
- Note any new dependency that might be needed, but don't plan to install it without flagging it (see Dependency and Config Skill).
- If the feature naturally splits into independent pieces, note which can be built/validated incrementally.

## Safety Checks
- If the plan requires schema changes, new auth rules, or changes to shared/global files, flag this explicitly as higher-risk before proceeding.
- Do not plan destructive operations (data deletion, overwrites of existing user data) without flagging for explicit approval.

## Validation Checks
- Confirm the plan covers: requirements, affected files, data needs, state needs, edge cases, and build order.
- Confirm the plan aligns with existing project structure and conventions (cross-check with Understand the Project Skill findings).
- Confirm no step depends on something not yet planned (no out-of-order dependencies).

## Common Mistakes to Avoid
- Jumping straight to code without identifying all affected files first.
- Forgetting edge cases (empty/error/loading) until QA.
- Planning new components that duplicate existing ones.
- Over-planning a small feature with unnecessary abstraction layers.
- Ignoring build order and ending up with UI built against data shapes that don't exist yet.

## Output Rule
Do not invent a custom final response format for this skill. Follow the Global Agent Output and Reporting Skill. Only include skill-specific reporting details when necessary for understanding the completed work.
