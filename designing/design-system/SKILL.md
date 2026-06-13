---
name: design-system
description: Create or extend design tokens, primitives, shared components, patterns, and layout building blocks. Use this skill when establishing a design system from scratch, adding new tokens (colors, spacing, typography, radii, shadows), creating cross-cutting primitives (Button, Input, Card, Modal, etc.), or when a feature reveals a gap in the shared design system. Do not use it for one-off, page-specific UI — use Create or Extend Component instead.
---

# Design System Skill

## Purpose
Build and maintain the shared visual foundation (tokens and primitives) so UI across the app stays consistent, reusable, and easy to update.

## When to Use
- No design tokens/primitives exist yet and the project needs a foundation.
- A new pattern (e.g. a new button variant, a new spacing value) is needed in more than one place.
- An existing primitive is missing a state, variant, or accessibility feature needed by multiple features.

## When Not to Use
- The UI is page-specific and unlikely to be reused — use Create or Extend Component Skill instead.
- A suitable token or primitive already exists — reuse it rather than creating a new one.

## Required Inputs
- Existing design tokens/styles (if any): colors, spacing scale, typography, radii, shadows, breakpoints.
- Existing primitive components and their props/variants.
- The specific gap or new need driving this task.

## Assumptions
- Existing tokens and primitives take precedence over new ones — extend, don't duplicate.
- If starting fresh, prefer raw CSS with CSS custom properties (variables) for tokens, organized in global styles, with CSS Modules for component-level styles where appropriate — unless the project already uses another approach.

## Step-by-Step Workflow
1. **Inventory existing tokens**: look in global styles (`/styles`, `globals.css`, theme files) for color, spacing, typography, radius, shadow, and breakpoint values already defined.
2. **Inventory existing primitives**: look in `/components` (or project equivalent) for Button, Input, Card, Modal, Badge, Tabs, etc., and note their props/variants/states.
3. **Identify the gap**: a missing token value, a missing variant, a missing state (loading/disabled/error), or a missing primitive entirely.
4. **For new tokens**: add to the existing token location using the existing naming convention (e.g. `--color-primary-500`, `--spacing-md`). Don't introduce a second token system.
5. **For new/extended primitives**:
   - Define clear props: variants, sizes, states (default, hover, focus, disabled, loading, error).
   - Build on tokens — no hard-coded colors/spacing/typography inside primitives.
   - Ensure accessibility defaults (semantic elements, focus states, ARIA where needed).
   - Ensure responsiveness where layout responsibility belongs to the primitive.
6. **Place files correctly**: shared primitives in `/components` (or project's equivalent shared UI location); tokens in global styles.
7. **Document new tokens/primitives briefly** if they introduce a new convention (via Document the Work Skill).

## Rules and Best Practices
- Search for an existing token or primitive before creating a new one.
- One primitive per UI concept — don't create `ButtonV2` alongside `Button`; extend the original.
- Keep tokens semantic (`--color-danger`, `--spacing-section`) rather than purely literal (`--red`, `--16px`) where possible.
- Keep primitives free of page-specific business logic and API calls.
- Expose variants/sizes/states via props, not via copy-pasted variants of the component.
- Keep styling consistent with the project's existing approach (CSS Modules, Tailwind, etc.) — don't introduce a new styling system without approval.
- Preserve accessibility and responsive behavior when extending existing primitives.

## Safety Checks
- Changing a shared primitive affects every place it's used — check usages before changing its default behavior, and prefer additive changes (new optional prop/variant) over changing existing defaults.
- Don't remove existing variants/props without checking for usages first.

## Validation Checks
- Confirm new tokens follow the existing naming convention and scale.
- Confirm new/extended primitives support the states they claim to (loading, error, disabled, focus) where relevant.
- Confirm no hard-coded values were introduced where a token should be used.
- Confirm existing usages of a changed primitive still render/behave correctly.

## Common Mistakes to Avoid
- Creating a new Button/Card/Modal when one already exists with a different name.
- Hard-coding colors, spacing, or font sizes instead of using/adding tokens.
- Adding business logic or API calls into a shared primitive.
- Changing a shared primitive's default appearance/behavior in a way that breaks other usages.
- Introducing a second styling system (e.g. adding Tailwind to a CSS Modules project) without approval.

## Output Rule
Do not invent a custom final response format for this skill. Follow the Global Agent Output and Reporting Skill. Only include skill-specific reporting details when necessary for understanding the completed work.
