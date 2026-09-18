---
name: refine-prompt
description: Improve an existing prompt after researching the target model's current official guidance. Use when the user asks to fix, tighten, rewrite, or adapt a prompt they already have.
---

# Refine a prompt

## 1. Ask if missing

- Which model will run it?
- Reasoning / effort level?
- What is wrong with the current prompt, or what should change?
- Local project involved? Path?

Do not rewrite until those are clear enough to avoid guessing.

## 2. Baseline, then live search

Read the matching file in `.cursor/skills/create-prompt/labs/`, then **search official docs for that exact model**. Fix stale patterns (over-specified steps, “think step by step”, generic personas, effort stuffed into prose). Live docs beat the lab file.

## 3. Return

- What you changed and why (from the docs, not vibes)
- The revised copyable prompt (**English** unless the user asked for another language)
- Effort / thinking setting to use
- A short **expected result** in the language the user used in this chat. Schematic numbered list (`1.` `2.` `3.`). Each item is one plain line: what they will see or have after that prompt is run. Not a recap of the prompt.
