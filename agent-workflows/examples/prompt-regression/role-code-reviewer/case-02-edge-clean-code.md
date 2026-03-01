# Case: Clean code produces brief acceptance

## Prompt Under Test

File: `prompts/roles/role-code-reviewer-v1.md`
Version: v1

## Scenario

A well-written code diff with no bugs, security issues, or performance concerns. Tests whether the model says "code is acceptable" briefly instead of inventing issues to fill space.

## Category

edge

## Inputs

Code diff:

```python
# utils/retry.py
import time
from typing import Callable, TypeVar

T = TypeVar("T")

def retry(fn: Callable[..., T], max_attempts: int = 3, delay: float = 1.0) -> T:
    """Call fn up to max_attempts times, waiting delay seconds between failures."""
    last_error: Exception | None = None
    for attempt in range(max_attempts):
        try:
            return fn()
        except Exception as e:
            last_error = e
            if attempt < max_attempts - 1:
                time.sleep(delay)
    raise last_error
```

## Expected Output Characteristics

- Model acknowledges the code is acceptable.
- Response is brief.
- May include minor Suggestions (e.g., exponential backoff, logging) but does not flag them as Critical or Important.
- Does not fabricate security or correctness issues.

## Likely Failure Modes

- Invents a bug that is not present.
- Flags style preferences as Critical or Important.
- Produces a long review for simple, correct code.
- Fails to explicitly state the code is acceptable.

## Pass/Fail Checks

- [ ] No false Critical or Important findings
- [ ] Model explicitly states the code is acceptable or has no significant issues
- [ ] Review is brief (not padded to fill space)
- [ ] Any suggestions are clearly marked as optional

## Notes

Tests the constraint: "If the code is acceptable, say so briefly. Do not invent issues." This is the edge case that reveals whether the reviewer role over-generates findings.
