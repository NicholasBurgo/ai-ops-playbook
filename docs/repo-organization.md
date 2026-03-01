# Repository Organization

This document explains the structure of the prompt and workflow library.

## Top-Level Folders

### prompts/

Standalone instruction artifacts. Each file is a complete prompt that can be used directly or composed into workflows.

Subfolders:

- `system/`: Global behavior rules applied to an entire session. High-leverage, high-risk. Changes require regression testing.
- `roles/`: Persona definitions. Define who the model is and how it operates. Do not include specific tasks.
- `tasks/`: One-shot reusable instructions for specific jobs. Parameterized where possible.
- `templates/`: Structural scaffolds with placeholders. Used to construct new prompts from proven patterns.

### workflows/

Multi-step procedures that require orchestration: sequencing, tool calls, state management, or human-in-the-loop decisions.

Subfolders:

- `planning/`: Pre-execution planning processes.
- `coding/`: Development workflows (bug fixing, code review, testing).
- `research/`: Research and analysis procedures.

### standards/

Policy and governance files. Define how prompts are written, evaluated, and maintained.

### examples/

Evidence artifacts: input/output pairs, transcripts, regression tests, demo outputs. Used for evaluation and demonstration, not as prompt definitions.

### tasks/

Operational tracking: backlog, lessons learned, decision log.

### docs/

Repository-level documentation and architecture explanations.

## Rules and Standards

Folder placement rules, naming conventions, versioning, and lifecycle are defined in the standards directory. Do not duplicate them here.

- **Folder boundaries and decision rules**: `standards/repo-rules.md`
- **Naming and frontmatter**: `standards/prompt-style-guide.md`
- **Prompt composition**: `standards/prompt-composition-rules.md`
- **Evaluation**: `standards/prompt-eval-rubric.md`
- **Prompt catalog**: `docs/prompt-catalog.md`
