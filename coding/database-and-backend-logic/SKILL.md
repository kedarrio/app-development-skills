---
name: database-and-backend-logic
description: Work with database schemas, migrations, queries, backend routes/server actions, seed data, and data models. Use this skill for any task touching the database or backend logic layer — adding/changing tables or fields, writing queries, creating API routes or server actions, validating backend inputs, or seeding data. Treat schema changes and data-affecting operations as higher-risk by default.
---

# Database and Backend Logic Skill

## Purpose
Implement and modify database schemas, queries, and backend logic safely and consistently — keeping data access in the correct layer, validating inputs, and avoiding destructive or schema-breaking changes without approval.

## When to Use
- Adding/modifying database tables, fields, relationships, or migrations.
- Writing or changing queries, ORM models, server actions, or API route handlers.
- Seeding or modifying data for development/testing.
- Validating backend input/output for an endpoint.

## When Not to Use
- Pure front-end tasks with no backend/database involvement.
- Tasks that only consume an existing, unchanged API (see Connect Data and API Skill).

## Required Inputs
- The existing schema/data model (tables/fields/relationships, ORM models, migration history).
- The existing backend framework/pattern (API routes, server actions, ORM such as Prisma/Drizzle, raw SQL, etc.) from Understand the Project Skill.
- The specific data/behavior requirement driving this task.

## Assumptions
- An existing schema/data model is in place unless explicitly told this is a from-scratch setup.
- Schema changes and destructive data operations require explicit approval before execution.

## Step-by-Step Workflow
1. **Review the existing schema/data model**: tables/collections, fields, types, relationships, indexes, and existing migrations.
2. **Check for existing tables/fields/relations that already satisfy the need** before adding new ones — don't invent parallel structures for the same concept.
3. **For schema changes**:
   - Define the change (new table/field/relation, type change, constraint change).
   - Identify migration impact: does this require a migration? Does it affect existing data (nullable vs. required, defaults, renames)?
   - Flag any change that could cause data loss (dropping/renaming columns, changing types incompatibly, removing tables) for explicit approval before applying.
4. **For queries/ORM logic**:
   - Follow the existing query/ORM pattern and naming conventions.
   - Keep queries efficient (avoid N+1 patterns where the existing codebase already avoids them; use existing includes/joins patterns).
   - Keep database logic in the backend/data layer (`/db`, server actions, API routes) — not in front-end components.
5. **For API routes/server actions**:
   - Validate inputs on the backend (types, required fields, ranges) regardless of front-end validation.
   - Return clear, consistent error responses matching the project's existing error shape/conventions.
   - Don't expose internal error details (stack traces, raw DB errors) to clients in production-style responses; log details server-side per project convention.
6. **For seed data**: use existing seed scripts/conventions if present; don't overwrite existing seed data wholesale without confirming it's safe to do so.
7. **Check secrets/config**: database connection strings and credentials come from environment variables per existing convention — never hard-coded.

## Rules and Best Practices
- Keep database/backend logic in the appropriate layer (`/db`, server actions, API route handlers) — never inside visual components.
- Don't invent tables, fields, or relationships that conflict with or duplicate the existing schema.
- Validate all backend inputs, even if the front-end also validates.
- Keep backend error responses clear, consistent, and free of leaked internals.
- Don't expose secrets (DB credentials, API keys) to front-end code.
- Prefer additive, backward-compatible schema changes (new nullable field with default) over breaking changes when possible.
- Keep query/ORM patterns consistent with existing usage (don't mix raw SQL into a project that consistently uses an ORM, or vice versa, without reason).

## Safety Checks
- Never run or write a migration/operation that drops tables/columns or deletes data without explicit approval.
- Never write a destructive migration without first confirming current data won't be lost or making the change backward-compatible.
- Flag any schema change that affects existing API consumers (front-end or other services) before applying.
- Don't modify production seed/config behavior without approval.

## Validation Checks
- Confirm new/changed schema doesn't conflict with existing fields/relations.
- Confirm migrations run cleanly against representative existing data (or are reviewed for impact if they can't be run).
- Confirm backend input validation rejects invalid input with a clear error.
- Confirm error responses don't leak internal details.
- Confirm no secrets are hard-coded.

## Common Mistakes to Avoid
- Adding a new table/field that duplicates an existing concept under a different name.
- Writing destructive migrations (drop column/table) without approval.
- Skipping backend validation because the front-end already validates.
- Returning raw database errors or stack traces to clients.
- Putting database queries directly inside UI components.
- Hard-coding database credentials or connection strings.

## Output Rule
Do not invent a custom final response format for this skill. Follow the Global Agent Output and Reporting Skill. Only include skill-specific reporting details when necessary for understanding the completed work.
