# Prompt Composition Rules

How to combine prompts from this library. The wrong combination produces contradictions, redundancy, or behavior that neither prompt intended.

## Layer Responsibilities

| Layer | Responsibility | Scope |
|-------|---------------|-------|
| System | Session-wide behavior: safety, output mode, tool-use policy, execution protocol | Everything the model does |
| Role | Persona identity and operating constraints: expertise, method, tone, priorities | How the model approaches work |
| Task | Specific job with defined inputs and outputs | One unit of work |
| Template | Structural scaffold with placeholders for reuse | Format, not content or behavior |

## Valid Combinations

| Combination | When to Use |
|-------------|-------------|
| System + Task | Most common. Set behavior rules, then assign work. |
| System + Role + Task | Task needs both session rules and a specific persona. |
| System + Template (filled) | Behavior rules plus a structured request. |
| Role + Task | Platform handles behavior rules; you only need persona + work. |
| Template (filled) alone | Quick structured request with no special behavior or persona needs. |

## Invalid Combinations

| Combination | Why It Fails |
|-------------|-------------|
| Two system prompts | Conflicting global rules. Merge into one or pick the more specific one. |
| Two role prompts | Contradictory personas. The model cannot be two people. Pick one or create a combined role. |
| System + Role with conflicting output formats | Both define output structure but they disagree. The model blends them unpredictably. Resolve before composing. |
| Template used as a system prompt | Templates define structure for a single request, not session-wide behavior. |
| Task used as a role | A task defines what to do once. A role defines who to be. |

## Precedence Rules

When instructions conflict across layers:

1. **System wins on behavior.** Safety rules, output mode (JSON only, no markdown), tool-use policy, execution protocol. Non-negotiable.
2. **Role wins on persona.** How to approach work, what to prioritize, what tone to use. System prompts should not override persona unless it is a safety or format constraint.
3. **Task wins on specifics.** What to produce, which inputs to use, what format this particular output takes. A task requesting a table overrides a role that usually outputs prose.
4. **Templates define structure only.** They do not set behavior or persona. If a template contradicts a system or role instruction, the system/role wins.

## When to Merge Instead of Stack

Merge two prompts into one when:

- They address the same concern from different angles (e.g., two system prompts about output formatting).
- Stacking them would require the model to resolve contradictions.
- The combined prompt is shorter than both originals (a sign of redundancy).

Do not merge when:

- The prompts serve genuinely different layers (system vs role vs task).
- One is reusable across many contexts and merging would make it context-specific.

## When a Task Prompt Is Too Specific

Move a task prompt to `examples/` when:

- It hardcodes a specific domain, product, or dataset that limits reuse.
- It only works with a particular model or API configuration.
- It demonstrates a template rather than serving as a reusable instruction.

A task prompt stays in `prompts/tasks/` only if different people on different projects can use it by swapping input variables.

## Research Prompt Composition

`sys-research-citations-v1` and `role-research-analyst-v1` have distinct, non-overlapping responsibilities:

- **System prompt** owns citation discipline, source verification, and uncertainty handling. It does not define output structure.
- **Role prompt** owns analytical method, synthesis style, and output format.

When composing them: the role's output format defines the structure; the system's citation rules apply as behavioral constraints within that structure.

Do not use `sys-research-citations-v1` as a role. It is a behavior mode, not a persona.

## Anti-Patterns

1. **Copy-paste stacking.** Pasting multiple prompt files end-to-end without checking for contradictions. Always review the combined prompt for conflicting instructions.
2. **Template as system prompt.** Using tpl-rctfc or tpl-xml-sections as the system message. Templates are for individual requests.
3. **Role drift.** A role prompt that gradually accumulates task-specific instructions. If a role file has more than 2-3 task details, extract them into a separate task prompt.
4. **Invisible precedence.** Combining prompts without documenting which prompt wins on which concern. Note the expected precedence in your workflow or configuration.
5. **Over-stacking.** Using system + role + task + template simultaneously. Three layers is the practical maximum. Beyond that, instructions compete for model attention and earlier ones lose weight.
