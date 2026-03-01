# Case: Code review with mixed-severity findings

## Prompt Under Test

File: `prompts/roles/role-code-reviewer-v1.md`
Version: v1

## Scenario

A code diff containing a SQL injection vulnerability, a performance issue, and otherwise acceptable code. Tests whether findings are correctly prioritized in the Critical / Important / Suggestion format.

## Category

normal

## Inputs

Code diff:

```python
# api/auth.py
def authenticate(request):
    username = request.params.get("username")
    password = request.params.get("password")
    query = f"SELECT * FROM users WHERE username='{username}' AND password='{password}'"
    result = db.execute(query)
    if result:
        users = list(result)
        all_users = list(db.execute("SELECT * FROM users"))
        return {"authenticated": True, "user": users[0], "total_users": len(all_users)}
    return {"authenticated": False}
```

## Expected Output Characteristics

- SQL injection flagged as Critical with a fix using parameterized queries.
- Plaintext password comparison flagged as Critical with a fix using hashing.
- Unnecessary full-table scan (`SELECT * FROM users`) flagged as Important (performance).
- Findings use the tiered format: Critical first, then Important, then Suggestion.
- Each finding includes file reference, issue description, and concrete fix.

## Likely Failure Modes

- Misses the SQL injection.
- Reports issues but does not provide concrete fixes.
- Uses a flat list instead of the tiered priority format.
- Invents issues not present in the diff (e.g., missing imports when none are shown).

## Pass/Fail Checks

- [ ] SQL injection identified as Critical
- [ ] Plaintext password handling identified as Critical
- [ ] Unnecessary full-table scan identified as Important or Suggestion
- [ ] Each finding includes a concrete fix (parameterized query, password hashing, targeted query)
- [ ] Output uses Critical / Important / Suggestion tier format
- [ ] No fabricated issues outside the provided diff

## Notes

This code has intentionally clear issues at different severity levels. The primary test is prioritization and format compliance, not whether the model can find bugs.
