---
id: tpl.xml.sections
version: v1
type: template
status: stable
title: XML Section Scaffold
created: 2026-03-01
tags: [template, xml, anthropic, structured, disambiguation]
models: [claude-3, claude-4, general]
source: https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices
inputs:
  - name: instructions
    required: true
    description: Core task instructions
  - name: context
    required: false
    description: Background information, documents, data
  - name: examples
    required: false
    description: Input/output examples
  - name: input
    required: true
    description: The actual input to process
  - name: output_format
    required: false
    description: Desired output structure
failure_modes: Requires discipline to keep tags consistent. Omit unused sections entirely rather than including empty tags.
---

<instructions>
{instructions}
</instructions>

<context>
{context}
</context>

<examples>
{examples}
</examples>

<input>
{input}
</input>

<output_format>
{output_format}
</output_format>

Follow <instructions> as the primary directive. Use <context> for background. Match the pattern in <examples> if provided. Process <input> and return results per <output_format>.

---

## Usage Notes

Use XML tags when a prompt mixes instructions, context, and data to prevent the model from confusing one for another. Particularly effective with Claude but works across providers.

Omit unused sections. Do not include empty tags.
