---
name: ux-flow-and-information-architecture
description: Plan screens, navigation, user flows, content structure, and cross-screen logic before building UI. Use this skill when a feature involves multiple screens or steps, when navigation/routing structure needs to be decided, when content hierarchy on a screen is unclear, or when a flow has branching paths (e.g. different states for different user roles). Do not use it for single-screen, single-purpose UI with an obvious layout.
---

# UX Flow and Information Architecture Skill

## Purpose
Define how users move through the app and how content/information is structured, so screens and navigation are coherent before component-level work begins.

## When to Use
- A feature spans multiple screens or steps (e.g. onboarding, checkout, multi-step forms).
- Navigation structure needs to be added or changed (new routes, tabs, modals vs. pages).
- A screen's content hierarchy or grouping is unclear.
- Different user states/roles need different flows or views.

## When Not to Use
- A single, self-contained screen with an obvious, simple layout.
- The flow is already defined and just needs implementation.

## Required Inputs
- The feature/goal driving the flow.
- Existing navigation structure (routes, tabs, nav bars, modals) from Understand the Project Skill.
- User roles/permissions if relevant.

## Assumptions
- Navigation patterns should match the framework's routing conventions (Next.js App Router segments, Expo Router file-based routes, Vite + React Router routes).
- Simpler flows are preferred when they meet the requirement.

## Step-by-Step Workflow
1. **Define the user goal**: what is the user trying to accomplish, end to end?
2. **List the steps/screens** required to accomplish it, in order.
3. **For each step, define**:
   - Entry point (how the user gets here).
   - Exit points (where the user can go next: continue, back, cancel, error).
   - Required content/data on that screen.
   - Primary action and secondary actions.
4. **Identify branching**: different roles, permissions, or states (e.g. logged in vs. guest, empty vs. populated) that change the flow.
5. **Decide navigation structure**: new route(s) vs. modal/sheet vs. inline expansion — follow existing patterns in the app for similar flows.
6. **Define information hierarchy per screen**: what's primary, secondary, tertiary; group related content; avoid unnecessary nesting.
7. **Note cross-screen state**: what data/state needs to persist or pass between screens (and flag for Manage State Skill).
8. **Check for unnecessary steps**: can any screen/step be removed or merged without hurting clarity?

## Rules and Best Practices
- Keep flows predictable: consistent placement of primary actions, back/cancel behavior, and navigation patterns across the app.
- Prefer the minimum number of steps that accomplishes the goal clearly.
- Match existing navigation idioms (e.g. if other multi-step flows in the app use a stepper, reuse that pattern).
- Define empty, loading, and error variants of each screen's content as part of the flow, not as an afterthought.
- For role-based flows, be explicit about what each role sees/can do at each step.
- Keep routing decisions consistent with the framework's conventions (don't invent custom routing patterns the framework doesn't support well).

## Safety Checks
- Changes to top-level navigation structure (adding/removing major routes or tabs) can be high-impact — flag if this affects many existing screens.
- Flows involving auth/permission boundaries should be cross-checked with the Auth and Access Skill.

## Validation Checks
- Confirm every step has defined entry/exit points (no dead ends).
- Confirm every step accounts for loading/empty/error states.
- Confirm role/permission branches are complete (no undefined state for a given role).
- Confirm the flow doesn't introduce more steps than necessary.

## Common Mistakes to Avoid
- Designing a flow without considering error/empty/loading states until later.
- Adding new top-level navigation when the flow could be a modal/step within an existing screen.
- Leaving "dead end" screens with no clear next action.
- Ignoring how different roles/permissions affect the flow.
- Overcomplicating a flow that could be a single screen with progressive disclosure.

## Output Rule
Do not invent a custom final response format for this skill. Follow the Global Agent Output and Reporting Skill. Only include skill-specific reporting details when necessary for understanding the completed work.
