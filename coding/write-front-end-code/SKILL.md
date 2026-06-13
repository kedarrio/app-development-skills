---
name: write-front-end-code
description: Implement UI code cleanly while respecting the project's folder boundaries (app/routes, components, lib, services, hooks, store), styling conventions, and state patterns. Use this skill for any task that involves writing or editing front-end code in Next.js, Expo Router, Vite, or similar frameworks — implementing components, hooks, styles, or wiring UI together. This is the general front-end implementation skill; for page/route assembly specifically, also see Assemble Page or Screen.
---

# Write Front-End Code Skill

## Purpose
Write front-end code that is clean, correctly placed, consistent with project conventions, and free of unnecessary complexity, duplication, or boundary violations.

## When to Use
- Implementing UI logic, components, hooks, or styles for a planned feature.
- Editing existing front-end code to add or change behavior.
- Any task that produces or modifies `.tsx`/`.jsx`/`.ts`/`.js`/style files in the front-end layers.

## When Not to Use
- Pure backend/database work with no front-end code involved (see Database and Backend Logic Skill).
- Page/route composition specifically when the work is primarily about assembling existing components into a screen (see Assemble Page or Screen Skill) — though this skill's rules still apply to any code written there.

## Required Inputs
- The plan or task description (from Plan the Feature Skill if applicable).
- Project conventions from Understand the Project Skill (framework, folder structure, styling, state).
- Existing related components/hooks/services to extend or follow as patterns.

## Assumptions
- Existing project structure and conventions take precedence over the default rule of thumb.
- Code should preserve existing behavior unless the task asks for a behavior change.

## Step-by-Step Workflow
1. **Confirm placement**: determine the correct file/folder for this code based on responsibility:
   - Reusable UI → `/components` (or project equivalent).
   - Helper/utility logic → `/lib`.
   - API/business calls → `/services`.
   - React logic (custom hooks) → `/hooks`.
   - Global state → `/store`.
   - Types → `/types`.
   - Routes/screens → `/app` (or framework's routing convention).
2. **Check for existing code to reuse or extend** before writing new code (components, hooks, utilities, types).
3. **Write the implementation**:
   - Keep functions and components focused on one responsibility.
   - Use clear, descriptive names — avoid `data`, `temp`, `stuff`, `helper`, `newThing` unless context makes them unambiguous.
   - Keep nesting shallow; extract logic into named functions/hooks when it improves clarity.
   - Avoid duplicating logic that already exists elsewhere — extract shared logic only if reuse is real.
4. **Apply styling per project convention** (CSS Modules, Tailwind, etc.); keep component styles co-located with the component, not in route files or scattered globals.
5. **Apply state per convention**: local state first, then shared/global only if truly needed (see Manage State Skill).
6. **Handle states relevant to the UI**: loading, error, empty, success/disabled — at minimum acknowledge them even if handled by a child component.
7. **Type everything** (if TypeScript): define/extend types in `/types` or co-located as per convention; avoid `any`/`as any`.
8. **Clean up before finishing**: remove unused imports/variables, commented-out code, stray `console.log`s, and placeholder TODOs that aren't tied to a real follow-up.

## Rules and Best Practices
- Preserve existing behavior unless the task explicitly requires a change.
- Prefer small, correct changes over large rewrites.
- Reuse existing components/hooks/services/types before creating new ones.
- Keep route/page files focused on composition — don't embed large UI blocks, component CSS, or business logic there (see Assemble Page or Screen Skill).
- Keep API calls out of UI components — use the services/data layer.
- Keep styling consistent with the existing approach; don't introduce a new styling system without approval.
- Don't use hard-coded spacing/colors/typography when tokens exist.
- Don't introduce a new dependency without flagging it (see Dependency and Config Skill).

## Safety Checks
- Changes to shared components/hooks/utilities affect multiple call sites — check usages before changing signatures or default behavior.
- Don't remove error handling, loading states, or accessibility features while editing for another purpose.

## Validation Checks
- Confirm the file is placed according to project convention/responsibility.
- Confirm no unused imports, dead code, or stray logs remain.
- Confirm types are correct and no `any`/type bypasses were introduced without justification.
- Confirm existing behavior elsewhere wasn't broken (check other usages of changed shared code).
- Run relevant lint/typecheck if available (see Validate and Test Skill).

## Common Mistakes to Avoid
- Putting reusable UI, component styles, or business logic inside route/page files.
- Duplicating an existing component, hook, or utility instead of reusing/extending it.
- Using `any`/`as any` to silence type errors.
- Leaving commented-out code, debug logs, or vague TODOs.
- Introducing a new state library or styling system without approval.
- Large, sweeping rewrites when a small targeted change would do.

## Output Rule
Do not invent a custom final response format for this skill. Follow the Global Agent Output and Reporting Skill. Only include skill-specific reporting details when necessary for understanding the completed work.
