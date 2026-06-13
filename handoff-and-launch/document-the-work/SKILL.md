---
name: document-the-work
description: Write or update README notes, setup docs, architecture notes, API documentation, code comments, and decision records. Use this skill when a change affects setup steps, architecture, API behavior, environment variables, scripts, or involves a tradeoff worth recording — and when existing docs would otherwise go stale. Do not use it to document things that are already obvious from clear code.
---

# Document the Work Skill

## Purpose
Keep project documentation accurate and useful by updating it when setup, architecture, APIs, environment variables, scripts, or important decisions change — without over-documenting the obvious.

## When to Use
- Setup steps changed (new env vars, new install/run steps).
- Architecture or folder conventions changed or were newly established.
- API behavior (request/response shape, new endpoints) changed.
- A non-obvious tradeoff or decision was made that future developers/agents should know about.

## When Not to Use
- The change is self-explanatory from clear code and existing docs remain accurate.
- Documenting would just restate what the code already makes obvious.

## Required Inputs
- The change made and its user/developer-facing impact.
- Existing documentation: README, `/docs`, architecture notes, decision logs, inline comments.

## Assumptions
- Documentation should reflect the current state of the code — outdated docs are worse than no docs.
- Decision records are for non-obvious tradeoffs, not routine implementation details.

## Step-by-Step Workflow
1. **Identify what changed that affects documentation**:
   - Setup/run instructions (new dependency, new env var, new script).
   - Architecture/conventions (new folder pattern, new shared module's purpose).
   - API contracts (new/changed endpoints, request/response shapes).
   - Decisions with tradeoffs (why X was chosen over Y).
2. **Find the right existing location** for each update — README section, `/docs` file, architecture notes, inline comment near the relevant code. Don't create a new doc file if an existing one is the natural home.
3. **Update concisely**:
   - Setup docs: add/update the specific step (e.g. new env var with description, new script usage).
   - Architecture notes: describe the new pattern/convention and where it applies.
   - API docs: document new/changed endpoints (method, path, request/response shape, auth requirements, errors).
   - Decision records: short entry — what was decided, why, and what alternatives were considered, if the project keeps such a log.
4. **Update inline comments** only where code isn't self-explanatory (non-obvious "why", not "what").
5. **Check for drift**: if this change makes an existing doc statement false, update or remove that statement — don't leave contradictions.

## Rules and Best Practices
- Keep docs concise and accurate; don't pad with obvious explanations.
- Write decision notes for tradeoffs, not for routine choices that follow existing convention.
- Update existing docs in place rather than creating new, overlapping doc files.
- Keep API docs in sync with actual request/response shapes (cross-check with Connect Data and API / Database and Backend Logic work).
- Use clear, specific language — avoid vague statements like "various configuration may be needed."
- Comments should explain *why*, not restate *what* the code visibly does.

## Safety Checks
- Don't document secrets/credentials values — only document that a variable is required and what it's for.
- Don't remove documentation for features that still exist, even if unrelated to this task, unless it's already wrong.

## Validation Checks
- Confirm updated docs accurately reflect the current code/behavior.
- Confirm no contradictions remain between docs and implementation.
- Confirm new env vars/scripts/setup steps are documented if introduced.
- Confirm no real secret values appear in documentation.

## Common Mistakes to Avoid
- Leaving docs stale after changing setup, APIs, or architecture.
- Creating a new doc file that duplicates/overlaps an existing one.
- Writing comments that just restate the code ("// increment i by 1").
- Documenting obvious code while skipping genuinely non-obvious decisions.
- Including secret values in documentation/examples.

## Output Rule
Do not invent a custom final response format for this skill. Follow the Global Agent Output and Reporting Skill. Only include skill-specific reporting details when necessary for understanding the completed work.
