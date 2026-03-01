# AI Ops Playbook

A version-controlled library of production-grade AI prompts, workflows, and operational standards.

## What This Is

An engineering system for managing AI prompts and workflows. Every prompt is structured with metadata, evaluated against a rubric, and maintained with version control. This is a library, not a collection of tips.

## Structure

```
prompts/
  system/      Behavior rules for entire sessions
  roles/       Persona definitions with constraints
  tasks/       Reusable single-shot instructions
  templates/   Parameterized scaffolds for prompt construction
workflows/
  planning/    Pre-execution planning processes
  coding/      Development workflows
  research/    Research and analysis procedures
standards/     Style guide, repo rules, evaluation rubric
examples/      I/O pairs, regression tests, demo outputs
tasks/         Backlog and lessons learned
docs/          Repository documentation
```

## Prompt Categories

| Category | Purpose | Example |
|----------|---------|---------|
| System | Set global model behavior for a session | Agentic execution protocol |
| Role | Define a persona and operating constraints | Code reviewer, research analyst |
| Task | Execute a specific job with defined output | Generate unit tests, debug a prompt |
| Template | Provide reusable structural scaffolding | RCTFC scaffold, XML sections, few-shot |

## Key Concepts

**Prompts vs Workflows**: A prompt is a standalone instruction. A workflow is a multi-step process that may use prompts as building blocks.

**Prompts vs Examples**: A prompt defines behavior. An example demonstrates or tests it with real input/output pairs.

**Standards vs Docs**: Standards are rules you follow when contributing. Docs explain why the repo is organized the way it is.

**Prompt Composition**: Prompts can be combined across layers (system + role + task). Not all combinations are valid. See `standards/prompt-composition-rules.md` for precedence rules, valid/invalid combinations, and anti-patterns.

**Prompt Lifecycle**: Every prompt has a status: `draft`, `stable`, or `deprecated`. Prompts without regression coverage remain `draft` until validated. See the lifecycle rules in `standards/repo-rules.md`.

**Prompt Catalog**: A full index of every prompt with purpose, usage guidance, composition notes, and lifecycle state is maintained in `docs/prompt-catalog.md`.

## Using This Repo

For day-to-day usage, including how to choose prompts, compose layers, use prompts in Cursor, handle failures, and decide when to add new prompts, see `docs/how-to-use-this-repo.md`.

## Naming Convention

All prompt files follow: `{type}-{topic}-v{major}.md`

| Prefix | Type |
|--------|------|
| sys- | System prompt |
| role- | Role prompt |
| task- | Task prompt |
| tpl- | Template |

Version is bumped on breaking changes only. Minor edits are done in-place.

## Evaluation

Every prompt must meet the minimum bar defined in `standards/prompt-eval-rubric.md`:

- Clear and unambiguous
- Specific about task and output format
- Reusable (parameterized, not hardcoded to one scenario)
- Failure modes documented

## Contributing

1. Follow the style guide: `standards/prompt-style-guide.md`
2. Place the file in the correct folder: see `docs/repo-organization.md`
3. Include YAML frontmatter with all required fields
4. Add at least one example case to `examples/`
5. Document known failure modes
6. Submit for review against the eval rubric

## License

MIT
