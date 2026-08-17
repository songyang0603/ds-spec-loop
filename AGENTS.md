# Repository instructions

This repository publishes one portable, repository-native Spec programming Skill.

## Authority

- `skills/ds-spec-loop/SKILL.md` owns the agent-facing core loop.
- `skills/ds-spec-loop/references/` owns detailed protocols and templates.
- `README.md` and `README.zh-CN.md` own public installation and usage guidance and remain equivalent in meaning.
- `docs/decisions/` owns this repository's working proposals and accepted decision rationale.
- `NOTICE` owns method attribution and independence from upstream projects.

## Working rules

- Every non-mechanical change adds or updates one owning decision record in the same bounded change. Search for an existing owner before creating another.
- Reuse the repository's current terminology and tools. Do not create a second Spec, ADR, documentation, test, or CI system when an existing one owns the responsibility.
- A working proposal may change before delivery. A stable accepted decision is replaced by a new cross-linked decision record rather than rewritten as though it never existed.
- Supersession is a relationship, not a lifecycle status or required directory.
- Keep one canonical home per fact. Other files may summarize or link to the owner.
- Use the smallest direct checks that cover the changed claims. Development-only evaluation artifacts stay outside the repository.
- Do not modify `../deepseek-harness` while maintaining this project.
