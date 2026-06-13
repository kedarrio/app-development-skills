---
name: clarify-the-request
description: Decide whether a request is clear enough to act on, and if not, ask only the minimum necessary clarification questions before starting work. Use this skill whenever a request is ambiguous, could be interpreted multiple ways with materially different outcomes, is missing information needed for a high-impact or irreversible change, or when you're about to make a risky assumption. Do not use it to stall on simple, low-risk tasks.
---

# Clarify the Request Skill

## Purpose
Ensure work starts on the right understanding by asking only the questions that would materially change the outcome — and making safe, stated assumptions for everything else.

## When to Use
- The request is ambiguous and multiple reasonable interpretations would lead to different results.
- The task is high-impact, irreversible, or affects many files (architecture, auth, schema, deployment).
- Required information (e.g. which data source, which design direction, which user role) is missing and can't be inferred from the project.
- The user's goal isn't clear enough to plan correctly.

## When Not to Use
- The task is simple, low-risk, and a reasonable default exists (e.g. "fix this typo", "add a loading spinner to this button").
- The project conventions already answer the ambiguity (e.g. styling approach is obvious from existing code).
- Clarifying would only confirm something that's already inferable at low risk.

## Required Inputs
- The user's request as given.
- Context already gathered from the Understand the Project Skill (if applicable).

## Assumptions
- The user prefers progress over interrogation; minimize friction.
- Low-risk ambiguities should be resolved with a stated assumption, not a question.
- High-risk ambiguities (data loss, security, architecture-wide changes) must always be clarified.

## Step-by-Step Workflow
1. **List open questions**: identify every point where the request could be interpreted in more than one way.
2. **Classify each open question** as:
   - **High impact** — affects correctness, safety, architecture, or is hard to reverse.
   - **Low impact** — affects style/detail only, easy to change later.
3. **Resolve low-impact questions yourself** by choosing the most likely interpretation based on project conventions and stating the assumption briefly in your response.
4. **For high-impact questions**, draft the minimum set of questions needed (ideally 1, rarely more than 3).
5. **Combine related questions** into a single message rather than asking one at a time.
6. **Ask the questions**, then wait for the answer before proceeding with the affected parts of the task. Unaffected parts of the task can proceed in parallel if safe.
7. **Record assumptions** made for low-impact items so they can be reported later via the Global Agent Output and Reporting Skill.

## Rules and Best Practices
- Ask only questions that would materially change the result.
- Prefer one well-formed question over several scattered ones.
- State assumptions explicitly and briefly rather than silently picking one.
- If the project convention already answers the question, don't ask — follow the convention.
- For naming, copy wording, minor layout choices, or other easily-reversible details, proceed with a sensible default.
- For anything touching auth, permissions, schema, deployment, deletion, or broad architecture changes, always clarify before acting, even if a "likely" answer exists.

## Safety Checks
- Never proceed on a high-impact assumption without asking.
- Never invent business logic, data models, or requirements that aren't stated or inferable from the project.
- If clarification is needed but the user is unavailable mid-task, pause the affected work and clearly state what's blocked and why.

## Validation Checks
- Confirm every high-impact ambiguity has either been clarified or explicitly flagged as blocking.
- Confirm every low-impact assumption is documented for the final report.
- Confirm the number of questions asked is minimal (1–3) and each one is necessary.

## Common Mistakes to Avoid
- Asking multiple rounds of trivial questions before starting simple work.
- Silently guessing on high-impact, hard-to-reverse decisions.
- Asking vague questions ("what do you want me to do?") instead of specific ones ("should deleting a user also delete their posts, or just deactivate the account?").
- Re-asking something the project conventions already make clear.
- Bundling unrelated questions about different parts of the task in a confusing way.

## Output Rule
Do not invent a custom final response format for this skill. Follow the Global Agent Output and Reporting Skill. Only include skill-specific reporting details when necessary for understanding the completed work.
