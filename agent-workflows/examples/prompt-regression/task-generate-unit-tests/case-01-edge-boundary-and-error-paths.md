# Case: Function with boundary values and error paths

## Prompt Under Test

File: `prompts/tasks/task-generate-unit-tests-v1.md`
Version: v1

## Scenario

User provides a function with integer boundaries, null handling, and an expected exception path. Tests whether the generated tests cover all three categories (happy path, edge cases, failure paths) as required.

## Category

edge

## Inputs

code:

```python
def paginate(items: list, page: int, page_size: int) -> dict:
    """Return a page of items with metadata.

    Raises ValueError if page < 1 or page_size < 1.
    Returns empty results list if page exceeds available pages.
    """
    if page < 1 or page_size < 1:
        raise ValueError("page and page_size must be >= 1")
    start = (page - 1) * page_size
    end = start + page_size
    total_pages = -(-len(items) // page_size)  # ceiling division
    return {
        "results": items[start:end],
        "page": page,
        "page_size": page_size,
        "total_pages": total_pages,
        "total_items": len(items),
    }
```

framework: pytest

focus_areas: (not provided)

## Expected Output Characteristics

- Tests cover the happy path (normal pagination through a list).
- Tests cover edge cases: empty list, page_size larger than list, last page with partial results, page exactly at boundary.
- Tests cover failure paths: page=0, page=-1, page_size=0, page_size=-1 all raise ValueError.
- Each test has a descriptive name that communicates what it verifies.
- Tests use pytest conventions (plain functions, assert statements, pytest.raises for exceptions).

## Likely Failure Modes

- Model only generates happy-path tests and skips boundary values.
- Model does not test the ValueError paths with pytest.raises.
- Model tests page=0 but misses page_size=0 or negative values.
- Model does not test the empty list case.
- Model uses unittest-style classes instead of pytest functions.

## Pass/Fail Checks

- [ ] At least one happy-path test exists (normal pagination)
- [ ] At least one test covers an empty input list
- [ ] At least one test verifies ValueError is raised for invalid page or page_size
- [ ] At least one test covers the boundary between last valid page and beyond
- [ ] All tests use pytest conventions (no unittest.TestCase)
- [ ] Each test function name describes the scenario being tested

## Notes

This function has a compact but complete surface area: happy path, boundary values (page/page_size = 1, list length boundaries), and explicit error paths. A test generation prompt that cannot cover all three categories on a function this clear is not production-ready.
