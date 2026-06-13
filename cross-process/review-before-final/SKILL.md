---
name: review-before-final
description: Check whether the completed work actually satisfies the original request before responding to the user. Use this skill as the last step of any non-trivial task — after coding, fixing, refactoring, or planning — to confirm the request was fully addressed, validation was performed, conventions were followed, and nothing was missed or silently skipped. This is the gate before the Global Agent Output and Reporting Skill.
---

# Review Before Final Skill

## Purpose
Catch gaps between what was asked and what was delivered before reporting completion — ensuring the response is accurate, complete, and honest about what was and wasn't done.

## When to Use
- As the final step before reporting any non-trivial completed task.
- After Debug and Fix, Refactor and Clean Up, or any multi-step implementation.

## When Not to Use
- Extremely trivial tasks where the work obviously and fully matches the request (e.g. answering a quick factual question with no code change).

## Required Inputs
- The original request (and any clarified scope from Clarify the Request Skill).
- The plan, if one was made (Plan the Feature Skill).
- The actual changes made.
- Validation results (Validate and Test Skill) and manual QA results (Manual QA and Regression Skill) if applicable.

## Assumptions
- The original request is the source of truth for "done," not just what was technically easiest to implement.
- It's better to report an honest gap than to claim full completion.

## Step-by-Step Workflow
1. **Re-read the original request** (and clarified scope) and list its distinct requirements/asks.
2. **For each requirement, check**: was it addressed? Fully, partially, or not at all?
3. **Check the plan vs. actual**: if a plan was made, did the implementation follow it? Note any deviations and why.
4. **Check edge cases and states**: were the edge cases identified during planning actually handled (per Error Handling Review / Manual QA Skills)?
5. **Check conventions**: does the work follow the project's existing structure, styling, naming, and patterns (per Understand the Project Skill findings)?
6. **Check validation**: was lint/typecheck/test/build run, and did it pass? If not run, why not?
7. **Check for leftover issues**: unused code, debug logs, placeholder text, TODOs without follow-ups, files left in an inconsistent state.
8. **Check risk items**: were any flagged risks (Risk Review Skill) resolved, approved, or clearly reported as outstanding?
9. **If gaps are found**:
   - If small and within scope: fix them now before reporting.
   - If they represent missing scope or require new approval: report them honestly as incomplete/outstanding rather than claiming done.

## Rules and Best Practices
- Treat the original request as the checklist — don't redefine "done" to match only what was built.
- Don't claim something works if it wasn't validated or tested.
- Don't hide partial completion — report it clearly.
- If scope grew or shrank during the task (Rethink or Reframe Skill), confirm the final result still serves the user's actual goal.
- Do a final pass for cleanliness: no stray debug code, no unused imports, no placeholder text.

## Safety Checks
- Confirm no risky/destructive action was performed without the required approval (cross-check Risk Review Skill).
- Confirm no security/auth/permission checks were weakened or removed unintentionally.

## Validation Checks
- Confirm every requirement from the original request has a clear status (done / partially done / not done, with reason).
- Confirm validation (automated and/or manual) was performed and its results are accurately represented.
- Confirm no leftover debug artifacts, dead code, or placeholder content remain.

## Common Mistakes to Avoid
- Reporting "done" when a requirement was missed or only partially addressed.
- Skipping this check on "small" tasks that turned out to have more requirements than expected.
- Claiming validation passed without having run it.
- Failing to mention a scope change that happened mid-task.
- Leaving debug logs/placeholder text in because the core logic "works."

## Output Rule
Do not invent a custom final response format for this skill. Follow the Global Agent Output and Reporting Skill. The findings from this review feed directly into that skill's reporting structure (task understood, validation result, assumptions, risks/unresolved issues, next steps).
