---
name: global-agent-output-and-reporting
description: Standardize how the agent reports completed work — task understood, actions taken, files touched, architecture rules followed, validation attempted/result, assumptions, risks/unresolved issues, unrelated failures, and recommended next steps. This is the central reporting skill referenced by every other skill's "Output rule." Use it at the end of any task to structure the final response to the user. Always use this format instead of inventing a custom report structure.
---

# Global Agent Output and Reporting Skill

## Purpose
Provide one consistent, honest, scannable reporting format for completed work, so the user always knows what was done, how it was verified, what's assumed, and what (if anything) still needs attention — regardless of which other skill(s) were used.

## When to Use
- At the end of any task that produced changes, a plan, an analysis, or any other deliverable.
- After Review Before Final Skill has confirmed the work against the original request.

## When Not to Use
- For trivial conversational replies with no work performed (e.g. answering a quick question with no changes, no files, nothing to validate). In that case, just answer directly — don't force this structure onto a one-line answer.

## Required Inputs
- The original request and clarified scope.
- The findings from Review Before Final Skill.
- A record of: files created/modified/moved/deleted, architecture decisions followed, validation run and its results, assumptions made, risks/issues found, and any unrelated failures encountered.

## Assumptions
- The user wants an accurate picture of what happened, not just a "done" signal.
- Sections with nothing to report can be omitted or marked "None" — don't pad the report with empty sections written out at length.

## Step-by-Step Workflow
1. **Gather inputs** from the work performed and from Review Before Final Skill's findings.
2. **Fill in each section of the reporting structure** (below) based on what actually happened — only include details that help the user understand the completed work.
3. **Be concise**: use short statements/lists; avoid restating the entire conversation or over-explaining simple changes.
4. **Be honest**: if something wasn't done, wasn't validated, or is uncertain, say so plainly — don't imply completeness that wasn't achieved.
5. **Surface anything actionable**: risks, unresolved issues, and next steps should be specific enough that the user (or the next agent) can act on them directly.
6. **Skip empty sections** or mark them "None" rather than leaving placeholders or over-explaining the absence.

## Rules and Best Practices
- Use this format for the final response instead of a skill-specific format, even when multiple skills were used in the task.
- Only include skill-specific reporting details (e.g. specific QA steps performed, specific architecture decisions) when they help the user understand the completed work — don't mechanically list every skill used.
- Be specific about file paths, not vague references ("a few components were updated").
- Be specific about what changed, not just that something changed.
- Don't over-explain simple, low-risk changes — a one-line summary plus the structure below (with empty sections omitted) is fine for small tasks.
- For larger tasks, the structure below should still be scannable — use short bullets, not long paragraphs.

## Safety Checks
- Never state that validation passed if it wasn't run, or that a risky action was taken if it wasn't approved.
- Never omit a known risk or unresolved issue to make the report look cleaner.
- Never claim a file was created/modified/deleted if that didn't actually happen.

## Validation Checks
- Confirm every file listed as created/modified/moved/deleted actually was.
- Confirm the validation section accurately reflects what was run and its real outcome.
- Confirm assumptions and risks listed match what was actually encountered during the task (cross-check with Clarify the Request, Risk Review, and Review Before Final outputs).

## Common Mistakes to Avoid
- Inventing a different report format per task or per skill.
- Padding the report with long explanations of simple changes.
- Saying "all tests pass" without having run them.
- Burying a real risk or unresolved issue inside a long paragraph instead of the dedicated section.
- Listing files that weren't actually touched, or omitting ones that were.

## Output Rule (Full Reporting Structure)

Structure the final response using the following sections. Omit a section (or write "None") if there's nothing to report for it — do not pad.

### Task understood
A short restatement of what was requested and the scope that was actually addressed (including any clarifications/assumptions that shaped scope).

### Actions taken
A concise, ordered summary of what was actually done (e.g. "Added X component", "Updated Y service to support Z", "Fixed bug in A causing B").

### Files created
List of new file paths, each with a one-line description of its purpose.

### Files modified
List of changed file paths, each with a one-line description of what changed.

### Files moved or deleted
List of any files moved (old path → new path) or deleted, with a one-line reason. If none, state "None."

### Architecture rules followed
Brief note on which structural conventions were followed (existing project convention vs. default rule of thumb) — especially relevant if a new pattern/location was introduced.

### Validation attempted
List of validation steps attempted (e.g. lint, typecheck, test, build, manual QA) and what was actually run. If none were run, state why.

### Validation result
The outcome of each validation step run (pass/fail), distinguishing failures caused by this task (and whether fixed) from unrelated pre-existing failures.

### Assumptions made
List of assumptions made during the task (from Clarify the Request and elsewhere) that could affect the result, stated plainly.

### Risks or unresolved issues
Any flagged risks (from Risk Review), known limitations, edge cases not handled, or issues that still need attention. If none, state "None."

### Unrelated failures
Any pre-existing issues discovered but not fixed because they're out of scope (e.g. unrelated failing tests, existing lint errors elsewhere). If none, state "None."

### Recommended next steps
Concrete, actionable next steps — for the user or for whoever continues the work (may overlap with Handoff Notes Skill output if the task is incomplete).
