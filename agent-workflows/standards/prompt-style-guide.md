# Prompt Style Guide

Rules for writing and formatting prompts in this repository.

## Frontmatter Schema

Every prompt file uses YAML frontmatter:

```yaml
---
id: <type>.<topic>              # e.g., sys.agentic.exec, role.code.reviewer
version: v1                     # major version only; bump on breaking changes
type: system|role|task|template
status: draft|stable|deprecated # lifecycle state (see standards/repo-rules.md)
title: <human-readable title>
created: YYYY-MM-DD
tags: [searchable, terms]
models: [general]               # or specific: [gpt-4, claude-3]
---
```

Additional optional fields (use when relevant):

- `inputs`: list of variables with `name`, `required`, `description`
- `output_format`: markdown|json|xml|text
- `source`: URL or reference for derived prompts
- `failure_modes`: known weaknesses

Do not add fields you cannot fill. An empty field is worse than a missing one.

## Naming Convention

Files follow the pattern: `{type}-{topic}-v{major}.md`

| Type | Prefix | Example |
|------|--------|---------|
| System | sys- | sys-agentic-execution-v1.md |
| Role | role- | role-code-reviewer-v1.md |
| Task | task- | task-generate-unit-tests-v1.md |
| Template | tpl- | tpl-rctfc-v1.md |

Rules:

- Lowercase, hyphen-separated
- No spaces, no underscores
- Topic should be 2-4 words maximum
- Version is always `-v{N}` suffix before `.md`

## Prompt Body Rules

1. Lead with the instruction. No preamble, no context-setting paragraph.
2. Use imperative mood ("Review the code") except for role prompts which start with "You are..."
3. For role prompts, follow the persona declaration immediately with constraints.
4. Specify output format explicitly when it matters.
5. Use delimiters (triple quotes, XML tags, or markdown headers) to separate sections.
6. Prefer positive instructions ("do X") over negative ("don't do Y").
7. If a negative rule is needed, pair it with what to do instead.
8. Use chain-of-thought triggers ("Think step by step, then give the final answer") inline when a task requires multi-step reasoning. These are techniques, not separate files.

## Forbidden Patterns

- Motivational language ("Let's create amazing results!")
- Filler sections ("## Future Work: TBD")
- Emoji
- Em dashes
- Duplicate instructions across files unless structurally necessary
- Vague qualifiers ("try to be helpful", "do your best")
- Single-sentence prompts as standalone files; if it fits in one line, reference it in this guide instead
