# Prompt Catalog

Index of all prompts in this library. Updated when prompts are added, promoted, or deprecated.

## System Prompts

| File | Purpose | Status | Regression |
|------|---------|--------|------------|
| [sys-agentic-execution-v1](../prompts/system/sys-agentic-execution-v1.md) | Enforce planning, verification, and controlled execution for agentic tasks | stable | 3 cases |
| [sys-research-citations-v1](../prompts/system/sys-research-citations-v1.md) | Research mode with strict source discipline and citation requirements | draft | 2 cases |
| [sys-json-strict-v1](../prompts/system/sys-json-strict-v1.md) | Force strict JSON-only output for pipelines and automation | stable | 2 cases |

### sys-agentic-execution-v1

- **When to use**: Agentic coding sessions where the model executes multi-step tasks autonomously.
- **When not to use**: Quick single-question interactions where planning overhead is unnecessary.
- **Inputs**: None (session-wide behavior).
- **Output shape**: Model follows planning/verification protocol; produces proof before marking done.
- **Composes with**: Any role or task prompt. Pairs well with role-code-reviewer-v1 for review tasks.

### sys-research-citations-v1

- **When to use**: Research sessions requiring verified claims and source discipline.
- **When not to use**: Casual fact-checking or creative writing where citations add friction.
- **Inputs**: None (session-wide behavior).
- **Output shape**: None. This prompt enforces sourcing and uncertainty constraints. Output structure is owned by the composed role or task prompt.
- **Composes with**: role-research-analyst-v1 (role owns output format; this prompt's citation rules apply as constraints within that format).

### sys-json-strict-v1

- **When to use**: Pipelines or automation that parse model output as JSON.
- **When not to use**: Human-facing responses where markdown or prose is expected.
- **Inputs**: Requires a JSON schema provided alongside this prompt.
- **Output shape**: Raw JSON object, no wrapping or commentary.
- **Composes with**: Any task prompt. Do not combine with role prompts that define prose output formats.

## Role Prompts

| File | Purpose | Status | Regression |
|------|---------|--------|------------|
| [role-code-reviewer-v1](../prompts/roles/role-code-reviewer-v1.md) | Structured code review persona with prioritized findings | stable | 2 cases |
| [role-research-analyst-v1](../prompts/roles/role-research-analyst-v1.md) | Hypothesis-driven analysis persona with evidence weighting | draft | 2 cases |

### role-code-reviewer-v1

- **When to use**: Code review of diffs, PRs, or specific files.
- **When not to use**: Greenfield code generation (use a task prompt instead).
- **Inputs**: Code diff or file content.
- **Output shape**: Prioritized list (Critical / Important / Suggestion) with file references and fix snippets.
- **Composes with**: sys-agentic-execution-v1. Avoid combining with sys-json-strict-v1 unless you restructure the output format.

### role-research-analyst-v1

- **When to use**: Complex research with multiple possible interpretations or ambiguous evidence.
- **When not to use**: Simple factual lookups or single-source questions.
- **Inputs**: Research question or topic.
- **Output shape**: Conclusion with confidence, evidence summary, limitations, next steps.
- **Composes with**: sys-research-citations-v1 (role's output format takes precedence; system's citation rules apply as constraints).

## Task Prompts

| File | Purpose | Status | Regression |
|------|---------|--------|------------|
| [task-prompt-debugger-v1](../prompts/tasks/task-prompt-debugger-v1.md) | Diagnose prompt failures and propose minimal fixes | draft | 1 case |
| [task-generate-unit-tests-v1](../prompts/tasks/task-generate-unit-tests-v1.md) | Generate unit tests for provided code | draft | 1 case |

### task-prompt-debugger-v1

- **When to use**: A prompt produces bad output and you need to identify the root cause.
- **When not to use**: When the issue is input quality, not prompt quality.
- **Inputs**: system_prompt (required), bad_outputs (required), expected_behavior (optional).
- **Output shape**: Diagnosis, root cause, fix (replacement text), risk assessment.
- **Composes with**: Any system prompt. Works standalone for quick diagnosis.

### task-generate-unit-tests-v1

- **When to use**: You have source code and need comprehensive unit test coverage.
- **When not to use**: Integration or E2E tests (this targets unit tests only).
- **Inputs**: code (required), framework (required), focus_areas (optional).
- **Output shape**: Complete test file with imports, setup, and test cases.
- **Composes with**: sys-agentic-execution-v1 for autonomous test generation workflows.

## Templates

| File | Purpose | Status | Regression |
|------|---------|--------|------------|
| [tpl-rctfc-v1](../prompts/templates/tpl-rctfc-v1.md) | Universal RCTFC scaffold (Role/Context/Task/Format/Constraints) | stable | none |
| [tpl-xml-sections-v1](../prompts/templates/tpl-xml-sections-v1.md) | XML tag scaffold for mixed instructions/context/data | stable | none |
| [tpl-fewshot-classification-v1](../prompts/templates/tpl-fewshot-classification-v1.md) | Few-shot classification with labeled examples | stable | none |

### tpl-rctfc-v1

- **When to use**: Prototyping a new prompt or standardizing an ad-hoc request.
- **When not to use**: When a specialized template or task prompt already exists for the job.
- **Inputs**: role, context, task, format, constraints.
- **Output shape**: Determined by the format field.

### tpl-xml-sections-v1

- **When to use**: Prompts that mix instructions with context, examples, and input data.
- **When not to use**: Simple single-instruction prompts where XML tags add complexity for no benefit.
- **Inputs**: instructions, context, examples, input, output_format.
- **Output shape**: Determined by the output_format field.

### tpl-fewshot-classification-v1

- **When to use**: Classification, labeling, or categorization tasks.
- **When not to use**: Tasks where examples are unavailable or the label space is too large for few-shot.
- **Inputs**: label_task, examples (2-5 I/O pairs), input.
- **Output shape**: Single label matching example format.

## Lifecycle Summary

| Status | Count | Prompts |
|--------|-------|---------|
| stable | 6 | sys-agentic-execution-v1, sys-json-strict-v1, role-code-reviewer-v1, tpl-rctfc-v1, tpl-xml-sections-v1, tpl-fewshot-classification-v1 |
| draft | 4 | sys-research-citations-v1, role-research-analyst-v1, task-prompt-debugger-v1, task-generate-unit-tests-v1 |
| deprecated | 0 | |
