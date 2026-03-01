# Lessons Learned

Operational observations from building and using this prompt library.

## Prompt Design

- **Merging beats splitting.** Three focused system prompts outperform eight granular ones. Agentic behavior rules (persistence, planning, tool-use, verification) belong in one prompt, not four separate files.
- **One-liners are not files.** "Let's think step-by-step" and "Use a friendly tone" are techniques to reference in the style guide, not standalone prompt files.
- **Niche prompts decay.** Domain-specific prompts (DTC email sequences, React form generators) go stale fast. Keep them in examples if needed, not in the core library.
- **Positive over negative.** "Do X instead" outperforms "Don't do Y" in prompt instructions. When a negative rule is needed, always pair it with the desired alternative.

## Repo Structure

- **Boundaries prevent rot.** Without clear rules on what goes in prompts/ vs workflows/ vs examples/, files migrate to the wrong place within weeks.
- **Frontmatter should be minimal.** A 15-field schema creates friction that discourages contribution. Start with 7 required fields; add optional fields per-file when needed.
- **Version in the filename.** `v1` in the name makes it grep-able and obvious which version is current without opening the file.
- **Kill placeholders early.** A .gitkeep file should be replaced the moment a real file lands in the directory. Empty directories with no plan are noise.
- **Define it once, reference it everywhere.** Decision rules, naming conventions, and versioning rules should have one canonical home in standards. Other docs should reference, not copy. Duplication drifts fast.

## Operational Maturity

- **Composition rules are as important as the prompts.** A library of good prompts is useless if combining them produces contradictions. Define valid combinations, precedence, and anti-patterns early.
- **Lifecycle tracking forces honesty.** Labeling prompts as draft/stable makes visible what is validated and what is assumed. Without it, every prompt looks equally reliable and none are.
- **Regression cases make the framework real.** A testing framework with no test cases is a spec, not a system. Even 5 real cases is better than a perfect README describing cases that do not exist.
