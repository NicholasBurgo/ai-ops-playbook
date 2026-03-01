---
id: tpl.rctfc
version: v1
type: template
status: stable
title: RCTFC Prompt Scaffold
created: 2026-03-01
tags: [template, framework, scaffold, universal]
models: [general]
source: https://www.reddit.com/r/PromptEngineering/comments/1r4b2y3/the_5layer_prompt_framework_that_makes_chatgpt/
inputs:
  - name: role
    required: true
    description: Who the model should act as
  - name: context
    required: true
    description: Background information and situation
  - name: task
    required: true
    description: What to do
  - name: format
    required: true
    description: Expected output structure
  - name: constraints
    required: false
    description: Restrictions, banned patterns, limits
failure_modes: Produces generic output if fields are left vague. The quality of this template is entirely dependent on the specificity of its inputs.
---

ROLE: {role}

CONTEXT: {context}

TASK: {task}

FORMAT: {format}

CONSTRAINTS: {constraints}

Execute the TASK using the CONTEXT. Follow the FORMAT exactly. Obey all CONSTRAINTS.

---

## Usage Notes

This is the most general-purpose prompt scaffold in the library. Use it when:
- No specialized template exists for your task.
- You are prototyping a new prompt before deciding on its final form.
- You want to standardize ad-hoc requests quickly.

For prompts with mixed instructions and data, consider tpl-xml-sections-v1 instead.
