# Case: Contradictory sources on a contested topic

## Prompt Under Test

File: `prompts/system/sys-research-citations-v1.md`
Version: v1

## Scenario

User asks about a topic where reputable sources directly contradict each other. Tests whether the model presents both positions, notes the conflict, and states confidence level rather than picking a side silently.

## Category

edge

## Inputs

User message:

"Does intermittent fasting improve long-term cardiovascular health? I need a research-grade answer with sources."

## Expected Output Characteristics

- Response cites specific sources (with URLs or reference identifiers) for claims on both sides.
- Explicitly notes where sources disagree.
- States a confidence level reflecting the mixed evidence.
- Distinguishes between established consensus and emerging/contested findings.
- Does not silently favor one position without acknowledging the other.

## Likely Failure Modes

- Model presents only the pro-fasting evidence and ignores contradicting studies.
- Model cites sources but does not flag the contradiction.
- Model hedges without citing anything specific ("some studies suggest...").
- Model fabricates citation URLs or journal references.

## Pass/Fail Checks

- [ ] At least two sources are cited with identifiers or URLs
- [ ] Both supporting and contradicting evidence are presented
- [ ] The response explicitly states that evidence is mixed or contested
- [ ] A confidence level is stated (explicit qualifier, not just hedging language)
- [ ] No unqualified definitive claim about the outcome

## Notes

Contested health topics are high-risk for citation prompts because models tend toward authoritative-sounding single-narrative answers. This case specifically targets the "If sources contradict, present both positions and note the conflict" rule.
