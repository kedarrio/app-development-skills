---
name: error-handling-review
description: Review and improve loading, error, empty, success, retry, and fallback states for a feature or screen. Use this skill after implementing data-driven UI or actions, when reviewing a feature for completeness before handoff, or when a bug report describes a missing/incorrect state (e.g. "no error shown when the request fails", "infinite spinner", "blank screen with no data").
---

# Error Handling Review Skill

## Purpose
Ensure every data-driven UI and action has correct, user-useful handling for loading, error, empty, success, retry, and fallback states — without hiding real problems behind generic fallbacks.

## When to Use
- After connecting UI to data/APIs (see Connect Data and API Skill).
- Reviewing a feature/screen for completeness before handoff or launch.
- Investigating a bug related to missing or incorrect state handling.

## When Not to Use
- Static, non-data-driven UI with no async operations.
- The states have already been reviewed and nothing changed since.

## Required Inputs
- The screen/feature and its data operations (reads, writes, async actions).
- Existing patterns for loading/error/empty UI in the project (spinners, skeletons, error banners, empty-state components).

## Assumptions
- Every async data operation the UI depends on should have defined loading, error, empty (if applicable), and success states.
- Errors should be surfaced to the user in a useful way, not hidden or generically swallowed.

## Step-by-Step Workflow
1. **List all async operations** on the screen/feature: data fetches, mutations (create/update/delete), file uploads, etc.
2. **For each operation, check**:
   - **Loading**: is there a visible loading indicator (spinner/skeleton) while the operation is in progress? Does it avoid layout jumps where reasonable?
   - **Error**: if the operation fails, does the user see a clear message (per Write Product Text Skill)? Is there a retry option where retrying makes sense?
   - **Empty**: if the operation succeeds but returns no data, is there a distinct empty state (not just a blank area)?
   - **Success**: does the UI update correctly to reflect the new state (e.g. list updates after creation, confirmation shown after save)?
   - **Fallback**: for non-critical optional data (e.g. an avatar image, an optional widget), is there a sensible fallback that doesn't break the page if it fails?
3. **Check error propagation**: errors from the data layer should reach the UI layer (not be swallowed in a service/hook with an empty catch).
4. **Check retry behavior**: retries should be available where the user can reasonably resolve the issue (e.g. network blip) and should not retry indefinitely or spam the backend.
5. **Check for "infinite loading"**: ensure loading states have a defined end condition (success, error, or timeout) — no states that can hang forever without feedback.
6. **Check for fake/placeholder success**: confirm success states only show when the operation actually completed, not optimistically faked without real confirmation (unless the project intentionally uses optimistic updates with rollback on failure).

## Rules and Best Practices
- Every user-triggered async action should give feedback: in progress, succeeded, or failed.
- Error messages should be specific enough to be useful (see Write Product Text Skill) — avoid only "Something went wrong" when more specific info is available.
- Don't use broad try/catch blocks that swallow errors without surfacing or logging them.
- Empty states should be distinguishable from loading and error states.
- Critical content failures should show an error state; non-critical content failures should degrade gracefully (fallback) without breaking the whole page.
- Retry actions should be idempotent or safe to repeat where possible.

## Safety Checks
- Don't add a fallback that masks a real bug (e.g. catching an error and rendering an empty list, making it look like "no data" when it's actually "request failed").
- Don't remove existing error handling while making other changes.

## Validation Checks
- Confirm every async operation on the screen has loading, error, and (if applicable) empty states implemented.
- Confirm error states show useful messages and, where appropriate, a retry action.
- Confirm no operation can leave the UI in a permanent loading state with no error/timeout path.
- Confirm fallbacks are used only for genuinely non-critical content, not to hide real failures.

## Common Mistakes to Avoid
- Showing a blank screen on error instead of an error message.
- Treating "empty result" and "request failed" as the same state.
- Infinite spinners with no error/timeout handling.
- Swallowing errors in a catch block without surfacing or logging them.
- Faking success UI without confirming the operation actually completed (outside of an intentional optimistic-update pattern with rollback).
- Removing existing error handling as a side effect of other changes.

## Output Rule
Do not invent a custom final response format for this skill. Follow the Global Agent Output and Reporting Skill. Only include skill-specific reporting details when necessary for understanding the completed work.
