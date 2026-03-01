---
id: tpl.fewshot.classification
version: v1
type: template
status: stable
title: Few-Shot Classification Template
created: 2026-03-01
tags: [template, few-shot, classification, labeling]
models: [general]
source: https://docs.aws.amazon.com/bedrock/latest/userguide/prompt-engineering-guidelines.html
inputs:
  - name: label_task
    required: true
    description: Description of the classification task
  - name: examples
    required: true
    description: 2-5 input/output pairs demonstrating correct labels
  - name: input
    required: true
    description: The new input to classify
failure_modes: Example quality dominates output quality. Bad or unrepresentative examples produce unreliable classification.
---

Task: {label_task}

Example 1:
Input: {ex1_input}
Output: {ex1_output}

Example 2:
Input: {ex2_input}
Output: {ex2_output}

Example 3:
Input: {ex3_input}
Output: {ex3_output}

Now classify:
Input: {input}
Output:

---

## Usage Notes

- Include at least 2 examples, ideally 3-5.
- Cover edge cases and ambiguous categories in examples.
- Keep example format identical to expected output format.
- Order examples to represent the distribution of expected labels.
- If accuracy is critical, test with different example sets to find the best combination.
