---
name: risk-review
description: Detect destructive actions, data loss potential, privacy issues, security risks, config risk, irreversible changes, and other high-impact decisions before acting. Use this skill before executing any change involving deletion, schema/migration changes, auth/permissions, environment/deployment config, broad multi-file changes, or anything described as risky/sensitive — and as a final check before destructive or irreversible operations.
---

# Risk Review Skill

## Purpose
Catch high-impact, destructive, or irreversible changes before they happen — ensuring they're flagged, explained, and explicitly approved rather than executed silently.

## When to Use
- Before deleting files, data, or database records/tables.
- Before schema/migration changes.
- Before changes to auth, permissions, roles, or access control.
- Before changes to environment variables, deployment config, or build/release config.
- Before broad changes affecting many files (architecture/restructure).
- Whenever a task "feels" risky even if it doesn't fit a category above.

## When Not to Use
- Routine, additive, easily-reversible changes (new component, new non-destructive function, new optional field with default).

## Required Inputs
- The proposed change/action.
- Its scope: how many files/areas/users/data it affects.
- Whether it's reversible and how (e.g. can be undone with a revert vs. permanent data loss).

## Assumptions
- "Reversible" means a normal revert/rollback restores the prior state without data loss — not just "technically possible with effort."
- When in doubt about risk level, treat it as higher risk.

## Step-by-Step Workflow
1. **Identify the action's category**:
   - Data deletion or overwrite (files, DB records, user data).
   - Schema/migration change.
   - Auth/permissions/roles change.
   - Environment/deployment/config change.
   - Broad multi-file/architecture change.
   - Other irreversible or hard-to-reverse action.
2. **Assess reversibility**: can this be undone easily (revert commit, restore from a non-destructive change) or would undoing it require restoring lost data/state?
3. **Assess blast radius**: how many users/files/areas of the app does this affect if something goes wrong?
4. **If high-impact and/or low-reversibility**:
   - Do not proceed automatically.
   - Clearly explain what the action does, why it's needed, what could go wrong, and what approval is being requested for.
   - Wait for explicit approval before proceeding.
5. **If low-impact and reversible**: proceed, but still note the action briefly if it's the kind of thing someone would want to know about (e.g. "added a new optional field with a default value").
6. **For approved high-risk actions**: keep the change as small and isolated as possible; avoid bundling it with unrelated changes.
7. **After the action**: confirm it had the intended effect and nothing beyond scope was affected.

## Rules and Best Practices
- Ask before destructive or irreversible actions — always.
- Ask before deleting files/data when ownership or usage is unclear.
- Ask before changes to auth, permissions, schema, deployment config, or environment setup.
- Ask before architecture changes affecting many files.
- State assumptions explicitly when they affect a risky action.
- Prefer reversible alternatives where they meet the requirement (e.g. soft-delete/deactivate instead of hard delete, if that satisfies the goal and the project supports it — but don't invent a new soft-delete mechanism without approval either).
- Keep risky changes small and isolated from unrelated work.

## Safety Checks
- Never perform irreversible data deletion without explicit, informed approval for that specific action.
- Never silently weaken security/permissions as a side effect of another change.
- Never change production-pointing config (URLs, keys) as a side effect of a dev-focused task.

## Validation Checks
- Confirm every high-risk action identified was either explicitly approved or not performed.
- Confirm approved risky actions were scoped exactly as described (no extra unapproved changes bundled in).
- Confirm the post-action state matches what was approved.

## Common Mistakes to Avoid
- Performing a destructive action because it "seemed implied" by the request.
- Bundling a risky change with unrelated routine changes.
- Underestimating blast radius of a shared-code or config change.
- Treating "the user said do X" as approval for destructive side effects of X that weren't discussed.
- Failing to flag a risk because the individual step seemed small, when the cumulative effect is large.

## Output Rule
Do not invent a custom final response format for this skill. Follow the Global Agent Output and Reporting Skill. Only include skill-specific reporting details when necessary for understanding the completed work. Risks identified (whether acted on or not) should be reported under "Risks or unresolved issues" per that skill.
