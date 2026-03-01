# Case: Vague bad outputs with no expected behavior specified

## Prompt Under Test

File: `prompts/tasks/task-prompt-debugger-v1.md`
Version: v1

## Scenario

User provides a system prompt and bad outputs, but expected_behavior is omitted and the bad_outputs are vague. Tests whether the task prompt still produces a structured diagnosis rather than punting.

## Category

edge

## Inputs

system_prompt:

```
You are a helpful customer support agent. Answer questions about our product. Be concise. If you don't know, say so.
```

bad_outputs:

```
Output 1: "I'd be happy to help! Our product is amazing and has many great features. Let me tell you all about it! First, we have..."
Output 2: "Absolutely! Great question! Our product is the best solution for your needs because..."
```

expected_behavior: (not provided)

## Expected Output Characteristics

- Diagnosis identifies the failure mode (likely "scope creep" or "instruction ignored" given the prompt says "Be concise").
- Root cause points to specific prompt text that is insufficient (e.g., "Be concise" is too vague to prevent effusive responses).
- Fix proposes a concrete replacement, not just "make it better."
- Risk section notes what might change as a side effect of the fix.

## Likely Failure Modes

- Model asks for more information instead of diagnosing with what is available.
- Model produces a vague diagnosis that mirrors the vague input ("the outputs are too verbose").
- Model proposes a rewrite of the entire prompt instead of a minimal fix.
- Model does not identify the specific instruction responsible ("Be concise" is too weak).

## Pass/Fail Checks

- [ ] Diagnosis names a specific failure mode from the PROCESS list
- [ ] Root cause identifies the specific instruction(s) that are insufficient
- [ ] Fix provides exact replacement text, not just advice
- [ ] Fix is a minimal edit, not a full prompt rewrite
- [ ] Risk section is present and identifies at least one potential side effect

## Notes

The task prompt's failure_modes note says "Vague complaints produce vague fixes." This case tests whether the structured PROCESS in the prompt is strong enough to produce useful output even when the user input is imprecise. The model must infer expected behavior from the system prompt's own instructions.
