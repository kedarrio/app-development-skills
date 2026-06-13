# App Development Skills

A bundle of 29 reusable agentic skills for AI coding agents (Claude, Claude Code, and compatible tools) working on app development projects — covering the full lifecycle from planning through launch, plus cross-cutting skills like debugging, refactoring, risk review, and output reporting.

These skills are **framework-agnostic** but designed with Next.js, Expo Router, and Vite-based projects in mind. Agents are expected to detect the existing project's framework, structure, and conventions and follow them — the skills include a default architecture rule of thumb (`/app`, `/components`, `/lib`, `/services`, `/db`, `/hooks`, `/store`, `/types`, `/styles`, `/public`) used only when no stronger project convention exists.

## How these skills fit together

The general flow is **Planning → Designing → Coding → Testing → Handoff/Launch**, but it isn't strictly linear — debugging, refactoring, documentation, and risk review can happen at any stage (`cross-process/`).

Every skill (except `global-agent-output-and-reporting`) ends with a short output rule pointing back to the **Global Agent Output and Reporting Skill**, which standardizes how the agent reports completed work (files touched, validation results, assumptions, risks, next steps). This keeps reporting consistent no matter which skill(s) were used.

## Skill index

### Planning (`planning/`)
| Skill | Purpose |
|---|---|
| [understand-the-project](planning/understand-the-project/SKILL.md) | Inspect and understand a repo before making changes |
| [clarify-the-request](planning/clarify-the-request/SKILL.md) | Ask only necessary questions before starting unclear work |
| [plan-the-feature](planning/plan-the-feature/SKILL.md) | Turn a feature idea into requirements, files, data needs, edge cases, and build order |
| [architecture-planning](planning/architecture-planning/SKILL.md) | Decide or review app structure, folder responsibility, and conventions |
| [rethink-or-reframe](planning/rethink-or-reframe/SKILL.md) | Re-evaluate direction when the current approach is wrong, too complex, or unnecessary |

### Designing (`designing/`)
| Skill | Purpose |
|---|---|
| [design-system](designing/design-system/SKILL.md) | Create or extend tokens, primitives, components, patterns, and layouts |
| [ux-flow-and-information-architecture](designing/ux-flow-and-information-architecture/SKILL.md) | Plan screens, navigation, user flows, and content structure |
| [create-or-extend-component](designing/create-or-extend-component/SKILL.md) | Build reusable UI components with clean props, variants, accessibility, and styling |
| [write-product-text](designing/write-product-text/SKILL.md) | Write app microcopy — buttons, empty states, errors, onboarding, helper text |
| [responsive-ui](designing/responsive-ui/SKILL.md) | Make layouts work across screen sizes, devices, and web/app contexts |
| [accessibility](designing/accessibility/SKILL.md) | Review and improve accessibility for web and mobile UI |

### Coding (`coding/`)
| Skill | Purpose |
|---|---|
| [write-front-end-code](coding/write-front-end-code/SKILL.md) | Implement UI code cleanly within folder/state/styling boundaries |
| [assemble-page-or-screen](coding/assemble-page-or-screen/SKILL.md) | Build route/page/screen files that compose components without becoming messy |
| [connect-data-and-api](coding/connect-data-and-api/SKILL.md) | Connect UI to APIs through services, types, and loading/error states |
| [manage-state](coding/manage-state/SKILL.md) | Decide where state belongs and avoid unnecessary global state |
| [auth-and-access](coding/auth-and-access/SKILL.md) | Handle login, sessions, protected routes, roles, permissions, and redirects |
| [database-and-backend-logic](coding/database-and-backend-logic/SKILL.md) | Work with schemas, migrations, queries, backend routes, and data models |
| [dependency-and-config](coding/dependency-and-config/SKILL.md) | Handle packages, env variables, config files, lockfiles, and scripts safely |

### Testing (`testing/`)
| Skill | Purpose |
|---|---|
| [validate-and-test](testing/validate-and-test/SKILL.md) | Run or recommend existing lint, typecheck, test, and build commands |
| [manual-qa-and-regression](testing/manual-qa-and-regression/SKILL.md) | Check user flows, edge cases, visual states, and regressions |
| [error-handling-review](testing/error-handling-review/SKILL.md) | Review loading, error, empty, success, retry, and fallback states |

### Handoff & Launch (`handoff-and-launch/`)
| Skill | Purpose |
|---|---|
| [document-the-work](handoff-and-launch/document-the-work/SKILL.md) | Write or update README, setup docs, architecture notes, API docs, decision records |
| [handoff-notes](handoff-and-launch/handoff-notes/SKILL.md) | Prepare clear continuation notes for another developer or agent |
| [launch-readiness](handoff-and-launch/launch-readiness/SKILL.md) | Check readiness for deployment, release, env setup, and platform requirements |

### Cross-process (`cross-process/`)
| Skill | Purpose |
|---|---|
| [debug-and-fix](cross-process/debug-and-fix/SKILL.md) | Diagnose root cause before applying the smallest correct fix |
| [refactor-and-clean-up](cross-process/refactor-and-clean-up/SKILL.md) | Clean redundant code, unused files, and inconsistent structure without breaking behavior |
| [risk-review](cross-process/risk-review/SKILL.md) | Detect destructive, irreversible, or high-impact actions before acting |
| [review-before-final](cross-process/review-before-final/SKILL.md) | Check the work satisfies the original request before responding |
| [global-agent-output-and-reporting](cross-process/global-agent-output-and-reporting/SKILL.md) | Standardize how the agent reports completed work, assumptions, and next steps |

## Using these skills

These skills follow the open **Agent Skills standard** (the `SKILL.md` format originally introduced by Anthropic, now adopted across multiple coding agents). The skill content is identical everywhere — only the destination folder changes per tool, and each agent auto-detects relevant skills from the `description` field in the frontmatter.

| Agent | Skills folder |
|---|---|
| **Claude Code** | Personal: `~/.claude/skills/<skill-name>/` · Project: `.claude/skills/<skill-name>/` |
| **Google Antigravity** | Project: `.agents/skills/<skill-name>/` (also works in Antigravity CLI) |
| **Cursor** | `.cursor/skills/<skill-name>/` |
| **OpenAI Codex CLI** | `.codex/skills/<skill-name>/` |

For each, the structure is the same: a folder named after the skill, containing `SKILL.md` at its root. No conversion needed — copy the same folder into whichever path matches your agent(s).

> Note: Claude.ai (the chat app, not Claude Code) is the exception — it requires uploading a ZIP per skill via Customize → Skills, as described earlier in this README.

## Downloading skills into your project repo (generic process)

1. **Get the bundle**
   - Clone: `git clone https://github.com/<your-username>/app-development-skills.git`
   - Or download the ZIP/tarball from GitHub and extract it locally.

2. **Pick the skills you need**
   - Browse the category folders (`planning/`, `designing/`, `coding/`, etc.) and note the skill folder names you want (e.g. `connect-data-and-api`, `debug-and-fix`).
   - You don't need all 29 — copy only what's relevant to your project/agent.

3. **Create the skills directory in your project** (if it doesn't exist), matching your agent:
```bash
   mkdir -p .claude/skills      # Claude Code
   mkdir -p .agents/skills       # Google Antigravity
   mkdir -p .cursor/skills       # Cursor
   mkdir -p .codex/skills        # Codex CLI
```

4. **Copy the chosen skill folders in**, flattening the category structure (the agent only cares about the skill folder itself, not which category it was filed under):
```bash
   cp -r app-development-skills/coding/connect-data-and-api .claude/skills/
   cp -r app-development-skills/cross-process/debug-and-fix .claude/skills/
   cp -r app-development-skills/cross-process/global-agent-output-and-reporting .claude/skills/
   # ...repeat for each skill you want
```

5. **Commit them to your repo** so the whole team (and any agent working in the repo) gets the same skills:
```bash
   git add .claude/skills
   git commit -m "Add app-development-skills: connect-data-and-api, debug-and-fix, global-agent-output-and-reporting"
```

6. **Reload the agent session** (new chat/session, or restart the IDE extension) so it picks up the new skills — most agents load the skill list at session start.

7. **Keep skills in sync (optional)**: if you want updates from the bundle to propagate, either re-run steps 2–5 periodically, or add `app-development-skills` as a git submodule and symlink the specific skill folders into each agent's skills directory.

## Customizing

These skills are written as general-purpose starting points. Teams are encouraged to fork this repo and adjust:
- The default architecture convention, if your projects use a different structure.
- Styling conventions (the skills default to CSS Modules + design tokens, extending whatever the project already uses).
- The `global-agent-output-and-reporting` skill's reporting structure, if your team has its own reporting format.

## License

MIT — see [LICENSE](LICENSE).
