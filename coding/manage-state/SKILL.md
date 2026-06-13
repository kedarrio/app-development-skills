---
name: manage-state
description: Decide where state belongs — local, shared, global, URL, or server/cache state — and implement it without unnecessary global state or duplication. Use this skill whenever a task involves adding, moving, or refactoring state (component state, context, global stores, URL params, server/cache state via React Query/SWR, etc.), or when reviewing whether existing state is in the right place.
---

# Manage State Skill

## Purpose
Place state in the right layer — local, shared, global, URL, or server/cache — so the app stays predictable, avoids duplication, and follows the project's existing state conventions.

## When to Use
- A new piece of UI needs state (form input, toggle, selection, etc.) and its scope needs to be decided.
- A feature requires sharing state between components/screens.
- Reviewing or refactoring existing state that seems misplaced, duplicated, or overly global.

## When Not to Use
- The state is trivially local and already correctly implemented (e.g. a single input's controlled value) — no action needed.
- Pure server data fetching with no client state involved (see Connect Data and API Skill, though server/cache state decisions overlap here).

## Required Inputs
- What the state represents and which components/screens need access to it.
- The project's existing state conventions (Context, Redux, Zustand, Jotai, React Query/SWR, URL params, etc.) from Understand the Project Skill.

## Assumptions
- Local state is the default; shared/global state is justified only when multiple distant components genuinely need it.
- The project's existing state library/pattern should be used — don't introduce a new one without approval.

## Step-by-Step Workflow
1. **Classify the state**:
   - **Local**: only one component (and maybe its direct children) needs it → `useState`/`useReducer` in that component.
   - **Shared (lifted)**: a few closely related components need it → lift to the nearest common parent, pass via props, or a small local context.
   - **Global**: truly app-wide state needed across distant, unrelated parts of the app (auth/session, theme, app-wide settings) → project's global store (Redux/Zustand/Jotai/Context).
   - **URL/search params**: state that represents navigation/filtering/sorting that should be shareable/bookmarkable → URL params (framework router).
   - **Server/cache state**: data from the backend → React Query/SWR/server components/cache layer, not duplicated into local/global state.
2. **Check for existing state holding similar data** — avoid creating a second source of truth for the same information.
3. **Implement using the project's existing pattern** for the chosen category (e.g. existing Zustand store, existing Context provider, existing React Query setup).
4. **Avoid derived state duplication**: if a value can be computed from existing state/props, compute it (e.g. via `useMemo`) rather than storing it separately and keeping it in sync.
5. **For global state additions**: confirm the addition is genuinely global; if it's only needed by a few components, prefer lifting state instead of adding to the global store.
6. **For URL state**: ensure navigation updates the URL appropriately and reading state from the URL doesn't conflict with other state sources.
7. **Clean up**: remove any now-unused state introduced by a previous, different approach.

## Rules and Best Practices
- Use local state first; escalate only when there's a real need to share.
- Don't duplicate the same piece of state in multiple places (e.g. both in a global store and as local component state).
- Don't store derived/computed values as separate state unless there's a clear performance or architectural reason.
- Prefer URL/search params for state that affects what's shown and should be shareable (filters, active tab, pagination).
- Prefer server/cache state patterns (React Query/SWR/etc.) for remote data — don't copy server data into a global store unless the project already does this intentionally.
- Follow the project's existing state management library/pattern; don't add a new state library without approval.
- Keep global stores organized by domain/feature, not as one giant catch-all object, if the project already has domain-organized stores.

## Safety Checks
- Adding to a global store affects app-wide state — check for naming collisions and unintended re-renders in unrelated components.
- Removing/renaming existing global state keys can break multiple consumers — search for usages first.

## Validation Checks
- Confirm the chosen state scope matches actual usage (not broader than needed, not narrower than needed).
- Confirm no duplicate sources of truth exist for the same data.
- Confirm derived values aren't unnecessarily stored as separate state.
- Confirm existing consumers of any changed/removed state still work.

## Common Mistakes to Avoid
- Putting everything in global state "just in case."
- Storing server data in both a global store and component state, causing sync issues.
- Storing derived values (e.g. a filtered list) as state instead of computing them.
- Introducing a new state management library alongside an existing one.
- Lifting state higher than necessary, causing unrelated components to re-render.
- Breaking other consumers when renaming/removing global state.

## Output Rule
Do not invent a custom final response format for this skill. Follow the Global Agent Output and Reporting Skill. Only include skill-specific reporting details when necessary for understanding the completed work.
