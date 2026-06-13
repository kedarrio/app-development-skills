---
name: accessibility
description: Review and improve accessibility of UI for web and mobile. Use this skill when building or reviewing any interactive UI (forms, buttons, modals, navigation, custom widgets), when a task mentions accessibility/a11y/screen readers/keyboard navigation, or as a check before finalizing any UI work. Applies to both web (Next.js/Vite) and native (Expo) contexts.
---

# Accessibility Skill

## Purpose
Ensure UI is usable via keyboard, screen readers, and assistive technology, and meets baseline accessibility expectations, without breaking visual design.

## When to Use
- Building new interactive UI (forms, buttons, modals, menus, custom widgets).
- Reviewing existing UI for accessibility gaps.
- As part of finishing any UI task, before marking it complete.

## When Not to Use
- Purely non-visual, non-interactive backend/logic tasks.
- Static, non-interactive decorative elements with no semantic meaning (though these still need correct handling, e.g. `alt=""` or `aria-hidden`).

## Required Inputs
- The component/page/screen being built or reviewed.
- Platform context: web (HTML/ARIA) vs. native (Expo/React Native accessibility props).

## Assumptions
- Semantic HTML/native elements are the first choice; ARIA/custom props are a supplement, not a replacement.
- Visual design and accessibility are not in conflict — accessible patterns can be styled to match design.

## Step-by-Step Workflow
1. **Use semantic elements first**: `<button>` for actions, `<a>` for navigation, `<label>` for form fields, headings (`<h1>`–`<h6>`) for structure, lists for grouped items.
2. **Check interactive elements**:
   - Are all clickable elements actually interactive elements (`button`, `a`, native `Pressable`/`TouchableOpacity` with accessibility props), not `div`/`span` with `onClick` only?
   - Can every interactive element be reached and activated via keyboard (web) — Tab to focus, Enter/Space to activate?
3. **Check focus states**: every focusable element has a visible focus indicator; focus order follows a logical reading order.
4. **Check forms**:
   - Every input has an associated label (`<label for>` or `aria-label`).
   - Error messages are associated with their input (e.g. `aria-describedby`) and announced.
   - Required fields are indicated both visually and programmatically.
5. **Check images/icons**: meaningful images have descriptive `alt` text; decorative images/icons use `alt=""` or `aria-hidden="true"`.
6. **Check dynamic content**: loading states, error messages, and important updates are announced to assistive tech (e.g. `aria-live` where appropriate) without being overused.
7. **Check color/contrast**: text and interactive elements meet reasonable contrast against their background (don't rely on color alone to convey state/errors — pair with text/icon).
8. **For Expo/React Native**: use `accessible`, `accessibilityLabel`, `accessibilityRole`, `accessibilityState` props; ensure touch targets meet minimum size (~44x44pt).
9. **Re-check after styling changes**: confirm focus, hover, disabled, and error states are still visually distinguishable.

## Rules and Best Practices
- Use ARIA only when native semantics genuinely aren't enough — don't add redundant ARIA to elements that already convey the right semantics.
- Never use a non-interactive element as a button/link when a real `button`/`a`/native pressable is available.
- Keep error messages programmatically linked to their inputs, not just visually nearby.
- Preserve existing focus/hover/disabled/error/loading visual states when changing styles — don't remove them to "simplify."
- Ensure custom components (dropdowns, modals, tabs) follow expected keyboard interaction patterns (e.g. Escape closes a modal, arrow keys navigate tabs) where the project already establishes such patterns, or follow common conventions if establishing new ones.
- For native apps, respect platform accessibility conventions and minimum touch target sizes.

## Safety Checks
- Don't remove `alt` text, labels, or ARIA attributes as part of unrelated styling/refactor changes.
- Don't replace semantic elements with non-semantic ones for styling convenience.

## Validation Checks
- Confirm all interactive elements are keyboard-operable (web) and have accessible roles/labels.
- Confirm all form inputs have associated labels and linked error messages.
- Confirm focus states remain visible after any styling changes.
- Confirm meaningful images have `alt` text and decorative ones are hidden from assistive tech.
- Confirm touch targets meet minimum size on native.

## Common Mistakes to Avoid
- Using `div`/`span` with `onClick` instead of `button`.
- Missing or unassociated labels on form inputs.
- Removing focus outlines without providing an alternative visible focus style.
- Conveying errors/state with color only.
- Overusing `aria-live` regions, causing excessive announcements.
- Ignoring accessibility on native apps because "it's just mobile."

## Output Rule
Do not invent a custom final response format for this skill. Follow the Global Agent Output and Reporting Skill. Only include skill-specific reporting details when necessary for understanding the completed work.
