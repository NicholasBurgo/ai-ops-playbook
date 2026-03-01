# Case: Research question with one dominant hypothesis

## Prompt Under Test

File: `prompts/roles/role-research-analyst-v1.md`
Version: v1

## Scenario

User asks a question where one explanation is overwhelmingly likely and alternatives are weak. Tests whether the model still forms competing hypotheses before concluding, rather than skipping straight to the obvious answer.

## Category

edge

## Inputs

User message:

"Our web application's response time jumped from 200ms to 4 seconds starting at exactly 2:00 AM last night. The only change deployed between 1:00 AM and 3:00 AM was a database migration that added an unindexed foreign key column to the orders table, which has 12 million rows. What caused the slowdown?"

## Expected Output Characteristics

- The model forms at least two competing hypotheses before concluding, even though the migration is the obvious cause.
- The conclusion identifies the unindexed column as the most likely cause but does not dismiss other possibilities without consideration.
- Confidence level is stated.
- Evidence for and against each hypothesis is summarized.
- Limitations or open questions are noted (e.g., "confirm with query execution plans").

## Likely Failure Modes

- Model skips hypothesis formation and immediately concludes it was the migration.
- Model presents only one hypothesis instead of competing alternatives.
- Model does not state a confidence level.
- Model fails to note any limitations or verification steps.

## Pass/Fail Checks

- [ ] At least two hypotheses are explicitly stated before the conclusion
- [ ] The dominant hypothesis is identified with supporting evidence
- [ ] At least one alternative hypothesis is considered with reasoning for why it is less likely
- [ ] A confidence level is stated for the conclusion
- [ ] Limitations or recommended verification steps are included

## Notes

When the answer is obvious, models tend to skip the analytical method and jump to conclusions. This tests whether the role prompt's method ("Form competing hypotheses before investigating") holds under pressure from a clear-cut scenario. The value of the method is that even obvious answers benefit from considering alternatives.
