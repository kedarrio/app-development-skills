---
name: refactor-and-clean-up
description: Clean up redundant code, unused files, duplicate components, misplaced logic, messy styles, and inconsistent structure without changing behavior. Use this skill when explicitly asked to refactor/clean up, when a task reveals dead code or duplication that's clearly unused, or when finishing a feature leaves behind now-unused files from an earlier approach. Do not use it to perform unrelated rewrites or to combine multiple unrelated cleanups into one task.
---

# Refactor and Clean Up Skill

## Purpose
Improve code organization and remove redundancy/dead code while preserving existing behavior — keeping the codebase consistent and easy to navigate.

## When to Use
- Explicitly asked to refactor or clean up a specific area.
- A completed feature left behind unused files/code from an earlier approach (see Rethink or Reframe Skill).
- Clearly unused imports, exports, components, or files are discovered during other work.

## When Not to Use
- As an excuse to rewrite large parts of the app beyond the cleanup's scope.
- Combining multiple unrelated cleanups into one task — keep each refactor focused.
- When it's unclear whether something is actually unused — confirm first (see workflow).

## Required Inputs
- The specific area/files to clean up, or the context that revealed the redundancy.
- Ability to search for usages across the codebase (to confirm something is truly unused/duplicated).

## Assumptions
- Behavior must be preserved unless the task explicitly asks for a behavior change.
- "Unused" must be confirmed via search, not assumed from a file's name or location.

## Step-by-Step Workflow
1. **Scope the cleanup**: define exactly what's being cleaned up (e.g. "remove unused components in `/components/legacy`", "consolidate duplicate `formatDate` utilities").
2. **For unused code/files**:
   - Search the codebase for references/imports/usages.
   - If genuinely unused, remove it. If ownership/usage is unclear (e.g. dynamically imported, used via string reference), don't delete — ask first.
3. **For duplicate logic/components**:
   - Identify which version is canonical (more complete, more recently maintained, more widely used).
   - Migrate usages of the duplicate(s) to the canonical version.
   - Remove the duplicate(s) after migration, and update all imports.
4. **For misplaced logic** (e.g. business logic inside a component, API calls in a UI file):
   - Move it to the correct layer per the default architecture rule of thumb or existing project structure.
   - Update imports/references.
5. **For messy/inconsistent styles**:
   - Consolidate repeated magic values into existing tokens if available.
   - Align inconsistent class/file naming with the project's existing convention.
6. **After moving/removing files**: update all imports and exports; remove now-empty files/folders.
7. **Validate**: run lint/typecheck/test/build (see Validate and Test Skill) and do a quick manual check (see Manual QA and Regression Skill) on affected areas to confirm behavior is unchanged.

## Rules and Best Practices
- Preserve behavior — refactors should not change what the app does, only how the code is organized.
- Move files based on responsibility, not convenience.
- Update all imports/exports after moving or removing files; leave no broken references.
- Remove dead code only when confirmed unused via search.
- Don't leave both the old and new versions of a file/component behind "just in case" — if replaced, remove the old one (after confirming via search and validation).
- Keep the cleanup focused on its stated scope; note other cleanup opportunities separately rather than doing them all at once.
- Ask before deleting files when ownership or usage is genuinely unclear.

## Safety Checks
- Don't delete files without confirming via search that they're unused.
- Don't combine a refactor with a behavior change in the same step — if a behavior change is also needed, treat it as a separate, explicit part of the task.
- Treat removal of shared/widely-used code as higher-impact — confirm all usages are migrated first.

## Validation Checks
- Confirm no broken imports/references remain after moves/removals.
- Confirm lint/typecheck/build still pass.
- Confirm affected areas behave the same as before the refactor (manual spot-check).
- Confirm no duplicate "old + new" versions of the same file/component remain.

## Common Mistakes to Avoid
- Deleting a file that's actually still used (e.g. via dynamic import) without checking.
- Leaving old and new versions of the same component/file both in place.
- Mixing a refactor with unrelated feature changes.
- Forgetting to update imports after moving a file.
- Using "cleanup" as justification for a broad, unscoped rewrite.

## Output Rule
Do not invent a custom final response format for this skill. Follow the Global Agent Output and Reporting Skill. Only include skill-specific reporting details when necessary for understanding the completed work.
