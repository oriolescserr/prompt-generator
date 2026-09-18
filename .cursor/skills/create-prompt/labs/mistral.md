# Mistral

Durable patterns. Confirm the **named** Mistral model on [docs.mistral.ai prompting](https://docs.mistral.ai/inference/prompting) before shipping.

## Structure

- Split **system** (standing behavior) and **user** (this request). If you cannot set system, prepend the rules to the user message.
- Open with purpose: “You are a …, your task is to …”.
- Hierarchical markdown (or XML). A stranger should be able to run the prompt with no extra context.
- Few-shot for format. Prefer real user/assistant turns when the output must match a schema.
- Use structured outputs / JSON schema when the app must parse the reply. Do not only describe the JSON in prose if the API can enforce it.

## Avoid

- Fuzzy words: “interesting”, “too long”, “many”, “make it better”. Use measurable criteria.
- Contradictory bullets. Use a decision tree.
- Asking the model to count characters/tokens; pass counts in.
- Generating huge blobs when a small delta would do.
- Numeric rating scales; worded scales work better, then map to numbers in code.

## Prompt skeleton

```text
You are a [role], your task is to [task].
# Rules
# Output format
# Examples
```
