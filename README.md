# ds-spec-loop

**English** | [简体中文](README.zh-CN.md)

> A reusable Agent Skill that applies Spec programming patterns observed in DeepSeek Harness to software development in other repositories.

`ds-spec-loop` helps coding agents keep requirements, decisions, implementation, tests, and documentation consistent while building features, fixing bugs, changing architecture or interfaces, improving tests and development processes, or removing code.

Here, Spec programming does not mean writing a long plan before coding. It means using the repository itself as the source of truth: instructions describe constraints, current documentation describes the system as it exists, decision records preserve why choices were made, and code plus tests provide executable evidence.

## 🧭 Method source

This Skill is an independent community project based on patterns observable in the public [DeepSeek Harness](https://github.com/deepseek-ai/deepseek-harness) repository and its Git history. Those patterns include:

- repository-level and directory-level instructions for agents;
- current-state architecture and package documentation;
- decision records with `proposed`, `implemented`, `rejected`, `superseded`, and `archived` states;
- implementation across the actual integration and runtime path;
- acceptance criteria tied to direct evidence;
- updates to code, tests, generated artifacts, and documentation in the same change.

`ds-spec-loop` turns these observed practices into a portable Agent Skill. It is not an official DeepSeek project, is not endorsed by DeepSeek, and does not redistribute DeepSeek Harness source code.

## ✨ What the Skill does

| Capability | What the Agent does |
| --- | --- |
| Understand the repository before editing | Reads applicable instructions, current docs, existing decisions, relevant source, tests, generated files, and Git history when needed |
| Maintain decision records | Creates or updates the record that owns a decision, and keeps its lifecycle accurate as work is implemented, rejected, superseded, or archived |
| Define verifiable acceptance criteria | Connects each requirement to observable behavior, likely failure points, and evidence that can confirm or disprove completion |
| Implement the complete path | Follows the change through definitions, providers, registration or loading, consumers, persistence, and user- or model-facing behavior where applicable |
| Keep the repository consistent | Updates affected code, public contracts, tests, snapshots, generated artifacts, current documentation, and decision rationale together |
| Support simplification and deletion | Checks real consumers and removes obsolete registrations, exports, files, tests, documentation, and compatibility surfaces—not only the main source file |
| Review without modifying | Can perform a read-only comparison of active decisions, source, tests, generated artifacts, and current documentation |
| Fit existing conventions | Reuses a repository's ADR, RFC, design-doc, or Spec system instead of creating a competing documentation structure |

Use it for feature development, bug fixes, API or configuration changes, architecture changes, test-strategy changes, development-process changes, code removal, or Spec-to-code review. A spelling correction, formatting-only edit, or other local mechanical change normally does not need this Skill.

## 🚀 Quick start

Install with the community-maintained cross-agent [`skills`](https://skills.sh/) CLI:

```bash
npx skills add songyang0603/ds-spec-loop
```

Then invoke it in Codex:

```text
Use $ds-spec-loop to implement this feature.
Before editing, inspect the repository's instructions, current documentation,
existing decisions, relevant source, tests, and actual integration path.
Keep the decision record, implementation, evidence, and documentation consistent.
```

Explicit invocation depends on the host:

| Host | Invoke |
| --- | --- |
| Codex | `$ds-spec-loop` |
| Claude Code | `/ds-spec-loop` |
| GitHub Copilot CLI | `/ds-spec-loop` |
| Other compatible agents | Use the host's documented Skill invocation or mention `ds-spec-loop` by name |

### Common usage

Write a Spec without implementing it:

```text
Use $ds-spec-loop to investigate this change and write the proposed decision record.
Do not implement it. Describe the problem independently of the preferred solution,
compare real alternatives, and connect acceptance criteria to direct evidence.
```

Continue an existing proposal:

```text
Use $ds-spec-loop to continue the existing proposed decision through implementation,
testing, documentation updates, and the correct lifecycle transition.
```

Review consistency without changing files:

```text
Use $ds-spec-loop to check whether active decisions, source, public contracts,
tests, generated artifacts, and current documentation agree. Do not modify files.
```

Simplify or remove code:

```text
Use $ds-spec-loop to investigate the real consumers of this code and plan its removal.
If removal is justified, update the full integration path and verify that obsolete files,
registrations, exports, tests, and documentation no longer remain.
```

The requested task boundary remains binding: a review-only task stays read-only, and a Spec-only task does not silently become implementation. For Claude Code or GitHub Copilot CLI, replace `$ds-spec-loop` with `/ds-spec-loop`.

## 🧩 How it works

The Skill treats the Spec as a set of connected repository records:

```text
instructions + current documentation + decision records
                           ↕
       source + types + configuration + integration path
                           ↕
       tests + runnable behavior + generated artifacts
```

- **Current documentation** explains what the repository does now.
- **Decision records** explain why a decision was proposed, accepted, rejected, replaced, or retained.
- **Source and public contracts** implement the decision.
- **Tests and runnable paths** provide evidence for observable behavior.
- **Repository-specific checks** enforce facts that can be decided mechanically.

The Agent updates only the records affected by the task. It does not assume that a format check proves semantic correctness, or that changing one module means the feature works through the complete system.

## 📦 Installation

The [Agent Skills specification](https://agentskills.io/specification) standardizes the portable `SKILL.md` package. Discovery directories and invocation syntax remain host-specific.

### Cross-agent installer

```bash
npx skills add songyang0603/ds-spec-loop
```

The installer discovers `skills/ds-spec-loop/SKILL.md` and lets you select the target Agent and installation scope.

### GitHub CLI

GitHub CLI also provides a preview Agent Skills installer:

```bash
gh skill install songyang0603/ds-spec-loop ds-spec-loop --agent codex --scope user
```

Replace `codex` with `claude-code` or `github-copilot` for those hosts.

### Manual installation

Clone the repository, then copy `skills/ds-spec-loop` into a supported discovery directory:

| Host | User scope | Repository scope |
| --- | --- | --- |
| Codex | `~/.agents/skills/ds-spec-loop` | `.agents/skills/ds-spec-loop` |
| Claude Code | `~/.claude/skills/ds-spec-loop` | `.claude/skills/ds-spec-loop` |
| GitHub Copilot CLI | `~/.copilot/skills/ds-spec-loop` or `~/.agents/skills/ds-spec-loop` | `.github/skills/ds-spec-loop` or `.agents/skills/ds-spec-loop` |

Codex and Claude Code also document support for linked Skill directories. For GitHub Copilot CLI, use a copy or its documented directory-registration mechanism. See the official [Codex](https://developers.openai.com/codex/skills/), [Claude Code](https://code.claude.com/docs/en/skills), and [GitHub Copilot CLI](https://docs.github.com/en/copilot/how-tos/copilot-cli/customize-copilot/add-skills) documentation for current behavior.

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

Agents load the compact `SKILL.md` entrypoint first and read only the reference files needed for the current task.

## 💬 Contributing

Ideas, issues, and pull requests are welcome. If something does not work well in your repository, open an Issue and tell us what you were trying to do, which Agent you used, and what happened. That is enough to start the conversation.

See [NOTICE](NOTICE) for attribution and [LICENSE](LICENSE) for this repository's license.
