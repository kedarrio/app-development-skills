---
name: connect-data-and-api
description: Connect UI to APIs or backend data through services, hooks, or framework data-fetching patterns — including types, loading states, error states, and clean data flow. Use this skill whenever a task involves fetching, sending, or syncing data between the front-end and an API/backend (REST, GraphQL, server actions, RPC). Do not use it for database schema/query work itself (see Database and Backend Logic Skill) or for pure UI-only tasks.
---

# Connect Data and API Skill

## Purpose
Wire UI to data sources through a clean, typed, reusable data layer — with proper loading, error, empty, and success handling — without scattering API calls across components.

## When to Use
- A component/screen needs to fetch, create, update, or delete data via an API.
- Existing data-fetching code needs new endpoints, parameters, or response handling.
- Data flow between UI and backend needs to be reviewed or cleaned up.

## When Not to Use
- The data is fully static/local with no API involved.
- The task is about the backend implementation itself (schema, queries, server routes) — see Database and Backend Logic Skill (this skill covers the front-end-facing connection).

## Required Inputs
- The data needed (shape, source, operation: read/create/update/delete).
- Existing data layer conventions: services, hooks, server actions, React Query/SWR, fetch wrappers, GraphQL client, etc.
- Existing types for requests/responses if any.

## Assumptions
- API calls live in a service/data layer (`/services`, hooks, loaders, or framework-appropriate data layer) — not directly inside visual components.
- The project's existing data-fetching pattern (React Query, SWR, server actions, plain fetch, etc.) should be followed, not replaced.

## Step-by-Step Workflow
1. **Identify the existing data-fetching pattern**: look for existing services/hooks/loaders that call similar endpoints; follow the same pattern (client library, error handling style, auth header injection, base URL config).
2. **Define or confirm types** for the request and response shapes (in `/types` or co-located per convention). Keep types consistent with the actual API response — don't guess fields that don't exist.
3. **Implement the data call** in the appropriate layer:
   - Service/data function that performs the fetch/mutation.
   - Hook (if the project uses hooks for data, e.g. `useUsers()`).
   - Framework data pattern (server actions, loaders) if that's the convention.
4. **Handle states**:
   - Loading: expose a loading flag/state for the UI to render a loading indicator.
   - Error: capture and expose error info; don't swallow errors silently.
   - Empty: distinguish "no data yet" vs. "loaded but empty result."
   - Success: return typed data ready for the UI.
5. **Wire the UI**: consume the service/hook in the component/page, rendering loading/error/empty/success states appropriately (see Error Handling Review Skill for deeper review).
6. **Avoid duplicate clients**: if an API client/base config already exists, reuse it; don't create a second fetch wrapper.
7. **Never hard-code secrets**: API keys/tokens come from environment config per project convention, never committed inline.
8. **For mutations**: confirm UI reflects the result (e.g. refetch, cache update, optimistic update per existing pattern) — don't fake a success state without actually performing/confirming the operation.

## Rules and Best Practices
- Keep API calls in the service/data layer, not in visual components.
- Reuse existing API clients, base URL config, and auth handling.
- Keep request/response types reusable and accurate to the real API.
- Handle loading, error, empty, and success states for every data operation that the UI depends on.
- Don't hide errors with broad try/catch blocks that silently swallow failures — surface them to the UI or calling code.
- Don't fake successful states (e.g. hard-coded "saved!" message) when the actual data flow isn't implemented yet — implement it or clearly mark it as not yet connected.
- Follow the project's existing pattern for caching/refetching (React Query, SWR, etc.) rather than introducing a new one.

## Safety Checks
- Never place API keys, tokens, or secrets in front-end code or commit them inline — use environment variables per project convention.
- Mutations that delete or overwrite data should follow existing confirmation patterns in the UI; don't add a destructive action without a confirmation step if the project convention requires one.

## Validation Checks
- Confirm types match real API responses (spot-check against actual response shape if possible).
- Confirm loading/error/empty/success states are all handled and visible in the UI.
- Confirm no duplicate API client/service was created when one already existed.
- Confirm no secrets are hard-coded.
- Confirm mutations actually perform the operation (no faked success).

## Common Mistakes to Avoid
- Calling `fetch`/API clients directly inside UI components instead of the data layer.
- Creating a second API client or service module that duplicates an existing one.
- Swallowing errors with empty `catch` blocks or generic fallbacks that hide real failures.
- Faking a "success" UI state without an implemented backend call.
- Hard-coding secrets or environment-specific URLs.
- Defining types that don't match the actual API response shape.

## Output Rule
Do not invent a custom final response format for this skill. Follow the Global Agent Output and Reporting Skill. Only include skill-specific reporting details when necessary for understanding the completed work.
