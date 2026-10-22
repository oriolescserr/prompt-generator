# Prompt Generator

A Cursor workspace to structure ideas you already have into prompts that fit the model you will run them on.

Say what you want in natural language. The agent turns that into a clear, ready-to-paste prompt, following the **official prompting guides** for the exact model you named. This is not an app and not a catalog of every model version.

## How it works

1. **Ask**: model, reasoning/effort, where the prompt will run, what it should do, and whether a project on this computer is involved (and its path).
2. **Baseline**: read a short lab note for that family (Claude, GPT, Gemini, Grok, DeepSeek, Cursor, Mistral) so the draft is not starting from zero.
3. **Search**: look up current official prompting, thinking, and effort docs for the named snapshot. Lab notes lose to live docs.
4. **Plugins**: compare the enabled plugins of that host (global and the target project) with its own file in `.host-plugins/` (`claude-code.md`, `codex.md`, `cursor.md`). The folder is gitignored. If the file is missing, it is created. New plugins a prompt might name are read once and noted (what they do, when to name them). A plugin that is only for the person using the host, such as an image preview, is listed by name at the end of the file. Removed plugins are deleted. A plugin already noted is not read again.
5. **Write**: one copyable prompt in **English** (unless you ask for another language), plus where to paste it and which reasoning setting to use.

If anything about the task would change the prompt, the agent asks instead of guessing.

## Use it

In Cursor, with this folder as the workspace:

- *Create a prompt for …*
- *Write a prompt that …*
- *Tighten this prompt for Grok 4.6 high*

You will be asked for the target model and effort if you omit them. If the work is tied to another repo, give the path so the prompt can be grounded in real files.

## What you get back

- Target model and effort
- Official pages used **in that session**
- A single prompt to paste
- How to set thinking / reasoning in the product or API
- The plugins that prompt names, or a one-line reason when it names none
- A short numbered expected result in the language you used in chat (what you should have once that prompt has been run)

## Repository layout

```text
.cursor/rules/
  prompt-specialist.mdc      # this repo only writes prompts
  ask-dont-guess.mdc         # model, effort, task, project path
  baselines-then-search.mdc  # lab notes ≠ live model spec

.cursor/skills/
  create-prompt/             # new prompts
    SKILL.md
    labs/                    # family patterns (not version lists)
  refine-prompt/             # rewrite an existing prompt

.host-plugins/               # local plugin notes, gitignored, one file per host
```

### Lab baselines

| File | Family |
| --- | --- |
| `labs/anthropic.md` | Claude |
| `labs/openai.md` | GPT / Codex |
| `labs/google.md` | Gemini |
| `labs/xai.md` | Grok / Grok Build |
| `labs/deepseek.md` | DeepSeek |
| `labs/cursor.md` | Composer, Cursor Grok, Cloud Agents |
| `labs/mistral.md` | Mistral |

These files hold **stable prompting style** (structure, what belongs in the prompt vs an effort slider, common failure modes). They do not pin model IDs, default effort, or thinking APIs. Those change; the live search is required.

For an unknown provider, the lab step is skipped and the agent searches only.

## Requirements

- [Cursor](https://cursor.com) with network access so the agent can fetch vendor docs
- A named target model (Claude, GPT, Gemini, Grok, Composer, DeepSeek, Mistral, or another model)
