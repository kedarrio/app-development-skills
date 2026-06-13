---
name: write-product-text
description: Write clear, specific app microcopy — button labels, empty states, error messages, onboarding text, form labels and helper text, tooltips, and confirmation/success messages. Use this skill whenever a task requires writing or rewriting any user-facing text in the app, or when implementing UI that includes text not yet specified. Do not use it for marketing copy, blog content, or long-form documentation.
---

# Write Product Text Skill

## Purpose
Write app microcopy that is clear, specific, and useful — helping users understand what happened, what to do next, and what an action will do.

## When to Use
- Implementing UI that needs labels, messages, or copy not explicitly provided.
- Writing or improving error messages, empty states, confirmations, or onboarding text.
- Reviewing existing copy that is vague, generic, or unclear.

## When Not to Use
- Marketing pages, blog posts, or long-form content (different skill/process).
- The exact copy has already been specified by the user/design and just needs to be implemented as-is.

## Required Inputs
- The context: what screen/state/action this text supports.
- The user's goal at that moment.
- Any existing tone/voice conventions in the app (check existing copy for tone).

## Assumptions
- Existing copy style/tone in the app should be matched unless asked to change it.
- Copy should describe the actual behavior — never describe a state or action that isn't real.

## Step-by-Step Workflow
1. **Identify the context**: what screen, what state (empty, error, loading, success, confirmation), what action.
2. **Identify the user's question at this moment**: e.g. "what went wrong?", "what happens if I click this?", "is this empty because there's no data, or because of a filter?"
3. **Draft copy that answers that question directly**:
   - **Buttons**: describe the action (e.g. "Save changes", "Delete project", not "Submit" or "OK" for consequential actions).
   - **Empty states**: explain why it's empty and what to do next (e.g. "No projects yet — create your first project to get started.").
   - **Error messages**: state what went wrong and, if possible, what to do (e.g. "Couldn't save changes. Check your connection and try again.").
   - **Confirmations**: state what was completed and any relevant next step (e.g. "Project deleted.").
   - **Form helper text**: reduce confusion before the user makes a mistake (e.g. format hints, requirements).
   - **Onboarding**: short, action-oriented, focused on the immediate next step.
4. **Match existing tone/voice**: check similar existing copy in the app for formality, terminology, and phrasing patterns.
5. **Keep it concise**: remove filler words; one clear sentence is usually better than two vague ones.
6. **Avoid generic AI-sounding phrasing** (e.g. "Oops! Something went wrong!", "Great job!", "Let's get started!") unless this matches the app's established voice.

## Rules and Best Practices
- Button labels describe the action, especially for consequential actions (delete, remove, cancel subscription).
- Error messages should never be vague placeholders like "An error occurred" when a more specific message is reasonably available.
- Empty states should differentiate "no data exists" vs. "no results match your filters" when relevant.
- Confirmation messages should confirm what happened, not just "Success."
- Don't invent claims about what an action does — copy must match actual behavior/implementation.
- Keep terminology consistent across the app (don't call the same concept by different names in different places).
- Avoid unnecessary exclamation points, emoji, or hype unless that matches the established voice.

## Safety Checks
- Don't write copy that promises functionality that doesn't exist (e.g. "Your changes are backed up automatically" if no backup exists).
- For destructive actions, ensure copy clearly communicates the consequence (e.g. "This will permanently delete this project and all its data.").

## Validation Checks
- Confirm copy matches the actual behavior of the action/state it describes.
- Confirm terminology is consistent with the rest of the app.
- Confirm error messages give the user a sense of what to do next where possible.
- Confirm destructive action copy clearly states the consequence.

## Common Mistakes to Avoid
- Generic, non-descriptive button labels ("Submit", "OK", "Click here") for actions with real consequences.
- Vague error messages ("Something went wrong") when the actual cause/remedy is knowable.
- Empty states that don't explain why or what to do.
- Overly cheerful or generic "AI-sounding" copy that doesn't match the app's voice.
- Inconsistent terminology for the same concept across screens.

## Output Rule
Do not invent a custom final response format for this skill. Follow the Global Agent Output and Reporting Skill. Only include skill-specific reporting details when necessary for understanding the completed work.
