---
name: responsive-ui
description: Make layouts and components work correctly across screen sizes, devices, and web/app contexts. Use this skill when building or reviewing UI that must adapt to different viewport sizes, when implementing layouts in Next.js/Vite (web breakpoints) or Expo Router (device sizes and safe areas), or when a responsive bug is reported (layout breaks on mobile/tablet/desktop). Do not use it for backend-only or non-visual tasks.
---

# Responsive UI Skill

## Purpose
Ensure layouts and components adapt correctly across screen sizes and platforms without breaking other breakpoints or hiding important content.

## When to Use
- Building new UI that needs to work across multiple screen sizes.
- Fixing a layout that breaks at certain widths or on certain devices.
- Reviewing a component/page for responsive correctness before handoff.

## When Not to Use
- Non-visual tasks (backend logic, data layer, config).
- A component explicitly defined as fixed-size by design (e.g. an icon) where responsiveness isn't applicable.

## Required Inputs
- The component/page/screen in question.
- Existing breakpoints/responsive patterns used in the project (check global styles/tokens).
- Target platforms (web only, mobile app only, or both).

## Assumptions
- Mobile-first approach is used where no stronger convention exists.
- Existing breakpoints should be reused, not redefined per-component.

## Step-by-Step Workflow
1. **Identify existing breakpoints**: check global styles/tokens for defined breakpoints (e.g. `--breakpoint-sm`, `sm:`/`md:`/`lg:` if Tailwind, or platform-specific dimension logic in Expo).
2. **Identify the platform context**: web (Next.js/Vite — viewport-based breakpoints) vs. native app (Expo — device dimensions, safe areas, orientation).
3. **Design/implement mobile-first**: start from the smallest relevant size, then add rules for larger sizes using existing breakpoints.
4. **Use flexible layout patterns**: flexbox/grid with relative units (`%`, `fr`, `rem`, `flex`) instead of fixed pixel widths/heights, unless a fixed size is intentional (e.g. icon size).
5. **Check content at each breakpoint**:
   - Does anything overflow, get cut off, or overlap?
   - Is important content hidden on small screens? If so, is that intentional and acceptable?
   - Do touch targets remain large enough on small/touch devices?
6. **For Expo/native**: account for safe areas (notches, status bars, home indicators) and test both portrait/landscape if relevant.
7. **Verify desktop/larger sizes still work** after making mobile-focused changes — don't fix mobile by breaking desktop.
8. **Preserve accessibility and interactive states** (focus, hover, active) across breakpoints.

## Rules and Best Practices
- Reuse existing breakpoints; don't invent new ad-hoc breakpoint values.
- Avoid fixed widths/heights unless required (e.g. fixed-size icons, avatars).
- Don't hide major content on smaller screens unless explicitly requested — prefer reflow/stacking over hiding.
- Keep responsive logic in styles (CSS media queries / responsive utility classes) rather than duplicating components per screen size, unless the platform requires structural differences (e.g. Expo layout differences).
- For Expo/React Native, use `SafeAreaView`/safe area hooks and platform-appropriate units; avoid assuming a single fixed device size.
- Test the smallest and largest realistic sizes, plus at least one in between.

## Safety Checks
- Changes to shared layout components affect every screen using them — verify other usages aren't broken across breakpoints.
- Don't remove existing responsive behavior (e.g. a working mobile menu) while fixing a desktop issue.

## Validation Checks
- Confirm no horizontal overflow/clipping at common widths (e.g. ~320px, ~768px, ~1024px, ~1440px for web).
- Confirm interactive elements remain reachable and appropriately sized on touch devices.
- Confirm safe areas are respected on native (no content under notches/status bars/home indicators).
- Confirm focus/hover/active states still work after responsive changes.

## Common Mistakes to Avoid
- Fixing a mobile layout issue by adding styles that break desktop (or vice versa).
- Using fixed pixel widths/heights that cause overflow on smaller screens.
- Hiding content on mobile as a shortcut instead of restructuring the layout.
- Forgetting safe areas on native apps, causing content to sit under system UI.
- Introducing a new breakpoint value instead of using an existing one.

## Output Rule
Do not invent a custom final response format for this skill. Follow the Global Agent Output and Reporting Skill. Only include skill-specific reporting details when necessary for understanding the completed work.
