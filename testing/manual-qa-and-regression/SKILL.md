---
name: manual-qa-and-regression
description: Manually walk through user flows, edge cases, and visual states to check whether a change works correctly and whether existing behavior broke. Use this skill after implementing a feature or fix, especially when automated tests are insufficient or don't exist, when the change affects UI/UX, or when a shared component/page was modified and other usages need checking. Complements Validate and Test (automated checks).
---

# Manual QA and Regression Skill

## Purpose
Verify that a change works as intended across realistic user flows and edge cases, and that it didn't break existing behavior elsewhere — especially where automated coverage is thin.

## When to Use
- After implementing/changing UI, flows, or shared components.
- When automated tests don't cover the changed behavior.
- When the change touches a component/page/utility used in multiple places.

## When Not to Use
- Pure backend/internal refactors fully covered by automated tests with no user-facing impact (still worth a quick sanity check, but deep manual QA isn't necessary).
- Documentation-only changes.

## Required Inputs
- The feature/fix and its intended behavior.
- The list of affected files/components/pages, including other places that use changed shared code.
- Relevant edge cases identified during planning (Plan the Feature Skill).

## Assumptions
- Manual QA targets realistic user actions, not just "does it render."
- Regression checks focus on areas plausibly affected by the change, not the entire app, unless the change is broad (e.g. shared layout/component/global state).

## Step-by-Step Workflow
1. **Define the happy path**: the primary intended flow — walk through it step by step as a user would.
2. **Check edge cases** identified during planning:
   - Empty data, maximum/minimum values, invalid input, slow/failed network, permission/role differences.
3. **Check visual states**: default, loading, error, empty, success, disabled, hover/focus where applicable — confirm each renders correctly and matches intended copy/design.
4. **Check responsive behavior** if UI changed (see Responsive UI Skill) — at least a quick check at small and large widths.
5. **Regression-check affected shared code**: for any shared component/utility/state changed, identify other places it's used and verify they still behave correctly.
6. **Check navigation**: links/buttons lead where expected; back/cancel behavior works; no dead ends introduced.
7. **Check persistence/data**: if data is created/updated/deleted, confirm it's reflected correctly after refresh/re-navigation (per the project's data flow).
8. **Record findings**: what was checked, what passed, what failed (and was fixed), and what couldn't be checked (e.g. no way to simulate a certain role/environment).

## Rules and Best Practices
- Prioritize checks based on what changed — don't attempt to manually re-test the entire app for a small change, but do check all direct consumers of changed shared code.
- Test both the "should work" and "should be blocked/handled" cases (e.g. a permission check should allow the right role and block the wrong one).
- Verify copy/text matches what was implemented in Write Product Text Skill (no leftover placeholder text).
- If a manual check reveals a bug, fix it (or flag it) before considering the task complete — don't report success if a manual check failed.
- Where automated tests could reasonably cover what was manually checked and don't yet exist, note this as a possible follow-up (don't necessarily write tests unless asked).

## Safety Checks
- If manual QA reveals that a shared component change broke another page/flow, treat this as a regression to fix before completing the task — don't leave other areas broken.
- Don't perform manual QA steps that would cause real side effects in a way that's hard to undo (e.g. sending real emails, real payments) without flagging this first.

## Validation Checks
- Confirm the primary flow works end-to-end.
- Confirm identified edge cases behave correctly (or are explicitly noted as unhandled, with a plan).
- Confirm other usages of changed shared code still work.
- Confirm no placeholder/lorem-ipsum text remains in user-facing copy.

## Common Mistakes to Avoid
- Only checking the happy path and skipping edge cases identified during planning.
- Not checking other usages of a changed shared component, missing a regression.
- Reporting success without actually walking through the flow.
- Ignoring visual states (loading/error/empty) because "the data usually loads fine."
- Performing QA steps that cause real, hard-to-undo side effects without warning.

## Output Rule
Do not invent a custom final response format for this skill. Follow the Global Agent Output and Reporting Skill. Only include skill-specific reporting details when necessary for understanding the completed work.
