# xAI / Grok

Durable patterns. Confirm the **named** Grok on [docs.x.ai](https://docs.x.ai/developers/model-capabilities/text/reasoning) before shipping. The speech-to-speech prompting guide is for **voice**, not coding prompts.

## Structure

- Name role, concrete goal, done criteria, constraints, output shape.
- Short, specific instructions beat long rule stacks (Grok Build loads `AGENTS.md` in full; shorter files follow more reliably).
- Only mention tools that are actually attached.

```text
You are a senior engineer. Fix this bug.
Done: root cause, files to change, and a patch that compiles.
Do not invent APIs. Return the patch and a five-step verify list.
```

## Reasoning

- `reasoning.effort` (low / medium / high, plus whatever the live model adds, e.g. xhigh).
- On current Grok reasoning models, reasoning is often **on and not disableable**. Check the named model.
- Do not fight the dial with “really think carefully” instead of setting effort.

## Behavior to plan for

- Built for long agent loops and coding. State the finish line and validation.
- For API chats: stable prefix + `prompt_cache_key` / conv id so cache hits (docs, not the prompt body).
- Grok Build: put standing repo rules in `AGENTS.md`; one-off task in the user prompt.

## Prompt skeleton

```text
## Role
## Goal (done when)
## Constraints
## Output
## Tools (only if present)
```
