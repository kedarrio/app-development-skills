---
name: rethink-or-reframe
description: Step back and re-evaluate the current approach when it seems too complex, fragile, misaligned with the actual goal, or going in circles. Use this skill when a plan or implementation is growing unexpectedly large, when repeated fixes aren't resolving the underlying issue, when a simpler path becomes visible mid-task, or when the original request may be solving the wrong problem. Do not use it to second-guess a working, appropriately-scoped plan without real cause.
---

# Rethink or Reframe Skill

## Purpose
Catch and correct situations where the current approach is wrong, overly complex, or unnecessary — before more time is spent building on a bad foundation.

## When to Use
- The plan or implementation is becoming much larger or more complex than the request justifies.
- Repeated debugging/fixes aren't addressing the real problem.
- A simpler, more direct solution becomes apparent mid-task.
- The original request seems to solve a symptom rather than the actual user goal.
- New information (from Understand the Project or during implementation) contradicts the original plan's assumptions.

## When Not to Use
- The current plan is working and appropriately scoped — don't second-guess it just to be thorough.
- Minor friction that doesn't indicate a wrong direction (e.g. one extra file needed).

## Required Inputs
- The current plan or in-progress implementation.
- The original request/goal.
- Whatever triggered the doubt (error pattern, growing scope, new info).

## Assumptions
- Changing direction mid-task has a cost; only do it when the benefit is clear.
- The user's underlying goal matters more than the literal original instruction if the two diverge.

## Step-by-Step Workflow
1. **Name the trigger**: what specifically suggests the current approach is wrong or too complex? (e.g. "this requires touching 12 files for a small UI tweak", "three fixes haven't resolved the error", "there's an existing utility that already does this").
2. **Restate the underlying goal** in plain terms, separate from the specific approach taken so far.
3. **Compare alternatives**: is there a simpler, smaller, or more direct way to achieve the same goal?
4. **Estimate the cost of switching**: how much of the current work is reusable vs. wasted?
5. **Decide**:
   - If the simpler path is clearly better and switching cost is low/medium — switch, and briefly note why.
   - If the current path is still reasonable despite the friction — continue, noting the tradeoff.
   - If the decision is high-impact (significant rework, affects scope/timeline materially) — surface it to the user before switching.
6. **If reframing the request itself** (the literal ask doesn't serve the actual goal), explain the mismatch and propose the better-aligned approach — don't silently do something different from what was asked.

## Rules and Best practices
- Prefer the smallest change that correctly solves the actual problem.
- Don't over-engineer: if a simple solution meets the requirement, don't build a general framework "just in case."
- Don't under-engineer: if the simple path will clearly need to be redone soon, say so.
- When switching direction mid-task, clean up any now-unused partial work from the abandoned approach (see Refactor and Clean Up Skill).
- Reframing is not an excuse to ignore the user's explicit constraints — propose, don't override.

## Safety Checks
- Don't abandon a partially-completed change without noting what state it's left in.
- If reframing changes scope significantly, treat it like a new plan — re-run Risk Review if it now touches sensitive areas.

## Validation Checks
- Confirm the new direction actually resolves the original trigger (it isn't just "different" but actually better).
- Confirm any abandoned partial work is either reverted or clearly left in a non-breaking state.
- Confirm the user's actual goal is still being met.

## Common Mistakes to Avoid
- Repeatedly rewriting the same code without identifying why the approach keeps failing.
- Silently changing what was asked for without flagging the change.
- Switching approaches late, after most of the original work is done, when continuing would have been cheaper.
- Treating "this is hard" as evidence the approach is wrong, when the task is just inherently complex.
- Leaving dead code/files from an abandoned approach.

## Output Rule
Do not invent a custom final response format for this skill. Follow the Global Agent Output and Reporting Skill. Only include skill-specific reporting details when necessary for understanding the completed work.
