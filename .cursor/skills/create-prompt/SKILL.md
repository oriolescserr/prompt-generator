---
name: create-prompt
description: Specialist workflow to write a ready-to-paste model prompt. Uses lab baselines, then always searches official docs for the exact model named. Use when the user asks to create, write, generate, or craft a prompt.
---

# Create a prompt

You are a specialist. Lab files save time. They do **not** replace a live lookup of the model the user named.

## 1. Ask

Ask only what is still unknown:

1. Which model?
2. How much reasoning / effort? (`low` / `medium` / `high` / `xhigh` / `max` / off / default)
3. What should the prompt make that model do? What does done look like?
4. Is this related to a project on this computer? If yes, where is it?

If you do not fully understand the task, ask. If they give a path, read only what you need.

## 2. Baseline, then live search

1. Read the matching file under [labs/](labs/):
   - Claude / Anthropic → [labs/anthropic.md](labs/anthropic.md)
   - GPT / OpenAI / Codex → [labs/openai.md](labs/openai.md)
   - Gemini / Google → [labs/google.md](labs/google.md)
   - Grok / xAI / Grok Build → [labs/xai.md](labs/xai.md)
   - DeepSeek → [labs/deepseek.md](labs/deepseek.md)
   - Composer / Cursor Cloud Agent / Cursor Grok → [labs/cursor.md](labs/cursor.md)
   - Mistral → [labs/mistral.md](labs/mistral.md)
   - Unknown family → skip the lab file
2. **Search the internet for that exact model** (prompting guide, thinking/effort, migration). Prefer the vendor site. Training data and lab files go stale.
3. If live docs conflict with the lab file, the live docs win. If you still have doubts, ask the user.

## 3. Write

One copyable prompt:

- **Write the prompt in English** unless the user explicitly asks for another language (their chat language does not change this)
- Shape it like the lab **and** the live page for that model
- Goal, constraints, success criteria, output shape, when to ask vs act
- Set reasoning with the vendor’s effort/thinking control, not fake chain-of-thought, unless the live guide says otherwise
- Ground in the local project only if you inspected it

Then give: model + effort, URLs from **this** search, the prompt, where to paste it.

Then a short **expected result** in the language the user used in this chat. Schematic numbered list (`1.` `2.` `3.`). Each item is one plain line: what they will see or have after someone runs that prompt. No jargon dump, no restating the XML.

Stop unless they want a revision.
