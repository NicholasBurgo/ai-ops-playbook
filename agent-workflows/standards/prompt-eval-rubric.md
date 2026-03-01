# Prompt Evaluation Rubric

Use this rubric to evaluate prompts before adding or updating them in the library.

## Dimensions

### 1. Clarity (Pass/Fail)

- The prompt's intent is unambiguous on first read.
- Instructions are ordered logically.
- No contradictory rules.

### 2. Specificity (1-3)

- **1**: Vague ("write good code").
- **2**: Directional but missing output format or constraints.
- **3**: Explicit about task, format, and constraints.

### 3. Reusability (1-3)

- **1**: Only works for one specific scenario with hardcoded context.
- **2**: Works across a category but needs manual adjustment.
- **3**: Fully parameterized with clear variable placeholders.

### 4. Output Control (1-3)

- **1**: No output format specified.
- **2**: Format mentioned but not enforced (e.g., "preferably JSON").
- **3**: Format strictly defined with schema or structure.

### 5. Failure Awareness (Pass/Fail)

- Known failure modes are documented.
- The prompt handles edge cases or explicitly scopes them out.

## Minimum Bar for Inclusion

A prompt must score:

- Clarity: Pass
- Specificity: 2+
- Reusability: 2+
- Output Control: 2+
- Failure Awareness: Pass

Prompts below this bar should be revised or moved to `examples/` as reference material.

## Recording an Evaluation

When documenting an evaluation, use this format in the PR description or frontmatter:

```yaml
eval:
  clarity: pass
  specificity: 3
  reusability: 3
  output_control: 2
  failure_awareness: pass
  notes: "Output control could be tighter; JSON schema not included."
```
