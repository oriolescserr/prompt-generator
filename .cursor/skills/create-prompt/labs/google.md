# Google / Gemini

Durable patterns. Confirm the **named** Gemini on [ai.google.dev prompting strategies](https://ai.google.dev/gemini-api/docs/prompting-strategies) and that model’s thinking docs before shipping.

## Structure

- Direct and short. Verbose “prompt engineering” from older models can make Gemini over-analyze.
- Put role, hard constraints, and output format in the system instruction or at the **start**.
- Long context (docs, code, video): **data first, question last**. Anchor with “Based on the document above…”.
- Negative constraints last when they must stick.
- Few-shot when format/tone must be stable.

## Reasoning

- Gemini thinking models reason **internally**. Do not require a visible plan unless you need it for the user.
- Set `thinking_level` / thinking config from the **live** page for that model (names and defaults change).
- Do not combine legacy `thinking_budget` with `thinking_level` on Gemini 3-class APIs.
- Keep sampling at the documented default for thinking work unless the live guide says otherwise.

## Behavior to plan for

- Default answers are terse. If you want a chatty tutor, say so.
- For grounded-only tasks, state that provided context is the only source of truth and what to do when the answer is not in it.
- “Think very hard” can add thinking tokens; prefer the thinking parameter when the docs offer one.

## Prompt skeleton

```text
<role>precise specialist for [domain]</role>
<instructions>
1. Do the task.
2. Stay inside the given constraints.
3. Return [format].
</instructions>
[long context]
[question last]
```
