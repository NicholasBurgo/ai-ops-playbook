# Repository Rules

## Folder Boundaries

| Folder | Contains | Does NOT Contain |
|--------|----------|-----------------|
| prompts/system | Global behavior rules, safety anchors, output mode enforcers | Task-specific instructions, user context |
| prompts/roles | Persona definitions with capability and constraint scoping | Actual tasks or user queries |
| prompts/tasks | Single-shot reusable task instructions | Multi-step orchestration, tooling config |
| prompts/templates | Parameterized scaffolds with placeholders | Filled-in examples (those go in examples/) |
| workflows/ | Multi-step procedures, chains, tool-use sequences, state flows | Standalone prompt text |
| standards/ | Policy: style guides, rubrics, contribution rules | Prompts, examples, or workflows |
| examples/ | I/O pairs, transcripts, regression tests, demo outputs | Prompt definitions or policy |
| tasks/ | Backlog, lessons learned, operational tracking | Prompt definitions or documentation |
| docs/ | Repo-level documentation, architecture explanations | Standards or prompts |

## Decision Rule

- If it can run as a single prompt: `prompts/`
- If it requires multiple steps, tools, state, or approvals: `workflows/`
- If it proves or demonstrates behavior: `examples/`
- If it governs how things are written: `standards/`

## Versioning

- Bump the major version (`v1` to `v2`) when the prompt's output schema, mandatory steps, or behavior changes in a non-backward-compatible way.
- Do not create a new file for minor wording fixes. Edit in place and update frontmatter.
- Old versions are preserved in git history, not as separate files.

## Lifecycle

Every prompt has a `status` field in frontmatter: `draft`, `stable`, or `deprecated`.

| Status | Meaning | Requirements |
|--------|---------|-------------|
| draft | Usable but not yet validated | Has frontmatter and follows style guide. May lack regression cases. |
| stable | Validated and relied upon | At least 2 regression cases (system/role) or 1 case (task/template). No known unresolved failure modes. |
| deprecated | Superseded or no longer recommended | Frontmatter includes a note pointing to the replacement. File remains for reference until removed. |

Promotion rules:

- New prompts enter as `draft`.
- Templates may be `stable` without regression cases if the pattern is structurally proven and carries minimal behavioral risk.
- A prompt moves to `deprecated` when a better alternative exists or the prompt is no longer reliable. Add a `deprecated_by` field to frontmatter pointing to the replacement.

### Promotion Gate: draft to stable

A non-template prompt may only be promoted to `stable` when **all** of the following are true:

1. **Regression coverage met.** At least 2 cases for system/role prompts, or 1 case for task prompts.
2. **Edge or failure case exists.** At least one regression case must be category `edge` or `failure-prone`. Happy-path-only coverage is insufficient.
3. **No unresolved composition conflict.** The prompt must not duplicate responsibilities held by another layer (system vs role vs task). Check `standards/prompt-composition-rules.md`.
4. **Catalog entry is current.** The prompt's entry in `docs/prompt-catalog.md` matches the prompt's actual behavior, inputs, output shape, and composition notes.
5. **Last revision has rationale.** The most recent meaningful edit to the prompt must have a commit message or frontmatter note explaining the change.

If any condition is not met, the prompt stays `draft` regardless of age or usage.

The current lifecycle state of all prompts is tracked in `docs/prompt-catalog.md`.

## Contribution Process

1. Write the prompt following `standards/prompt-style-guide.md`.
2. Add frontmatter with all required fields.
3. Add at least one example case to `examples/` demonstrating expected behavior.
4. Note known failure modes in frontmatter or a comment block.
5. Submit for review. Reviewer checks against `standards/prompt-eval-rubric.md`.

## What Does Not Belong in This Repo

- API keys, tokens, or credentials
- Model configuration files (temperature, top-p) without accompanying prompts
- Blog posts or opinion pieces
- Prompts that only work for one specific user's context without being parameterized
- Empty placeholder files (remove .gitkeep once a real file exists in the directory)
