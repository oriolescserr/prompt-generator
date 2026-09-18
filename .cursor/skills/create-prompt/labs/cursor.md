# Cursor (Composer, Cursor Grok, Cloud Agents)

Durable patterns. Confirm the **named** Cursor model on [cursor.com/docs](https://cursor.com/docs) / help and, for Cloud Agents, the current [Cloud Agents API](https://cursor.com/docs/cloud-agent/api/endpoints).

## Structure

- Cursor models are **coding agents**: goal, repo constraints, files that matter, how to verify (test, screenshot, command).
- Put standing conventions in `.cursor/rules` / `AGENTS.md`. The generated prompt is the **task**, not a second style guide.
- Be explicit about scope (what not to refactor) and approval (push, production, secrets).

## Reasoning and model choice

- Effort and Fast are **picker / `model.params`**, not paragraphs in the prompt. Discover valid params for that model (`GET /v1/models` or the product UI).
- Composer-class: everyday implementation, tight edit/run loops, cost-sensitive.
- Cursor Grok-class: harder, longer, more ambitious first versions. Effort low → xhigh as the product allows.
- Cloud Agent body: `prompt.text` plus `model.id` and params. Do not assume a slug from memory.

## Behavior to plan for

- Strong instruction following across many rules. Keep the task prompt short so rules and the task do not fight.
- Ask for a local project path; ground the prompt in that tree.
- Fast mode can change billing; mention it in “how to use”, not inside the prompt text.

## Prompt skeleton

```text
Task:
Repo / paths:
Constraints:
Done when (verification):
Do not:
```
