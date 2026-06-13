---
name: assemble-page-or-screen
description: Build route, page, or screen files that compose existing components into a working screen, without turning them into large UI or business-logic files. Use this skill when creating or editing files inside the app/routing layer (e.g. Next.js app/ pages, Expo Router screens, Vite route components) — wiring up layout, data fetching entry points, and framework-level loading/error boundaries. Do not use it for building the reusable components themselves.
---

# Assemble Page or Screen Skill

## Purpose
Compose route/page/screen files that wire together existing components, layout, and data cleanly — keeping routing files thin and focused on composition, not implementation.

## When to Use
- Creating a new route/page/screen.
- Editing an existing route/page/screen to add/rearrange sections, hook up new components, or adjust page-level layout.
- Adding framework-level loading/error boundaries (e.g. Next.js `loading.tsx`/`error.tsx`, Expo Router layouts).

## When Not to Use
- Building the actual reusable UI components used on the page (see Create or Extend Component Skill).
- Writing business logic, API clients, or database queries (see Connect Data and API / Database and Backend Logic Skills) — these are called from the page, not implemented in it.

## Required Inputs
- The plan/feature describing what the screen needs to show and do.
- The components, services, and types already available (or being built alongside).
- The framework's routing conventions (confirmed via Understand the Project Skill).

## Assumptions
- Route/page/screen files are composition layers: they assemble components, pass data/props, and handle page-level layout and framework-provided states.
- Reusable UI, component styles, and business logic live elsewhere and are imported in.

## Step-by-Step Workflow
1. **Confirm the route/file location and naming** per the framework's convention (e.g. Next.js App Router `app/.../page.tsx`, Expo Router file-based route, Vite route component).
2. **Identify the components needed** for this screen — reuse existing ones; flag any missing components for Create or Extend Component Skill.
3. **Determine data needs**: what data does this screen need, and how is it fetched per the project's convention (server component fetch, loader, hook, service call)? Wire to the data layer — don't fetch inline with ad-hoc logic if a service/hook pattern exists.
4. **Compose the page**:
   - Set up page-level layout (structure/sections) using layout primitives or simple layout markup.
   - Import and arrange components, passing data via props.
   - Add framework-level loading/error/empty handling (e.g. `loading.tsx`, `error.tsx`, suspense boundaries, or equivalent) where the framework supports it.
5. **Keep the file thin**: if a section of JSX is becoming a large, self-contained block of UI with its own logic, extract it into a component instead of growing the page file.
6. **Wire navigation**: links/buttons that navigate use the framework's navigation primitives (e.g. `next/link`, Expo Router `Link`/`router`), not ad-hoc anchor tags or window navigation unless required.
7. **Verify metadata/config** if relevant (page titles, SEO metadata for web, screen options for Expo Router) per existing conventions.

## Rules and Best Practices
- Route files should compose imported components — not contain reusable components, component CSS, database logic, or scattered business logic.
- Keep page-level layout simple; push complex/reusable layout patterns into shared layout components if reused elsewhere.
- Use the framework's built-in loading/error/empty mechanisms where available instead of inventing custom ones.
- Pass data down via props/typed interfaces; don't pass loosely-typed blobs.
- Keep navigation consistent with the framework's navigation primitives.
- If the same page structure is needed in multiple places, extract a shared layout/template component rather than duplicating the page file.

## Safety Checks
- Don't restructure routing (renaming/moving route files) as a side effect of a feature task — that's an architecture change (see Architecture Planning Skill).
- Check that new routes don't unintentionally bypass auth/permission checks used by sibling routes (see Auth and Access Skill).

## Validation Checks
- Confirm the route renders with real or representative data, including loading/error/empty states.
- Confirm the page file doesn't contain large inline UI blocks, component-level CSS, or direct database/API client code.
- Confirm navigation links/actions use the framework's navigation primitives and point to valid routes.
- Confirm the route follows the framework's file/naming convention.

## Common Mistakes to Avoid
- Turning a page/route file into a large component with embedded styles and logic.
- Fetching data with ad-hoc inline logic when a service/hook convention already exists.
- Duplicating a page structure instead of extracting a shared layout.
- Using plain `<a>`/manual navigation instead of the framework's navigation primitives.
- Skipping loading/error/empty states at the page level when the framework supports them easily.

## Output Rule
Do not invent a custom final response format for this skill. Follow the Global Agent Output and Reporting Skill. Only include skill-specific reporting details when necessary for understanding the completed work.
