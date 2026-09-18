# DeepSeek

Durable patterns. Confirm the **named** DeepSeek on [api-docs.deepseek.com thinking mode](https://api-docs.deepseek.com/guides/thinking_mode/) before shipping.

## Structure

- Normal chat messages: system for standing rules, user for the task.
- Be explicit about the final answer vs scratch work. Visible CoT is a **API field** (`reasoning_content`), not something you should demand in `content`.
- JSON / schemas when the caller must parse the result.

## Reasoning

- Thinking is typically a request flag (`thinking` enabled/disabled) plus `reasoning_effort`.
- Effort aliases on the wire change; **look up the named model**. Compatibility maps (e.g. medium → high) are not something to hardcode.
- Temperature / some sampling knobs are ignored or clamped in thinking mode. Do not prompt around that; set the API correctly.
- With **tools**, pass `reasoning_content` back every turn or the API may 400. Without tools, prior CoT is often dropped.

## Behavior to plan for

- Default thinking is often on. If the user wants a fast non-thinking prompt, say so and reflect that in the **settings**, not with “don’t think” in the text unless docs require it.
- `tool_choice` required/named may be illegal while thinking is on.

## Prompt skeleton

```text
System: standing rules, output contract.
User: the problem, constraints, definition of done.
```

Tell the user which thinking / effort fields to send with the prompt.
