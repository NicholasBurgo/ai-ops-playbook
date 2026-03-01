---
id: task.generate.unit.tests
version: v1
type: task
status: draft
title: Unit Test Generation
created: 2026-03-01
tags: [testing, unit-tests, code-generation, quality]
models: [general]
source: https://code.visualstudio.com/docs/copilot/customization/prompt-files
inputs:
  - name: code
    required: true
    description: The source code or file to generate tests for
  - name: framework
    required: true
    description: Test framework (e.g., pytest, jest, xunit)
  - name: focus_areas
    required: false
    description: Specific functions or areas to prioritize
failure_modes: Can hallucinate APIs or method signatures if the full code under test is not provided. Always include the actual source.
---

Generate unit tests for the provided code.

INPUTS
- Code under test: {code}
- Test framework: {framework}
- Focus areas (if specified): {focus_areas}

REQUIREMENTS
1. Cover the happy path for each public function or method.
2. Cover edge cases: empty inputs, null/undefined, boundary values, type mismatches.
3. Cover failure paths: expected exceptions, error returns, invalid state.
4. Each test should be independent and self-documenting through its name.
5. Use the specified test framework's conventions and assertions.

CONSTRAINTS
- Do not mock what you can construct. Prefer real objects over mocks when practical.
- Do not test private implementation details unless they represent critical logic.
- If dependencies must be mocked, use the framework's standard mocking pattern.
- Include all necessary imports and setup.
