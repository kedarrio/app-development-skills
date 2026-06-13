---
name: launch-readiness
description: Check readiness for deployment or release — environment setup, build success, app store or platform requirements, and known risks. Use this skill when asked to prepare for launch/release/deployment, before merging a significant feature to a production-bound branch, or when reviewing whether the app is ready to ship to users. Covers web (Next.js/Vite) and native (Expo/App Store/Play Store) contexts.
---

# Launch Readiness Skill

## Purpose
Verify the app is genuinely ready for deployment or release — builds succeed, environment/config is correct, platform requirements are met, and known risks are surfaced before shipping.

## When to Use
- Preparing for a deployment/release.
- Reviewing a feature branch before it merges to a production-bound branch.
- Explicitly asked "is this ready to launch/ship?"

## When Not to Use
- Early/mid-development tasks with no near-term release intent.
- Routine commits with no deployment implications.

## Required Inputs
- The build/deploy process (scripts, CI config, hosting target, app store pipeline if native).
- Environment variable requirements for the target environment.
- Recent changes since the last release (for risk context).

## Assumptions
- "Ready" means build succeeds, required config is present, and known risks are documented — not that every possible edge case is handled.
- Platform requirements (app store guidelines, web hosting requirements) follow the project's existing target platforms.

## Step-by-Step Workflow
1. **Run the build** for the target environment (web build, or native build/prebuild for Expo) — confirm it succeeds (see Validate and Test Skill).
2. **Check environment configuration**: confirm all required environment variables are documented (`.env.example`/equivalent) and that the target environment has them set (without exposing secret values).
3. **Check for leftover debug artifacts**: console logs not intended for production, debug flags left enabled, test/mock data left in place.
4. **For web (Next.js/Vite)**: check routing works in production build mode, check for broken links/assets, check meta/SEO basics if relevant.
5. **For native (Expo)**: check app config (`app.json`/`app.config.*`) for correct app name, version/build number, icons/splash screens, permissions declared match what the app actually uses, and platform-specific requirements (iOS/Android) per the project's target.
6. **Run final validation**: lint/typecheck/test/build per Validate and Test Skill.
7. **Run a final manual QA pass** on critical flows (see Manual QA and Regression Skill) — especially anything changed recently.
8. **Compile known risks/unresolved issues**: anything not fully tested, known limitations, follow-ups planned for after launch.
9. **Confirm rollback/monitoring basics exist** if the project has them (don't introduce new infra, just confirm existing safety nets are in place and not disabled).

## Rules and Best Practices
- Don't claim "ready to launch" without actually running the build and core validation.
- Treat unresolved high-impact issues (auth, data integrity, payment flows) as blockers — surface them clearly rather than downplaying.
- Check that environment-specific config (API URLs, keys) is correctly set for the target environment, not pointing at dev/staging by mistake.
- For native apps, double-check version/build numbers are incremented per the project's release convention if applicable.
- Keep a clear separation between "must fix before launch" and "known issue, acceptable for this release."

## Safety Checks
- Don't proceed with a release if the build fails or critical flows are broken — flag as a blocker.
- Don't disable failing checks/tests to force a "ready" status.
- Flag any change to deployment config, environment variables, or permissions as high-impact (see Risk Review Skill) before finalizing.

## Validation Checks
- Confirm production/release build succeeds.
- Confirm required environment variables are present for the target environment.
- Confirm no debug/test artifacts remain in production-bound code.
- Confirm critical flows pass manual QA.
- Confirm native app config (icons, permissions, version) is correct if applicable.

## Common Mistakes to Avoid
- Declaring "ready to launch" without running the build or tests.
- Missing environment variables required only in production.
- Leaving debug logs, test data, or feature flags in an unintended state.
- Treating a known critical bug as "minor" to avoid delaying launch.
- Forgetting platform-specific requirements (app icons, permissions, version bumps) for native releases.

## Output Rule
Do not invent a custom final response format for this skill. Follow the Global Agent Output and Reporting Skill. Only include skill-specific reporting details when necessary for understanding the completed work.
