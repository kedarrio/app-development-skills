---
name: understand-the-project
description: Inspect and understand a codebase before making any changes. Use this skill at the start of nearly every task — before planning, coding, debugging, or refactoring — to detect the framework, folder structure, conventions, dependencies, and existing patterns so new work fits the project instead of fighting it. Always run this skill first when entering an unfamiliar repo, resuming a project, or before any task that touches files you haven't inspected yet.
---

# Understand the Project Skill

## Purpose
Build an accurate, current picture of the project's framework, structure, conventions, and state before making any change. This prevents wrong assumptions, duplicate code, broken conventions, and wasted work.

## When to Use
- At the start of any new task in a repo you haven't inspected recently.
- Before planning a feature, writing code, debugging, or refactoring.
- When the project structure, stack, or conventions are unknown or unclear.
- After a long gap, when the codebase may have changed.

## When Not to Use
- For trivial, isolated tasks where the relevant file and convention are already known and recently confirmed (e.g. fixing a typo in a string you just read).
- When the user explicitly provides full context and the task is scoped to a single already-inspected file.

## Required Inputs
- Access to the project's file tree.
- The task or request that motivates the inspection (helps focus what to look at).

## Assumptions
- The project may use Next.js, Expo Router, Vite, or another framework — do not assume which.
- The project may already deviate from the default architecture rule of thumb (`/app`, `/components`, `/lib`, `/services`, `/db`, `/hooks`, `/store`, `/types`, `/styles`, `/public`). Existing structure wins.
- Package manager (npm/yarn/pnpm/bun) is determined by lockfile, not preference.

## Step-by-Step Workflow
1. **Read root config files**: `package.json`, `tsconfig.json` / `jsconfig.json`, framework config (`next.config.*`, `vite.config.*`, `app.json`/`expo`), `.env.example`, lockfile (determines package manager).
2. **Identify the framework and routing style**: Next.js (App Router vs Pages Router), Expo Router, Vite + React Router, or other. Confirm by checking actual folder layout, not just dependencies.
3. **Map the top-level structure**: list top 2 levels of directories. Note what each top-level folder actually contains vs. the default rule of thumb.
4. **Identify styling approach**: CSS Modules, Tailwind, styled-components, global CSS, etc. — check `package.json` and a sample component.
5. **Identify state management**: look for Redux/Zustand/Jotai/Context/React Query/SWR/etc.
6. **Identify data layer**: how API calls are made (fetch wrappers, service files, server actions, ORMs like Prisma/Drizzle).
7. **Check for existing scripts**: lint, typecheck, test, build commands in `package.json`.
8. **Check for docs**: README, `/docs`, architecture notes, decision records.
9. **Scan for patterns relevant to the current task**: e.g. if the task involves auth, find existing auth code; if it involves a component type, find similar existing components.
10. **Summarize findings internally** (framework, structure, conventions, scripts, relevant existing files) and carry this into the next skill (Clarify, Plan, etc.).

## Rules and Best Practices
- Detect before assuming. Never default to the rule-of-thumb structure if the project already has its own.
- Confirm the package manager from the lockfile (`package-lock.json`, `yarn.lock`, `pnpm-lock.yaml`, `bun.lockb`) and never switch it.
- Note the framework's routing convention precisely (e.g. Next.js App Router uses `app/` with `page.tsx`/`layout.tsx`; Expo Router uses file-based routing under `app/`; Vite + React Router uses a router config file).
- Identify at least one existing example of each relevant pattern (component, service call, state usage) before writing new code that follows it.
- Keep this inspection proportional to the task — a full deep audit is not required for small, well-scoped tasks, but the basics (framework, structure, styling, relevant existing files) should always be checked.

## Safety Checks
- Do not modify any files during this skill — it is read-only.
- Do not assume missing context; if critical project details can't be determined from the repo, flag this for the Clarify the Request Skill.

## Validation Checks
- Confirm: framework identified, routing style identified, package manager identified, styling approach identified, state approach identified, relevant existing files for the task identified.
- If any of these can't be determined, note it explicitly rather than guessing.

## Common Mistakes to Avoid
- Assuming the default `/app /components /lib ...` structure without checking.
- Assuming Next.js when the project is Expo Router or Vite (or vice versa).
- Missing an existing similar component/service and creating a duplicate.
- Inspecting too broadly for a tiny task, wasting time before getting to the actual work.
- Trusting `package.json` dependencies alone without confirming actual usage in code.

## Output Rule
Do not invent a custom final response format for this skill. Follow the Global Agent Output and Reporting Skill. Only include skill-specific reporting details when necessary for understanding the completed work.
