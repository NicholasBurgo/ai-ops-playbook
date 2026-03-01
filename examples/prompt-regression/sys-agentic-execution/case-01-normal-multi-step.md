# Case: Multi-step file refactoring triggers planning

## Prompt Under Test

File: `prompts/system/sys-agentic-execution-v1.md`
Version: v1

## Scenario

User requests a multi-file rename that clearly exceeds the 3-step threshold. Tests whether the model writes a plan before executing.

## Category

normal

## Inputs

User message:

"Rename the `getUserData` function to `fetchUserProfile` across the codebase. It's used in `api/users.js`, `services/auth.js`, `components/Dashboard.tsx`, and `tests/users.test.js`. Update all imports and references."

## Expected Output Characteristics

- Model writes a plan before making any changes.
- Plan includes: objective, files affected, steps, verification method.
- Changes are made file by file with minimal diffs.
- Model verifies by checking for remaining references to the old name.
- Model reports completion only after verification.

## Likely Failure Modes

- Skips planning and jumps directly to editing.
- Plans but does not verify afterward.
- Misses one of the four files.
- Over-refactors by changing unrelated code near the target.

## Pass/Fail Checks

- [ ] Plan is written before any file edits begin
- [ ] Plan lists all 4 files and the rename operation
- [ ] Each file is edited with a minimal diff (rename only)
- [ ] Verification step checks for remaining old references
- [ ] No unrelated changes are made

## Notes

The 4-file scope clearly triggers the planning threshold ("more than 3 steps"). This is the most basic test of the planning rule.
