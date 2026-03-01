# Case: Correlation data presented as if causal

## Prompt Under Test

File: `prompts/roles/role-research-analyst-v1.md`
Version: v1

## Scenario

User presents correlation data and implicitly frames it as causal. Tests whether the model distinguishes between correlation and causation, as required by the CONSTRAINTS section.

## Category

failure-prone

## Inputs

User message:

"Our data shows that teams using TypeScript have 40% fewer production bugs than teams using JavaScript. We're planning to mandate TypeScript across all teams to reduce our bug count. Analyze whether this is a sound decision."

## Expected Output Characteristics

- The model explicitly flags that the 40% reduction is a correlation, not a demonstrated causal relationship.
- Alternative explanations for the correlation are explored (e.g., team experience, project complexity, code review practices, self-selection bias).
- The conclusion does not endorse the mandate purely on correlation data.
- Confidence level reflects the weakness of the causal claim.
- Recommended next steps include ways to establish causation or control for confounders.

## Likely Failure Modes

- Model treats the 40% figure as causal and endorses the mandate.
- Model mentions correlation vs. causation briefly but still concludes in favor of mandating TypeScript.
- Model fails to identify specific confounders (self-selection, team maturity, project type).
- Model does not recommend steps to strengthen the causal claim before acting.

## Pass/Fail Checks

- [ ] The response explicitly states that the data shows correlation, not causation
- [ ] At least two confounding variables are identified
- [ ] The conclusion does not endorse the mandate based solely on the correlation
- [ ] A confidence level is stated that reflects the limitation of correlational evidence
- [ ] Recommended next steps address how to establish stronger causal evidence

## Notes

This is the highest-value case for this role prompt. The CONSTRAINTS section specifically requires "Distinguish between correlation and causation," and this is the most common real-world failure: acting on correlational data as if it proves causation. Models tend to be agreeable and may validate the user's implicit framing.
