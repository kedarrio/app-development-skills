---
name: architecture-planning
description: Decide, review, or document app structure — folder responsibilities, module boundaries, and conventions. Use this skill when setting up a new project area, when a feature doesn't fit cleanly into the existing structure, when asked to review or improve architecture, or before any task specifically described as architecture setup, restructuring, or migration. Do not use it for routine feature work that fits existing structure.
---

# Architecture Planning Skill

## Purpose
Establish or review the structural rules of the project — where code lives, how layers interact, and what conventions apply — so the codebase stays organized and predictable as it grows.

## When to Use
- Starting a new project or a new major area with no established convention yet.
- A new feature doesn't fit any existing folder/module pattern.
- Explicitly asked to review, document, or improve the architecture.
- The task is specifically scoped as architecture setup, restructuring, or migration.

## When Not to Use
- Routine feature work that fits the existing structure — just follow the convention (see Understand the Project Skill).
- Small one-off files that clearly belong in an existing folder by existing rules.

## Required Inputs
- Current project structure (from Understand the Project Skill).
- The framework in use and its routing/structure conventions.
- The specific architectural question or gap driving this task.

## Assumptions
- If the project has an established structure, it takes precedence over the default rule of thumb.
- Architecture changes are higher-risk and broad — they affect many files and future work.

## Step-by-Step Workflow
1. **Confirm the framework's structural conventions** (e.g. Next.js App Router file conventions, Expo Router file-based routing, Vite project layout).
2. **Inventory current structure**: list top-level folders and what currently lives in each; note any inconsistencies.
3. **Identify the gap or question**: e.g. "where should shared form validation logic live?" or "this feature needs a new top-level area — where does it go?"
4. **Apply the default rule of thumb as a baseline** when no stronger convention exists:
   - `/app` = routes and screens
   - `/components` = UI
   - `/lib` = helper logic
   - `/services` = API/business calls
   - `/db` = database
   - `/hooks` = React logic
   - `/store` = global state
   - `/types` = TypeScript types
   - `/styles` = global CSS
   - `/public` = images and static files
5. **Decide placement** based on responsibility, not convenience — ask "where would a future developer look for this?"
6. **Document the decision** briefly: what goes where, and why, especially if it sets a new precedent.
7. **If this is a migration/restructure**, plan it as its own isolated task: list files to move, update imports, and validate after each batch — don't mix with feature work.
8. **Flag broad impact**: if the decision affects many existing files, flag for Risk Review before executing.

## Rules and Best Practices
- Extend existing patterns before introducing new ones.
- Keep folder responsibilities single-purpose and clearly named.
- Don't create a new top-level folder for something that fits an existing one.
- Don't restructure the whole project to accommodate one feature — adapt the feature or make a minimal, justified structural addition.
- Document new conventions where future agents/devs will see them (README or architecture notes) via the Document the Work Skill.
- Keep routing files, UI components, business logic, and data access in clearly separate layers regardless of framework.

## Safety Checks
- Treat any change affecting more than a handful of files as high-impact — confirm before executing.
- Do not change the framework or package manager as part of an architecture decision.
- Do not silently restructure existing folders while doing unrelated feature work.

## Validation Checks
- Confirm the decision is consistent with the framework's own conventions (doesn't fight the framework).
- Confirm the decision doesn't create two parallel patterns for the same kind of thing.
- If a migration was performed, confirm all imports were updated and nothing references old paths.

## Common Mistakes to Avoid
- Forcing Next.js conventions onto an Expo Router project (or vice versa).
- Creating a second "utils" or "helpers" folder when `/lib` already exists.
- Mixing architecture changes into a feature PR/task, making both harder to review.
- Deciding structure based on personal preference rather than responsibility and existing precedent.
- Leaving old files/paths behind after a restructure.

## Output Rule
Do not invent a custom final response format for this skill. Follow the Global Agent Output and Reporting Skill. Only include skill-specific reporting details when necessary for understanding the completed work.
