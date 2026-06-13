---
name: handoff-notes
description: Prepare clear continuation notes for another developer or AI agent picking up the work. Use this skill when a task is partially complete and work will continue later/by someone else, when ending a session with open threads, or when explicitly asked for handoff/continuation notes. Distinct from Document the Work (which updates permanent project docs) — handoff notes are about the current state and what's next.
---

# Handoff Notes Skill

## Purpose
Give the next person/agent everything they need to continue the work efficiently: what's done, what's in progress, what's left, and anything they need to know before continuing.

## When to Use
- A task is incomplete at the end of a session and work will resume later.
- Explicitly asked for handoff/continuation notes.
- A task is complete but has follow-ups, caveats, or context the next person should know.

## When Not to Use
- The task is fully complete with no follow-ups, and the Global Agent Output and Reporting Skill's summary already covers everything needed.

## Required Inputs
- Current state of the work: what's done, what's in progress, what's not started.
- Any blockers, open questions, or assumptions made.
- Relevant file paths and context needed to resume.

## Assumptions
- The reader has access to the repo but not to this conversation's full context — notes must be self-contained.
- The reader may be a different AI agent or a human developer — write for both.

## Step-by-Step Workflow
1. **Summarize the goal**: what was the task trying to accomplish?
2. **State current status**: done / in progress / not started, in concrete terms (not "mostly done" — say what specifically works and what doesn't).
3. **List files touched so far** and their role (created/modified, what each contains/does).
4. **Describe what's left**, as concrete next steps, in suggested order.
5. **Note blockers/open questions**: anything that needs a decision or external input before continuing (e.g. "needs design confirmation on X", "waiting on API endpoint Y to exist").
6. **Note assumptions made** that the next person should be aware of/validate.
7. **Note any known issues**: things that don't work yet, edge cases not handled, validation not run.
8. **Point to relevant context**: related plan/decisions, existing patterns followed, anything non-obvious about why something was done a certain way.

## Rules and Best Practices
- Be specific: "Implemented the form UI in `components/SignupForm.tsx`; not yet wired to the signup API" is useful, "mostly done with signup" is not.
- Order next steps logically (e.g. respecting build order from Plan the Feature Skill).
- Separate "must do next" from "nice to have later."
- Include enough context that someone unfamiliar with this specific conversation can pick up without re-deriving decisions already made.
- Keep it concise — a focused list beats a long narrative.

## Safety Checks
- Flag any half-finished change that could leave the app in a broken/inconsistent state if left as-is (e.g. a schema change without the corresponding code update) so the next person knows not to deploy/merge prematurely.
- Don't omit known risks or unresolved issues to make the handoff look cleaner.

## Validation Checks
- Confirm every "in progress" item has a clear next step.
- Confirm all touched files are listed.
- Confirm blockers/assumptions/risks are all captured.
- Confirm the notes would make sense to someone without this conversation's context.

## Common Mistakes to Avoid
- Vague status descriptions ("almost done", "just needs polish").
- Omitting files that were touched.
- Leaving out blockers or open questions, causing the next person to rediscover them.
- Writing notes that assume the reader has the same context as this conversation.
- Hiding that something is left in a broken/incomplete state.

## Output Rule
Do not invent a custom final response format for this skill. Follow the Global Agent Output and Reporting Skill. Only include skill-specific reporting details when necessary for understanding the completed work. Handoff notes themselves are a deliverable of this skill and may be more detailed than a typical final report — structure them clearly under the headings above.
