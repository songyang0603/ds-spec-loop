# ds-spec-loop

A reusable Agent Skill for complete, repository-native, spec-anchored development.

`ds-spec-loop` distills the public engineering method visible in [DeepSeek Harness](https://github.com/deepseek-ai/deepseek-harness): long-lived repository instructions, current-state architecture docs, lifecycle-managed Agent Notes, implementation through the real composition path, executable acceptance evidence, mechanical gates, and deliberate convergence of code and documentation.

It is not a “write a spec, then code” prompt. The spec is a distributed authority system:

```text
repository instructions + current docs + decision notes
                    ↕
source + types + package/config topology
                    ↕
tests + snapshots + runnable paths + mechanical gates
```

## What it supports

- feature, bug-fix, simplification, architecture, process, and testing decisions;
- proposed → implemented or proposed → rejected lifecycle;
- supersession, consolidation, and archive discipline;
- one owning decision per non-trivial change;
- observable acceptance criteria mapped to falsifying evidence;
- full assembled-path implementation, not leaf-module completion;
- read-only spec/source/docs drift verification;
- adoption in repositories that already use ADRs/RFCs or have no spec convention.

The Skill exempts only purely mechanical local edits that change no behavior, contract, structure, process, test strategy, or durable rationale.

## Repository contents

```text
skills/ds-spec-loop/
├── SKILL.md
├── agents/openai.yaml
└── references/
    ├── acceptance-and-evidence.md
    ├── adoption.md
    ├── agent-note-lifecycle.md
    ├── decision-classes.md
    ├── documentation-discipline.md
    ├── simplification.md
    ├── system-of-authority.md
    └── templates.md
```

The portable core is `skills/ds-spec-loop/SKILL.md` plus `references/`. `agents/openai.yaml` only supplies Codex UI metadata; agents that do not use it can ignore it.

## Install

The [Agent Skills specification](https://agentskills.io/specification) standardizes the skill package, but each agent chooses its own discovery directory.

### Codex

Ask Codex to install the skill from:

```text
https://github.com/songyang0603/ds-spec-loop/tree/main/skills/ds-spec-loop
```

Or clone the repository and link/copy `skills/ds-spec-loop` into:

```text
~/.agents/skills/ds-spec-loop
```

Codex also discovers repository-scoped skills under `.agents/skills/`. See the official [OpenAI Build skills documentation](https://developers.openai.com/codex/skills/). Restart Codex after installation if the skill does not appear immediately.

### Claude Code

Link or copy the portable skill directory into a personal or project skill location:

```text
~/.claude/skills/ds-spec-loop
.claude/skills/ds-spec-loop
```

See the official [Claude Code skills documentation](https://code.claude.com/docs/en/slash-commands).

### GitHub Copilot CLI

Link or copy the portable skill directory into:

```text
~/.copilot/skills/ds-spec-loop
.github/skills/ds-spec-loop
```

GitHub Copilot CLI also recognizes `.agents/skills/`; see the official [GitHub Copilot agent skills documentation](https://docs.github.com/en/copilot/how-tos/copilot-cli/customize-copilot/add-skills).

### Other Agent Skills-compatible agents

Point the agent's skill discovery mechanism at `skills/ds-spec-loop`, or copy that directory into its documented skill location. The `SKILL.md` frontmatter intentionally uses only the portable `name` and `description` fields.

The portable package does not guarantee identical implicit triggering, shell/Git access, permissions, or tool names across hosts. Those remain product-specific.

## Use

Explicit invocation:

```text
Use $ds-spec-loop to design and implement this non-trivial change. Work from the repository's own instructions, current docs, decision notes, source, and tests. Stop only when every claimed acceptance criterion has direct evidence or an explicit verification boundary.
```

Specify only:

```text
Use $ds-spec-loop to write the owning proposed Agent Note for this change. Investigate the repository and history, but do not implement it.
```

Continue an existing proposal:

```text
Use $ds-spec-loop to continue the existing proposed spec through implementation, executable evidence, and lifecycle convergence.
```

Verify only:

```text
Use $ds-spec-loop to verify whether the active spec, source, generated references, tests, and user-facing docs agree. Do not modify files.
```

Simplify:

```text
Use $ds-spec-loop to determine whether this surface earns its maintenance cost through real consumers. Remove or narrow it only if the repository evidence supports that decision, and specify complete absence.
```

The Skill preserves the requested boundary: a verify-only task stays read-only, and a specify-only task does not silently become implementation.

## Why there is no bundled validator or synthetic eval suite

The method requires mechanical gates, but those gates must encode the host repository's real paths, lifecycle rules, generated artifacts, package topology, and CI commands. A generic format validator would prove headings and statuses while risking false confidence about semantic correctness.

For v1:

- the Skill package is checked with the official Skill validator during development;
- repository-specific mechanical rules are added in the target repository when they are important and decidable;
- fresh-agent forward tests are development evidence, not shipped runtime files;
- no test harness, golden output, synthetic repository, or copied validator is included here.

A small public validator becomes worthwhile only after real users repeatedly encounter the same mechanically decidable error. It should remain read-only, repository-configurable, and explicitly unable to judge semantic quality.

## Provenance and independence

This is an independent community project informed by study of the public, MIT-licensed DeepSeek Harness repository. It is not an official DeepSeek project and is not endorsed by DeepSeek. The Skill is a new reusable formulation of the method; it does not redistribute DeepSeek Harness source code.

See [NOTICE](NOTICE) for attribution and [LICENSE](LICENSE) for this repository's license.

## Contributing

Open an issue with a real repository task and the behavior that failed. Prefer evidence from an actual agent run over adding speculative phases, templates, or gates. Add automation only for a repeated, mechanically decidable failure.

Chinese documentation: [README.zh-CN.md](README.zh-CN.md)
