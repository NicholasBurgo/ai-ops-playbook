# Case: Model suppresses explanatory commentary around JSON

## Prompt Under Test

File: `prompts/system/sys-json-strict-v1.md`
Version: v1

## Scenario

User asks a question that naturally invites explanation. Tests whether the model suppresses all non-JSON text and returns only the JSON object.

## Category

failure-prone

## Inputs

Schema provided alongside system prompt:

```json
{
  "type": "object",
  "properties": {
    "sentiment": { "type": "string", "enum": ["positive", "negative", "neutral"] },
    "confidence": { "type": "number", "minimum": 0, "maximum": 1 },
    "reasoning": { "type": "string" }
  },
  "required": ["sentiment", "confidence", "reasoning"]
}
```

User message:

"What's the sentiment of this review? I'd also love to understand your thinking. Review: 'The battery life is incredible but the screen is dim and hard to read outdoors. Overall I'm satisfied but wouldn't recommend it for outdoor use.'"

## Expected Output Characteristics

- Output is a single JSON object with sentiment, confidence, and reasoning fields.
- No preamble like "Here's my analysis:" or "Sure, let me help."
- No trailing commentary like "Let me know if you need anything else."
- The reasoning field contains the explanation (inside JSON), not as free text outside the object.

## Likely Failure Modes

- Model adds conversational preamble before the JSON ("Sure! Here's the analysis:").
- Model adds a closing remark after the JSON.
- Model wraps the JSON in ```json markdown fences.
- Model produces the reasoning as prose outside the JSON and returns a minimal JSON object.

## Pass/Fail Checks

- [ ] Output starts with `{` and ends with `}` (no surrounding text)
- [ ] No markdown fences anywhere in output
- [ ] sentiment field is one of: positive, negative, neutral
- [ ] reasoning field is a non-empty string explaining the analysis
- [ ] No text exists outside the JSON object

## Notes

The user's phrasing ("I'd also love to understand your thinking") strongly invites conversational response. This tests whether the strict JSON system prompt overrides that pressure. This is the most common real-world failure mode for JSON-only prompts.
