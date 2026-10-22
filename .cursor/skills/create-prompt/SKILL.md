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
4. Where will the prompt run? (Claude Code, Cursor, Codex, or a chat with no plugins)
5. Is this related to a project on this computer? If yes, where is it?

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

## 3. Plugins on this computer

Do this after the model and the host are known, before writing. The plugins are the ones for **the host that will run the prompt**, on this machine. Not the plugins of the session that is writing the prompt.

A plain chat or API call has no local plugins. Skip this step.

Notes live in `.host-plugins/`, one file per host: `.host-plugins/claude-code.md`, `.host-plugins/codex.md`, `.host-plugins/cursor.md`. The folder is gitignored. Slug the host name in lowercase with hyphens. If the folder or that host's file is missing, create them. Do not open or edit the other hosts' files. Do not commit the folder, and do not copy it into the repo.

List the enabled plugins for this run: global, plus the target project when there is one. Ignore marketplace entries that are not installed.

- **Claude Code.** From the target project directory, run `claude plugin list --json`. Keep rows with `enabled: true`. `user` is global; `project` and `local` are that repo; `skills-dir` and `synced` count. If the command fails, read `enabledPlugins` in `~/.claude/settings.json`, `<project>/.claude/settings.json`, and `<project>/.claude/settings.local.json`. A later file overrides the same id. Install paths are in `~/.claude/plugins/installed_plugins.json`.
- **Cursor.** Read `plugin.json` name and description under `~/.cursor/plugins`, and skill descriptions in the target project's `.cursor/skills`. User skills Cursor loads count as global.
- **Codex.** Read `~/.codex/plugins` and `~/.codex/skills`, plus plugin config in the target project. Do not invent a list command.
- **Any other host.** Search that product's config and plugin folders. If you cannot find them, ask. Do not guess a path.

Compare that list with this host's file only. Match on id, scope, and project path. Leave other projects' entries in that file as they are.

- Already listed, still enabled: keep it. Do not open the plugin again. A name on the list at the end counts as listed.
- New, and a generated prompt might name it: read its manifest and the descriptions of its skills, then add an entry. Write what it does from those texts. Write when a prompt should name it. Do not guess either one.
- New, and only the person at the keyboard uses it (a preview, a pet, or other host chrome): a generated prompt would never name it. Add the id to `## Not used in prompts` at the end of the file. No explanation.
- Gone from this slice (global, or this project): delete the entry or the id.

One entry looks like this:

```text
### plugin-id
- scope: user | project | local
- project: path or -
- version: version or -
- what: one or two sentences from the plugin itself
- use when: the kind of prompt that should name it
```

End the file with the ids a prompt will never name:

```text
## Not used in prompts

- plugin-id
```

Use the notes when you write. If one already covers part of the task, name it in the prompt and tell the agent to use it. Do not copy its steps into the prompt. Leave unused plugins out. When the prompt depends on one, say so next to where to paste it.

## 4. Write

One copyable prompt:

- **Write the prompt in English** unless the user explicitly asks for another language (their chat language does not change this)
- Shape it like the lab **and** the live page for that model
- Goal, constraints, success criteria, output shape, when to ask vs act
- Set reasoning with the vendor’s effort/thinking control, not fake chain-of-thought, unless the live guide says otherwise
- Ground in the local project only if you inspected it

Then give: model + effort, URLs from **this** search, the prompt, where to paste it.

After the prompt, before the expected result, name every plugin or skill the prompt tells the model to use. One short line each: the id, and why this prompt names it. If it names none, say that no plugin was used and give the reason in one short line (a plain chat, or none of the enabled plugins fit this task). Same language as the expected result.

Then a short **expected result** in the language the user used in this chat. A numbered list with as many items as the outcome needs, at most 5. Each item is one plain line: what they will see or have after someone runs that prompt. No jargon dump, no restating the XML.

Stop unless they want a revision.
