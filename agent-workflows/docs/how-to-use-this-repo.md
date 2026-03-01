# How to Use This Repo

Practical guide for using this prompt library in day-to-day work.

## Choosing a Prompt

1. Open `docs/prompt-catalog.md`.
2. Find the prompt whose "When to use" matches your task.
3. Prefer `stable` prompts. Use `draft` prompts when no stable alternative exists, but expect rougher edges.
4. Check the "Composes with" note before combining prompts.

If nothing in the catalog fits, do not create a new prompt file yet. Write an ad-hoc prompt inline, use a template (`tpl-rctfc-v1` or `tpl-xml-sections-v1`) as scaffolding, and see the earned entry rules below.

## Composing Prompts

Pick layers based on what your task needs:

| What you need | Layers to use |
|---------------|---------------|
| Autonomous coding session | sys-agentic-execution + role or task |
| Code review | sys-agentic-execution + role-code-reviewer |
| Research with citations | sys-research-citations + role-research-analyst |
| JSON pipeline output | sys-json-strict + task |
| Quick structured request | template alone |

Rules:

- One system prompt maximum. If you need two, merge them.
- One role prompt maximum. Do not stack personas.
- System wins on behavior. Role wins on persona. Task wins on specifics.
- Three layers is the practical maximum. See `standards/prompt-composition-rules.md` for details.

## Using Prompts in Cursor

**As system instructions in Cursor rules:**
Copy the prompt body (below the frontmatter) into a `.cursor/rules/*.mdc` file or an `AGENTS.md` file. Use the frontmatter's `tags` to decide which file patterns or directories the rule should apply to.

**As inline instructions in a chat session:**
Paste the prompt body into the chat as your first message or as context. For composed prompts, paste system first, then role, then task.

**As a reference during prompt writing:**
When writing a new ad-hoc prompt for a specific task, use the templates (`tpl-rctfc-v1`, `tpl-xml-sections-v1`) as structural starting points. Fill in the placeholders and send.

## When a Prompt Fails

When a prompt produces bad output:

1. **Record the failure.** Note the prompt used, the input, the bad output, and what you expected.
2. **Decide: prompt bug or coverage gap?**
   - If the prompt's instructions are wrong or ambiguous: edit the prompt. Update frontmatter. Commit with rationale.
   - If the prompt's instructions are correct but the scenario was not covered by regression cases: add a regression case under `examples/prompt-regression/<prompt-name>/`.
3. **If the fix changes output schema or behavior:** bump the version (`v1` to `v2`). See versioning rules in `standards/repo-rules.md`.
4. **If a stable prompt is edited:** re-run its regression cases to verify you did not break existing behavior.

Use `task-prompt-debugger-v1` for structured diagnosis when the root cause is not obvious.

## New Prompt vs Example vs Workflow

| You have... | It belongs in... |
|-------------|-----------------|
| A reusable instruction that works across projects by swapping variables | `prompts/` (system, role, task, or template) |
| A one-off instruction tied to a specific project, domain, or dataset | `examples/` as a demo or transcript |
| A multi-step process that requires tools, state, or approvals | `workflows/` |
| A filled-in template showing how a prompt was used | `examples/` |
| A test case for an existing prompt | `examples/prompt-regression/<prompt-name>/` |

When in doubt, put it in `examples/` first. Promote to `prompts/` only if it earns entry.

## Earned Entry: When to Add a New Prompt File

A new prompt file is only justified when **all** of the following are true:

1. **Repeated real use.** You have used this prompt (or a close variant) at least 3 times in real work. One-off instructions do not belong in the library.
2. **Real gap.** No existing prompt, template, or composition of existing prompts covers this need.
3. **Reusable behavior.** The prompt works across different projects and users by swapping input variables. If it only works for one context, it is an example.
4. **Regression-case potential.** You can write at least one meaningful test case for it. If you cannot define pass/fail checks, the prompt is too vague.
5. **Clean folder fit.** The prompt clearly belongs in exactly one folder (`system/`, `roles/`, `tasks/`, or `templates/`). If it straddles two, it needs to be split or restructured first.

If any condition is not met, keep the prompt as an ad-hoc instruction or an example. Do not add it to the library.

New prompt files always enter as `draft`. Promotion to `stable` requires meeting the full gate in `standards/repo-rules.md`.
