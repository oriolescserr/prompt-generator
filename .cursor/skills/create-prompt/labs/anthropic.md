# Anthropic / Claude

Durable patterns. Confirm the **named** Claude (Opus, Sonnet, Haiku, Fable, …) on [platform.claude.com](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices) before shipping.

## Structure

- Be clear and direct. Treat Claude as a new hire who lacks your norms.
- Say **why** a constraint exists; Claude generalizes from the reason.
- Use XML (or consistent markdown) for mixed blocks: instructions, context, examples, input.
- 3–5 diverse examples beat long prose when format/tone matter.
- Numbered steps when order or completeness matters.

```text
❌ Create a dashboard
✅ Create an analytics dashboard. Include relevant features and interactions. Go beyond a static layout.
```

## Reasoning

- Depth is usually an **API/product effort or thinking setting**, not “think step by step” in the prompt.
- Do not tell Claude to echo, transcribe, or dump internal reasoning into the user-visible answer (can trigger refusals on some models).
- Effort ≠ verbosity. If you need a short reply, prompt for length separately.

## Behavior to plan for

- Recent Claude models follow instructions **literally**. If a rule applies to every section, say so.
- Do not add extra verification/subagent loops unless the live page still wants them; some models already self-check.
- For coding agents: specify the full task up front; constrain scope (“do only what was asked”).
- Frontend: name palette, type, and layout. “Make it clean” often collapses to a house style.

## Prompt skeleton

```text
<role>...</role>
<goal>...</goal>
<constraints>...</constraints>
<context>...</context>
<output>...</output>
<when_to_ask>...</when_to_ask>
```
