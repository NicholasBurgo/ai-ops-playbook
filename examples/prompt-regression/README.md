# Prompt Regression Testing

This directory contains input/output cases used to validate prompt behavior across versions.

## Structure

Each prompt with regression tests gets a subdirectory named after the prompt (without version suffix):

```
prompt-regression/
  regression-case-template.md
  sys-agentic-execution/
    case-01-normal-multi-step.md
    case-02-edge-trivial-task.md
    case-03-failure-plan-deviation.md
  role-code-reviewer/
    case-01-normal-mixed-findings.md
    case-02-edge-clean-code.md
```

## Creating a New Case

1. Copy `regression-case-template.md` into the appropriate prompt subdirectory.
2. Rename to `case-NN-<short-description>.md`.
3. Fill in all sections. Do not leave placeholders.
4. Aim for one normal case, one edge case, and one failure-prone case per prompt.

## Case Categories

| Category | Purpose |
|----------|---------|
| normal | Standard usage that should always work correctly. |
| edge | Boundary condition or unusual input that tests prompt limits. |
| failure-prone | Scenario where the prompt is likely to break or produce bad output. |

## Running Cases

Cases are designed for manual evaluation. To run a case:

1. Load the prompt under test as the system/role/task instruction.
2. Provide the inputs from the case file.
3. Evaluate the output against the pass/fail checks.
4. Record model, date, and result in the Notes section.

## When to Add Cases

- When a new prompt is added to the library (required for promotion to `stable`).
- When a prompt is updated (validate the change does not break existing behavior).
- When a failure is discovered (add a case that reproduces it).

## Minimum Coverage

| Prompt Type | Required Cases for `stable` |
|-------------|----------------------------|
| System | 2 |
| Role | 2 |
| Task | 1 |
| Template | 1 (if behavioral, not purely structural) |

At least one case must be category `edge` or `failure-prone`. Happy-path-only coverage does not qualify for promotion. See `standards/repo-rules.md` for the full promotion gate.
