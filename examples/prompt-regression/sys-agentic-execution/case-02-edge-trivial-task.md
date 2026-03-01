# Case: Trivial question does not trigger planning

## Prompt Under Test

File: `prompts/system/sys-agentic-execution-v1.md`
Version: v1

## Scenario

User asks a simple factual question that requires no plan. Tests whether the model avoids unnecessary planning overhead for trivial requests.

## Category

edge

## Inputs

User message:

"What does the `Array.prototype.flat()` method do in JavaScript?"

## Expected Output Characteristics

- Model answers directly without writing a plan.
- Response is concise and accurate.
- No unnecessary verification section for a factual question.

## Likely Failure Modes

- Model writes a plan for a single-question factual lookup (over-applies the protocol).
- Model asks for confirmation before answering.
- Model appends a verification section that adds no value.

## Pass/Fail Checks

- [ ] No plan is written for this simple question
- [ ] Answer is factually correct
- [ ] Response is concise (no protocol overhead)

## Notes

Tests the implicit threshold: tasks under 3 steps should not trigger planning. The prompt says "If a task involves more than 3 steps... write a plan first." A factual question is 1 step. This is the edge case that reveals whether the protocol is applied too rigidly.
