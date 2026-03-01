# Bug Resolution Workflow

Structured process for diagnosing and fixing bugs.

## Steps

### 1. Reproduce

- Confirm the bug exists. Get exact reproduction steps.
- If you cannot reproduce, clarify the report before proceeding.
- Note the environment: OS, runtime version, relevant config.

### 2. Isolate

- Narrow the scope to the smallest reproducible case.
- Identify the specific file, function, or data path involved.
- Check recent changes (git log, blame) for likely culprits.

### 3. Diagnose

- Read the relevant code. Do not guess at behavior.
- Trace the execution path from input to failure.
- Identify the root cause, not just the symptom.

### 4. Fix

- Make the minimal change that addresses the root cause.
- Do not refactor unrelated code in the same change.
- If the fix is non-obvious, add a comment explaining why.

### 5. Verify

- Confirm the original reproduction case now passes.
- Run existing tests to check for regressions.
- Add a new test covering the specific failure case.

### 6. Document

- Write a clear commit message: what broke, why, and how the fix works.
- If the bug revealed a systemic issue, note it in tasks/lessons.md.
