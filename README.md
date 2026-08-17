# ds-spec-loop

**English** | [简体中文](README.zh-CN.md)

> A general Spec programming Skill for coding agents.

`ds-spec-loop` helps coding agents keep requirements, decisions, implementation, tests, and documentation consistent while building features, fixing bugs, changing architecture or interfaces, improving tests and development processes, or removing code.

Here, Spec programming does not mean writing a long plan before coding. It means using the repository itself as the source of truth: instructions describe constraints, current documentation describes the system as it exists, decision records preserve why choices were made, and code plus tests provide executable evidence.

## Method origin

This independent community project was developed from analysis of Spec and decision practices visible in the public [DeepSeek Harness](https://github.com/deepseek-ai/deepseek-harness) repository and Git history.

The runtime Skill uses general terms and does not require that repository's directories, framework, or test commands. This project is not official, is not affiliated with or endorsed by DeepSeek, and does not redistribute DeepSeek Harness source code. See [NOTICE](NOTICE).

## 🚀 Install and use

### Community Skills CLI

The community-maintained [`skills`](https://skills.sh/) installer requires Node.js and lets you choose the target coding agent and installation scope:

```bash
npx skills add songyang0603/ds-spec-loop
```

### GitHub CLI

```bash
gh skill install songyang0603/ds-spec-loop ds-spec-loop --agent codex --scope user
```

Replace `codex` with `claude-code` or `github-copilot` when appropriate.

### Manual installation

Clone or download this repository, then copy the entire `skills/ds-spec-loop` directory:

| Host | User scope | Repository scope |
|---|---|---|
| Codex | `~/.agents/skills/ds-spec-loop` | `.agents/skills/ds-spec-loop` |
| Claude Code | `~/.claude/skills/ds-spec-loop` | `.claude/skills/ds-spec-loop` |
| GitHub Copilot | `~/.copilot/skills/ds-spec-loop` or `~/.agents/skills/ds-spec-loop` | `.github/skills/ds-spec-loop`, `.claude/skills/ds-spec-loop`, or `.agents/skills/ds-spec-loop` |

See the current official documentation for [Codex](https://learn.chatgpt.com/docs/build-skills), [Claude Code](https://code.claude.com/docs/en/skills), and [GitHub Copilot](https://docs.github.com/en/copilot/how-tos/copilot-cli/customize-copilot/add-skills).

### Invoke the Skill

| Host | Command |
|---|---|
| Codex | `$ds-spec-loop` |
| Claude Code | `/ds-spec-loop` |
| GitHub Copilot CLI | `/ds-spec-loop` |

Examples below use Codex syntax. Replace `$ds-spec-loop` with `/ds-spec-loop` in Claude Code or GitHub Copilot CLI.

Implement a change:

```text
Use $ds-spec-loop to implement this change. Reuse the repository's existing
decision, documentation, test, and CI conventions, and keep them consistent.
```

Write a proposal without implementing it:

```text
Use $ds-spec-loop to investigate this change and write its proposal.
Do not implement it. Compare real alternatives and define direct checks.
```

Review without modifying:

```text
Use $ds-spec-loop to check whether proposals, decisions, code, tests,
generated files, and current documentation agree. Do not modify files.
```

The requested task boundary remains binding: review-only stays read-only, and proposal-only does not silently become implementation.

## ✨ What it does

| Feature | What the agent does |
|---|---|
| Understand existing conventions | Reads applicable instructions, proposals, decisions, current docs, source, tests, generated files, CI, and relevant Git history |
| Reuse one decision record | Updates the record already responsible for the change; creates a narrowly scoped record when none exists |
| Write testable acceptance criteria | States what should be observable, where it can fail, and which direct check can disprove completion |
| Trace the affected integration path | Checks the layers that actually connect the change to its caller, runtime, persistence, or visible result |
| Handle changed requirements | Revises an unfinished proposal in place; creates a replacement record only after a delivered decision is reversed |
| Keep the repository consistent | Updates affected decisions, code, tests, generated files, public contracts, and current docs in the same pull request or linked changes |
| Remove code completely | Checks real consumers and removes obsolete code, registration, exports, config, tests, docs, and compatibility behavior |

The core rule is:

> Every non-mechanical change creates or updates one decision record responsible for that change.

A spelling correction, formatting-only edit, or other local mechanical change is exempt only when it changes no behavior, contract, structure, process, test strategy, stored-data format, or rationale.

## 🧭 How it works

The Skill does not impose one directory layout. It first finds which existing files already perform each job.

| Responsibility | Common repository forms |
|---|---|
| Working rules | `AGENTS.md`, `CLAUDE.md`, Copilot instructions |
| Unfinished decision | Spec, RFC, proposal, design doc, draft ADR |
| Current decision | ADR, decision record, implemented design, shipped RFC |
| Current system description | architecture docs, README, API or package docs |
| Focused checks | `pytest`, `cargo test`, `go test`, `pnpm test`, real CLI/UI/API checks |
| Full checks | GitHub Actions, Makefile, pre-commit, repository scripts |

A Python project is not told to run `pnpm test`. A repository that already uses ADRs is not told to create another decision directory.

If no equivalent convention exists, the Skill proposes only a small fallback: repository instructions, current architecture documentation, and a directory such as `docs/decisions/`. It does not create class folders, archives, indexes, validators, translations, or checksum files without a demonstrated need.

### Decision lifecycle

The method preserves three meanings without forcing particular status words:

| Stage | Meaning |
|---|---|
| Working | not delivered yet, partly implemented, or still changing |
| Current | implementation, direct checks, and current documentation agree |
| Declined | considered but not adopted; retained only while the reason remains useful |

An `accepted` ADR does not always mean the code has shipped. A decision becomes Current only when implementation, direct checks, and current documentation agree.

Replacement is a relationship between decisions:

- change an unfinished proposal directly;
- create a new cross-linked record when a delivered decision is reversed;
- keep both decisions Current when only part of the earlier decision was replaced;
- consolidate an old decision only after the new record preserves its unique rationale, consequences, verification requirements, and reintroduction conditions.

## Repository contents

```text
skills/ds-spec-loop/
├── SKILL.md
├── agents/openai.yaml
└── references/
    ├── acceptance-and-evidence.md
    ├── adoption.md
    ├── decision-classes.md
    ├── decision-record-lifecycle.md
    ├── documentation-discipline.md
    ├── requirement-change.md
    ├── simplification.md
    ├── system-of-authority.md
    └── templates.md
```

`SKILL.md` contains the portable core. References load only when the task needs them. `agents/openai.yaml` contains optional Codex-specific metadata, including the default invocation prompt.

## 📝 Update log

### v0.2 — 2026-08-17

Further generalized the Spec programming loop so it can be used in projects with different conventions. The Skill reuses each project's existing Specs, RFCs, ADRs, documentation, testing, and CI conventions, while strengthening rules for mid-development requirement changes, decision ownership, lifecycle transitions, partial replacement, and verification evidence. This update has passed cross-language scenario tests, structural validation, and independent review.

### v0.1 — 2026-08-15

Published the first open-source version, based on Spec programming patterns observed in the public DeepSeek Harness repository. It included the reusable Skill, English and Chinese documentation, and installation instructions for Codex, Claude Code, and GitHub Copilot.

## Contributing

Contributions are welcome. If you find a problem or have a suggestion, please open an Issue with enough context to understand or reproduce it; documentation improvements, usage examples, and focused pull requests are also appreciated.

See [LICENSE](LICENSE) for the project license.
