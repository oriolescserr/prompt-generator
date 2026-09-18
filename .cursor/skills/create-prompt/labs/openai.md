# OpenAI / GPT

Durable patterns. Confirm the **named** GPT (and reasoning vs non-reasoning) on [developers.openai.com](https://developers.openai.com/api/docs/guides/prompt-guidance) before shipping.

## Structure

- Outcome-first: goal, success criteria, constraints, evidence, output shape, stop rules.
- Leave the path to the model. Over-specified step lists often hurt newer GPT reasoning models.
- Use ALWAYS / NEVER only for real invariants (safety, required fields). For judgment, write decision rules.
- Keep prompts lean. Repeated rules and leftover process text from older models add noise.
- Delimiters (markdown, XML, headings) for distinct input parts.

```text
❌ ALWAYS search. ALWAYS think step by step. NEVER answer without three tools.
✅ Success means: eligibility decided from policy + account evidence; complete allowed actions; return completed_actions, customer_message, blockers. If a required field is missing, ask for that field only.
```

## Reasoning

- Set `reasoning.effort` (and any mode the live docs document). Do not recover quality with “think harder” prose.
- Avoid chain-of-thought prompts on reasoning models (“think step by step”, “explain your hidden reasoning”).
- Try zero-shot first; few-shot only when the output contract is picky, and keep examples aligned with the instructions.
- Verbosity is often a separate control (`text.verbosity`) plus prompt length rules.

## Behavior to plan for

- Flagship models may **ask** when a gap would change the outcome. If you want autonomy, say what in-scope work they may finish without asking.
- Put approval only on destructive / external / scope-expanding actions.
- For tools: what the tool is for, when to use it, what “done” is. Expose only relevant tools.
- Skills / `AGENTS.md` are followed closely. Conflicting files cause pauses. Say user instructions win if that is true.

## Prompt skeleton

```text
Role:
Goal:
Success criteria:
Constraints:
Tools:
Output:
Stop rules:
```
