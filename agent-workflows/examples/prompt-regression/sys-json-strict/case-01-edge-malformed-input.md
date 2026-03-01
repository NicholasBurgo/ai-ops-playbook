# Case: Malformed input triggers error JSON

## Prompt Under Test

File: `prompts/system/sys-json-strict-v1.md`
Version: v1

## Scenario

User provides ambiguous, incomplete input that cannot fulfill the requested JSON schema. Tests whether the model returns the error object instead of guessing or adding commentary.

## Category

edge

## Inputs

Schema provided alongside system prompt:

```json
{
  "type": "object",
  "properties": {
    "name": { "type": "string" },
    "age": { "type": "integer" },
    "email": { "type": "string", "format": "email" }
  },
  "required": ["name", "age", "email"]
}
```

User message:

"Parse this into the schema: 'John, maybe 30ish, no contact info given'"

## Expected Output Characteristics

- Output is valid JSON (parseable, no syntax errors).
- The model returns `{"error": "<description>"}` because the email field is required but not provided and the age is ambiguous.
- No markdown fences, no commentary outside the JSON object.

## Likely Failure Modes

- Model guesses an email or fabricates one to fill the schema.
- Model approximates the age (30) and returns a complete object instead of an error.
- Model wraps the output in ```json fences.
- Model adds a text explanation before or after the JSON.

## Pass/Fail Checks

- [ ] Output is valid JSON (parseable by a strict JSON parser)
- [ ] Output uses the error format: `{"error": "..."}`
- [ ] No fabricated email address appears in the output
- [ ] No markdown wrapping or commentary outside the JSON object

## Notes

Tests the error path defined in the prompt rules. Models strongly prefer to produce "helpful" complete responses, which conflicts with strict schema adherence when required fields cannot be populated.
