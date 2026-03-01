# Planning Protocol

Use this workflow before starting any non-trivial task.

## When to Plan

A plan is required when the task involves:

- More than 3 discrete steps
- Changes across multiple files or systems
- New dependencies or architectural decisions
- Irreversible actions
- Unclear requirements that need assumption-surfacing

## Plan Structure

```
Objective
  One sentence: what does "done" look like?

Assumptions
  What are you assuming about context, requirements, or constraints?

Constraints
  Hard limits: time, budget, backward compatibility, security.

Steps
  1. Step with expected outcome
  2. Step with expected outcome
  ...

Verification
  How will you prove this works? Tests, manual checks, logs, demo?

Completion Condition
  Specific, observable condition that means the task is finished.
```

## Rules

- Do not start execution until the plan is written.
- If requirements are ambiguous, list your assumptions and proceed. Flag them for review.
- If execution deviates from the plan, stop and update the plan before continuing.
- Plans are living documents. Update them as you learn.
- Keep plans short. A plan longer than the implementation is overthinking.
