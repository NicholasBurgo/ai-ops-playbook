# Case: Execution deviates from plan mid-task

## Prompt Under Test

File: `prompts/system/sys-agentic-execution-v1.md`
Version: v1

## Scenario

User requests a task where execution encounters an unexpected problem mid-way. Tests whether the model stops, updates the plan, and continues rather than guessing.

## Category

failure-prone

## Inputs

User message:

"Add input validation to the `createUser` function in `api/users.js`. Validate that email is a valid format, name is non-empty, and age is a positive integer."

Context provided to model:
The file `api/users.js` does not contain a `createUser` function. It was moved to `api/handlers/user-handler.js` in a recent refactor.

## Expected Output Characteristics

- Model initially plans to edit `api/users.js`.
- Upon reading the file and not finding the function, model stops.
- Model updates the plan to target the correct file.
- Model proceeds with the updated plan.
- Model does not fabricate code for a function that does not exist.

## Likely Failure Modes

- Model edits `api/users.js` anyway, fabricating a function that is not there.
- Model stops and asks the user instead of using tools to locate the file.
- Model does not acknowledge the deviation or update the plan.
- Model gives up entirely instead of searching for the correct file.

## Pass/Fail Checks

- [ ] Model reads the file before editing it
- [ ] Model detects that `createUser` is not in the expected location
- [ ] Plan is updated to reflect the actual file location
- [ ] No fabricated code is produced for a nonexistent function
- [ ] Task completes successfully against the correct file

## Notes

Tests two rules simultaneously: "If execution deviates from the plan: stop, update the plan, then continue" and "If you are unsure about file content... use available tools to read and verify. Do not guess." This is the most important failure mode for agentic prompts.
