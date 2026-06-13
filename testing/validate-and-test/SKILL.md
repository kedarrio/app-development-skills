---
name: validate-and-test
description: Run or recommend the project's existing lint, typecheck, test, and build commands to validate changes. Use this skill after making code changes, before reporting work as complete, to confirm the change builds/compiles/passes existing checks. Also use it to identify and report pre-existing failures unrelated to the current task.
---

# Validate and Test Skill

## Purpose
Confirm that code changes don't break existing lint, type, test, or build checks — using the project's own tooling — and clearly separate failures caused by this task from pre-existing issues.

## When to Use
- After completing code changes, before reporting the task as done.
- When asked to verify a change works or "make sure nothing broke."
- When investigating whether a reported issue is caused by the current change or pre-existing.

## When Not to Use
- Pure planning/documentation tasks with no code changes.
- When no validation tooling exists and running ad-hoc checks wouldn't add value (state this rather than skipping silently).

## Required Inputs
- `package.json` (or equivalent) to identify available scripts: lint, typecheck, test, build, format.
- The set of files changed in this task.

## Assumptions
- Existing scripts are the source of truth for how to validate — don't invent new validation commands.
- Validation should be scoped reasonably (e.g. run relevant test files/packages first if the project is large and full runs are slow), but a full check should be attempted when feasible.

## Step-by-Step Workflow
1. **Check `package.json` (or project equivalent)** for available scripts: `lint`, `typecheck`/`tsc`, `test`, `build`, `format`/`format:check`.
2. **Run relevant commands** for the type of change made:
   - Front-end/TS changes → typecheck + lint at minimum; build if feasible.
   - Logic changes with existing tests → run relevant test suite(s), or full test run if scoped tests aren't clearly identifiable.
   - Config/dependency changes → build, and relevant tests.
3. **Capture results**: note pass/fail for each command run.
4. **For failures**:
   - Determine whether the failure is caused by this task's changes or pre-existing (check if the same failure occurs on unrelated/unchanged files, or existed before the change if that can be determined).
   - If caused by this task: fix it (see Debug and Fix Skill) and re-run validation.
   - If pre-existing/unrelated: do not attempt to fix unless asked; report it separately as a pre-existing issue.
5. **If validation cannot be run** (no scripts exist, environment limitations, command errors out for environment reasons): state clearly why, and suggest manual validation steps (see Manual QA and Regression Skill) as a fallback.
6. **Re-run after fixes** to confirm the fix resolved the issue without introducing new ones.

## Rules and Best Practices
- Use only the project's existing validation scripts/tools — don't introduce new linters/test runners without approval (see Dependency and Config Skill).
- Never claim validation passed unless it was actually run and actually passed.
- Always distinguish failures caused by this task from unrelated pre-existing failures.
- If a full test/build run is too slow/impractical, run the most relevant subset and state that a full run wasn't performed.
- Fix failures caused by the current task before considering the task complete; report unrelated failures without fixing them (unless asked).

## Safety Checks
- Don't modify test files just to make them pass if the underlying code is actually wrong — fix the code (or flag if the test itself seems incorrect, rather than silently changing its expectations).
- Don't disable/skip failing tests or lint rules to force a pass.

## Validation Checks
- Confirm which commands were run and their results (pass/fail).
- Confirm any failures were triaged as task-caused (fixed) vs. pre-existing (reported separately).
- Confirm re-validation was performed after any fix.

## Common Mistakes to Avoid
- Saying "tests pass" without running them.
- Fixing unrelated pre-existing failures as part of this task without flagging the scope change.
- Disabling a failing test/lint rule instead of fixing the issue.
- Running an unrelated/foreign validation tool not used by the project.
- Not re-running validation after a fix to confirm it actually worked.

## Output Rule
Do not invent a custom final response format for this skill. Follow the Global Agent Output and Reporting Skill. Only include skill-specific reporting details when necessary for understanding the completed work.
