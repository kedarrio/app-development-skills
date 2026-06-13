---
name: debug-and-fix
description: Diagnose the root cause of a bug before applying the smallest correct fix. Use this skill whenever something is broken, erroring, behaving unexpectedly, or a test/build/lint is failing. Always read the actual error message and trace the relevant code before changing anything — do not apply speculative fixes. Can be invoked at any stage of development, not just during a dedicated testing phase.
---

# Debug and Fix Skill

## Purpose
Find and fix the actual root cause of a bug with the smallest correct change — without masking symptoms, guessing, or introducing new risks.

## When to Use
- An error, crash, test failure, build failure, or lint failure occurs.
- Behavior doesn't match expectations (UI shows wrong data, action doesn't do what it should, etc.).
- A previous fix didn't fully resolve the issue.

## When Not to Use
- The "bug" is actually a missing feature/requirement, not broken existing behavior — use Plan the Feature Skill instead.
- The issue is purely about code quality/structure with no broken behavior — use Refactor and Clean Up Skill.

## Required Inputs
- The actual error message/stack trace, failing test output, or a precise description of the unexpected behavior (steps to reproduce, expected vs. actual).
- Access to the relevant code and recent changes (diff/history if available).

## Assumptions
- The reported symptom may not be where the actual root cause lives.
- A fix is not correct just because the symptom disappears — it must address the actual cause.

## Step-by-Step Workflow
1. **Read the actual error message/stack trace in full** — identify the exact file, line, and error type. Don't skip to guessing based on the general area.
2. **Reproduce or confirm the issue**: understand the exact steps/conditions that trigger it.
3. **Trace the relevant code path**: follow the logic from where the error surfaces back to where the bad state/input originates. Check function inputs, types, data shapes, and recent changes along this path.
4. **Check recent changes** (git history/diff if available) for anything that could have introduced this — especially if the bug is newly reported.
5. **Form a hypothesis** about the root cause, and verify it (e.g. by inspecting the actual data/state at the relevant point, not just assuming).
6. **Identify the smallest correct fix** that addresses the root cause — not a workaround that papers over it.
7. **Apply the fix**, following Write Front-End Code / Database and Backend Logic / etc. conventions as relevant to where the fix lives.
8. **Validate the fix**: confirm the original issue is resolved (re-run the failing test/reproduce steps) and run relevant validation (see Validate and Test Skill) to confirm nothing else broke.
9. **If the root cause can't be confirmed**: state clearly what was checked, what hypotheses were ruled out, and what remains unknown — don't apply a speculative fix and call it done.

## Rules and Best Practices
- Always read the actual error/log output before forming a hypothesis.
- Trace the code path; don't fix based on the error message's surface location alone if the root cause is upstream.
- Apply the smallest correct fix — avoid rewriting large sections "while you're in there."
- Don't use `any`/`as any`, empty catch blocks, broad fallbacks, duplicated logic, or config hacks to make an error go away unless the root cause genuinely requires that specific change (and even then, document why).
- If multiple bugs are found, fix the one that's actually in scope; note others separately rather than silently expanding scope.
- After fixing, consider whether the same root cause affects other similar code paths (but don't change them speculatively without checking).

## Safety Checks
- Don't fix a bug by changing test expectations unless the test itself was actually wrong (and say so explicitly).
- Don't suppress an error (e.g. swallow exception, disable a check) as the "fix" — that's masking, not fixing.
- If the root cause touches auth, data integrity, or schema, treat the fix as higher-risk (see Risk Review Skill) even if the fix itself is small.

## Validation Checks
- Confirm the original failing case now passes/behaves correctly.
- Confirm the fix addresses the root cause, not just the symptom (explain why, briefly).
- Confirm relevant validation (lint/typecheck/test/build) still passes after the fix.
- Confirm no new errors were introduced.

## Common Mistakes to Avoid
- Guessing at a fix without reading the actual error message.
- Fixing the symptom (e.g. wrapping in try/catch to hide an error) instead of the cause.
- Large speculative rewrites "to be safe."
- Using `any`/type bypasses to silence a type error instead of fixing the type mismatch.
- Declaring a fix complete without re-running the failing case.
- Expanding scope to fix unrelated issues discovered along the way without flagging it.

## Output Rule
Do not invent a custom final response format for this skill. Follow the Global Agent Output and Reporting Skill. Only include skill-specific reporting details when necessary for understanding the completed work.
