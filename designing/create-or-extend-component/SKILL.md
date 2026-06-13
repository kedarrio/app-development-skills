---
name: create-or-extend-component
description: Build a new reusable UI component or extend an existing one with clean props, variants, accessibility, and styling. Use this skill whenever a task calls for a button, input, card, modal, form element, table, tabs, badge, layout shell, or any other piece of UI that is or could be reused across the app. Always search for an existing equivalent component first — this skill covers both creating new components and extending existing ones.
---

# Create or Extend Component Skill

## Purpose
Produce reusable, accessible, responsive UI components that fit the existing design system and avoid duplication — by extending existing components wherever possible.

## When to Use
- A new piece of UI is needed that is reusable or belongs to the design system (buttons, inputs, cards, modals, tabs, badges, layout shells, etc.).
- An existing component needs a new variant, size, state, or prop to support a new use case.

## When Not to Use
- The UI is truly one-off and page-specific with no reuse potential — consider building it inline within the page/screen (still following styling rules), not as a new shared component.
- A suitable component already exists and meets the need as-is — just use it.

## Required Inputs
- The UI requirement (what it needs to do, look like, and support).
- Existing components/primitives from `/components` (or project equivalent) and the Design System Skill's tokens.
- Any design reference (if provided).

## Assumptions
- Reuse is checked first; creation/extension is the fallback.
- Components receive data via props or established state/data patterns — they don't own API calls or business logic.

## Step-by-Step Workflow
1. **Search for an existing component** that matches or is close to the need (by name, by visual similarity, by folder convention).
2. **If a close match exists**: determine whether a new prop/variant on the existing component covers the need. Prefer this over a new component.
3. **If no match exists**: define the new component's:
   - Name (clear, specific, not vague).
   - Props: data props, variant/size props, event handlers, state props (loading, disabled, error, selected, etc.).
   - Visual states: default, hover, focus, active, disabled, loading, error, empty (as applicable).
4. **Build using existing tokens/primitives** — no hard-coded colors, spacing, radii, shadows, or typography values.
5. **Apply accessibility defaults**: semantic HTML elements, keyboard support, ARIA only where semantics aren't enough, accessible labels, visible focus states.
6. **Apply responsiveness** if the component owns layout (see Responsive UI Skill).
7. **Place the file correctly**: shared components in `/components` (or project equivalent); component-level styles co-located with the component (e.g. CSS Modules file alongside it) unless the project convention differs.
8. **Keep the component free of**: API calls, route/navigation logic, and page-specific business logic — pass these in via props/handlers instead.
9. **If extending**, verify existing usages still work with the new prop/variant added as optional/additive.

## Rules and Best Practices
- Build reusable components only when the UI appears in more than one place or clearly belongs to the design system — don't over-abstract one-off UI.
- Keep one component per UI concept; extend rather than duplicate.
- Components should handle their own loading/disabled/error/empty visual states when relevant, driven by props.
- Components should be accessible and responsive by default when that responsibility belongs to them.
- Keep component styles close to the component (e.g. `Component.module.css` next to `Component.tsx`), not inside route/page files or scattered globals.
- Use the project's existing styling method; if starting fresh, prefer CSS Modules with raw CSS and design tokens.
- Avoid vague names (`Box`, `Wrapper`, `Item`) unless genuinely generic and well-scoped; prefer names that describe role (`UserCard`, `ConfirmDialog`).

## Safety Checks
- Before changing an existing shared component's default prop values or markup structure, check where else it's used — avoid breaking other call sites.
- Don't delete or rename an existing component's exported API without checking usages and updating them.

## Validation Checks
- Confirm the component renders correctly for all defined states (default, loading, error, empty, disabled) where applicable.
- Confirm keyboard navigation and focus states work for interactive elements.
- Confirm no hard-coded design values were introduced where tokens exist.
- Confirm existing usages of an extended component still work unchanged unless the change was intentional and approved.

## Common Mistakes to Avoid
- Creating a near-duplicate of an existing component instead of extending it.
- Putting API calls or business logic inside a UI component.
- Hard-coding colors/spacing instead of using design tokens.
- Skipping accessibility (e.g. using a `div` with an onClick instead of a `button`).
- Placing a reusable component inside `/app` or a route/page file.
- Breaking other usages when changing a shared component's defaults.

## Output Rule
Do not invent a custom final response format for this skill. Follow the Global Agent Output and Reporting Skill. Only include skill-specific reporting details when necessary for understanding the completed work.
