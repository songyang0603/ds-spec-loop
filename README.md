# ds-spec-loop

**English** | [简体中文](README.zh-CN.md)

> A repository-native Agent Skill that keeps decisions, code, tests, and current documentation aligned throughout non-trivial AI-assisted development.

`ds-spec-loop` turns Spec programming into a durable engineering practice for coding agents—not a large plan written before coding. It adapts patterns observable in the public [DeepSeek Harness](https://github.com/deepseek-ai/deepseek-harness) repository and Git history: repository instructions, current-state documentation, lifecycle-managed decision notes, complete composition-path implementation, falsifiable acceptance criteria backed by direct evidence, and deliberate convergence of every authority surface affected by the change.

It is designed to make vibe coding more reliable without making every edit ceremonial. The Agent first reconstructs what the repository already says, establishes the decision that owns the change, implements through the real assembled path, and finishes only when the Spec, implementation, evidence, and current truth agree.

## Quick start

Install with the community cross-agent [`skills`](https://skills.sh/) CLI:

```bash
npx skills add songyang0603/ds-spec-loop
```

Then ask your coding agent:

```text
Use $ds-spec-loop to design and implement this non-trivial change.
Recover the repository's existing authority first, establish or update the owning
decision, implement the complete assembled path, and converge the spec, code,
tests, evidence, and current documentation before claiming completion.
```

Explicit invocation depends on the host:

| Host | Invoke |
| --- | --- |
| Codex | `$ds-spec-loop` |
| Claude Code | `/ds-spec-loop` |
| GitHub Copilot CLI | `/ds-spec-loop` |
| Other compatible agents | Use the host's documented Skill invocation or mention `ds-spec-loop` by name |

## Why use it

Fast AI-generated patches often fail outside the edited file. A change can look complete while it:

- solves the prompt but violates the repository's actual contract;
- implements a leaf module without reaching its provider, loader, consumer, persistence, or user-facing path;
- leaves an architecture document or durable rationale stale;
- duplicates an existing decision or repeats an alternative the repository already rejected;
- deletes source while leaving exports, registrations, manifests, snapshots, docs, or durable formats behind;
- treats a passing formatter or unit test as proof of end-to-end behavior.

`ds-spec-loop` gives the Agent a repository-wide definition of completion. It also makes later Agent sessions more effective: they can recover current truth and past reasoning from maintained repository artifacts instead of rediscovering intent from scratch.

## The method

The Spec is a distributed authority system, not a single Markdown document:

```text
repository instructions + current-state docs + decision records
                              ↕
       source + types + package/config/composition topology
                              ↕
 tests + snapshots + runnable paths + generated artifacts + gates
```

The authority system keeps six coupled responsibilities coherent:

- **Reconstruct repository authority.** Read governing instructions, current-state docs, existing decisions, public contracts, entry points, assembly paths, tests, generated outputs, and relevant history before preferring an implementation.
- **Establish the owning decision.** Reuse the record that already owns the decision or create one when the change alters behavior, contracts, architecture, process, test strategy, durable formats, or rationale. Keep one owning record per durable decision rather than duplicating it.
- **Make acceptance falsifiable.** For every acceptance statement, identify the observable result, where it can fail, the evidence that could disprove it, and the exact command or runtime path that produces that evidence.
- **Change the complete assembled path.** Trace and update definition, provider, registration or loader, consumer, persistence, and model or user exposure wherever they exist—not only the leaf implementation.
- **Review against the real consumer.** Re-read the request and decision independently of the patch, test positive and negative guarantees, and distinguish executed checks from inspection or unverified boundaries.
- **Converge lifecycle and current truth.** Move a proposal to `implemented` only after the implementation and evidence agree; rewrite it as present truth, update current documentation, and preserve rejected or superseded reasoning without treating history as current authority.

Decision records have an explicit lifecycle:

```text
proposed ──→ implemented ──→ archived
    └──────→ rejected
```

Archive an implemented record only after it no longer owns active rationale. When a decision changes, create a cross-linked successor and mark the prior record as superseded; do not rewrite the old record into its opposite.

The Skill uses six decision classes—`feature`, `bug-fix`, `simplification`, `architecture`, `process`, and `testing`—because each has different likely failure surfaces and evidence needs. It adopts a repository's existing ADR/RFC/Spec conventions when they already provide equivalent ownership and lifecycle semantics.

Purely mechanical local edits are exempt when they change no behavior, contract, structure, process, test strategy, durable format, or lasting rationale. Diff size and file count are not the deciding factors.

## What it can do

| Task | What the Agent does |
| --- | --- |
| Design a change | Investigates the repository and writes or repairs the owning proposed decision before implementation |
| Implement a proposal | Continues an existing proposal through the real composition path, direct evidence, and lifecycle convergence |
| Fix a bug | Captures the violated contract, root cause, regression surface, and evidence that the failure is actually closed |
| Simplify or delete | Proves the surface and its consumers, specifies complete absence, and removes stale topology and documentation |
| Review or verify | Performs a read-only check for disagreement among active decisions, source, tests, generated artifacts, and current docs |
| Adopt Spec programming | Maps the method onto the repository's current conventions instead of imposing a parallel documentation system |

The requested boundary remains binding: a verify-only task stays read-only, and a specify-only task does not silently become implementation.

## Installation

The [Agent Skills specification](https://agentskills.io/specification) standardizes the portable `SKILL.md` package. Discovery directories and invocation syntax remain host-specific.

### Cross-agent installer

The quickest option for Codex, Claude Code, GitHub Copilot, Cursor, Gemini CLI, OpenCode, Windsurf, and other supported agents is:

```bash
npx skills add songyang0603/ds-spec-loop
```

The installer discovers `skills/ds-spec-loop/SKILL.md` and lets you choose the target Agent and scope.

### GitHub CLI

GitHub CLI also provides a preview Agent Skills installer:

```bash
gh skill install songyang0603/ds-spec-loop ds-spec-loop --agent codex --scope user
```

Replace `codex` with `claude-code` or `github-copilot` for those hosts.

### Manual installation

Clone this repository, then copy `skills/ds-spec-loop` into a discovery directory supported by your Agent:

| Host | User scope | Repository scope |
| --- | --- | --- |
| Codex | `~/.agents/skills/ds-spec-loop` | `.agents/skills/ds-spec-loop` |
| Claude Code | `~/.claude/skills/ds-spec-loop` | `.claude/skills/ds-spec-loop` |
| GitHub Copilot CLI | `~/.copilot/skills/ds-spec-loop` or `~/.agents/skills/ds-spec-loop` | `.github/skills/ds-spec-loop` or `.agents/skills/ds-spec-loop` |

Codex and Claude Code also document support for linked Skill directories. For GitHub Copilot CLI, use a copy or its documented directory-registration mechanism rather than assuming direct symlink discovery. See the official [Codex](https://developers.openai.com/codex/skills/), [Claude Code](https://code.claude.com/docs/en/skills), and [GitHub Copilot CLI](https://docs.github.com/en/copilot/how-tos/copilot-cli/customize-copilot/add-skills) documentation for current behavior. Restart or reload the Agent if a newly created top-level Skill directory is not detected.

For another Agent Skills-compatible host, install the portable `skills/ds-spec-loop` directory using that product's documented discovery mechanism. The package intentionally keeps portable instructions in `SKILL.md` and `references/`; `agents/openai.yaml` only supplies optional Codex UI metadata.

## Usage recipes

### Complete implementation

```text
Use $ds-spec-loop to design and implement this change. Begin from the repository's
own instructions, current docs, decisions, source, and tests. Do not claim completion
until every acceptance criterion has direct evidence or an explicit verification boundary.
```

### Specify only

```text
Use $ds-spec-loop to investigate this change and write the owning proposed Agent Note.
Do not implement it. Make the problem solution-independent and map every acceptance
criterion to evidence that could falsify it.
```

### Continue an existing proposal

```text
Use $ds-spec-loop to continue the existing proposed decision through implementation,
assembled-path verification, documentation updates, and lifecycle convergence.
```

### Verify drift without editing

```text
Use $ds-spec-loop to verify whether active decisions, source, public contracts,
generated references, tests, and user-facing docs agree. Do not modify files.
```

### Simplify or remove a surface

```text
Use $ds-spec-loop to determine whether this surface earns its maintenance cost through
real consumers. If repository evidence supports removal, specify and verify complete
absence across source, registrations, exports, manifests, tests, and documentation.
```

For Claude Code or GitHub Copilot CLI, replace `$ds-spec-loop` with `/ds-spec-loop`.

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

## Provenance and independence

This is an independent, community-authored adaptation of engineering patterns observable in the public, MIT-licensed DeepSeek Harness repository and its Git history. It is not an official DeepSeek project and is not endorsed by DeepSeek. The Skill is a new reusable formulation of those patterns and does not redistribute DeepSeek Harness source code.

See [NOTICE](NOTICE) for attribution and [LICENSE](LICENSE) for this repository's license.

## Contributing

Issues and pull requests are welcome. The most useful reports include a real repository task, the Agent and version used, the invocation, the observed behavior, the expected behavior, and the repository evidence showing the gap.
