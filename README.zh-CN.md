# ds-spec-loop

[English](README.md) | **简体中文**

> 一个供编程 Agent 使用的通用 Spec 编程 Skill。

`ds-spec-loop` 用于帮助编程 Agent 在开发功能、修复 Bug、调整架构或接口、改进测试与开发流程、简化或删除代码时，让需求、决策、实现、测试和文档保持一致。

这里的 Spec 编程不是“先写一份很长的计划再开始编码”，而是把仓库本身作为事实来源：仓库指令记录约束，当前文档描述系统现状，决策记录保留选择某种方案的原因，代码和测试提供可以运行或检查的证据。

## 方法来源

这个独立社区项目源于对 [DeepSeek Harness](https://github.com/deepseek-ai/deepseek-harness) 公开仓库和 Git 历史中 Spec 与决策方法的分析。

运行时 Skill 使用通用术语，不要求复制该仓库的目录、框架或测试命令。本项目不是 DeepSeek 官方项目，与 DeepSeek 没有隶属或背书关系，也不分发 DeepSeek Harness 源代码。详见 [NOTICE](NOTICE)。

## 🚀 安装与使用

### Community Skills CLI

社区维护的 [`skills`](https://skills.sh/) 安装器需要 Node.js，并会让你选择目标编程 Agent 和安装范围：

```bash
npx skills add songyang0603/ds-spec-loop
```

### GitHub CLI

```bash
gh skill install songyang0603/ds-spec-loop ds-spec-loop --agent codex --scope user
```

按需将 `codex` 替换为 `claude-code` 或 `github-copilot`。

### 手动安装

Clone 或下载本仓库，然后复制完整的 `skills/ds-spec-loop` 目录：

| 宿主 | 用户级目录 | 仓库级目录 |
|---|---|---|
| Codex | `~/.agents/skills/ds-spec-loop` | `.agents/skills/ds-spec-loop` |
| Claude Code | `~/.claude/skills/ds-spec-loop` | `.claude/skills/ds-spec-loop` |
| GitHub Copilot | `~/.copilot/skills/ds-spec-loop` 或 `~/.agents/skills/ds-spec-loop` | `.github/skills/ds-spec-loop`、`.claude/skills/ds-spec-loop` 或 `.agents/skills/ds-spec-loop` |

最新行为请参考 [Codex](https://learn.chatgpt.com/docs/build-skills)、[Claude Code](https://code.claude.com/docs/en/skills) 和 [GitHub Copilot](https://docs.github.com/en/copilot/how-tos/copilot-cli/customize-copilot/add-skills) 官方文档。

### 调用 Skill

| 宿主 | 命令 |
|---|---|
| Codex | `$ds-spec-loop` |
| Claude Code | `/ds-spec-loop` |
| GitHub Copilot CLI | `/ds-spec-loop` |

下面的示例使用 Codex 语法。在 Claude Code 或 GitHub Copilot CLI 中，请把 `$ds-spec-loop` 替换为 `/ds-spec-loop`。

实现一个变更：

```text
使用 $ds-spec-loop 实现这个变更。
复用仓库已有的决策、文档、测试和 CI 规范，并保持它们一致。
```

只写工作提案，不实现：

```text
使用 $ds-spec-loop 调查这个变更并编写工作提案，不要实现。
比较真实可行的替代方案，并为每项验收条件注明直接检查方式。
```

只读检查：

```text
使用 $ds-spec-loop 检查提案、决策、代码、测试、生成文件和当前文档
是否一致。不要修改文件。
```

用户指定的任务边界始终有效：只读检查不会变成修改，只写提案也不会被自动扩展成实现。

## ✨ 功能

| 功能 | Agent 会做什么 |
|---|---|
| 识别仓库现有规范 | 读取适用的仓库指令、提案、决策、当前文档、源码、测试、生成文件、CI 和相关 Git 历史 |
| 复用一份决策记录 | 优先更新已经负责该变更的记录；没有记录时才建立一份范围明确的新记录 |
| 编写可测试的验收条件 | 说明应该看到什么结果、哪里可能失败，以及哪个直接检查可以否定“已经完成” |
| 检查受影响的完整调用路径 | 确认修改后的代码真正连接到调用方、运行时、持久化或用户可见结果 |
| 处理需求变化 | 交付前直接修改未完成的提案；已交付决策被反转时才建立替换记录 |
| 保持仓库内容一致 | 在同一个 PR 或一组关联变更中，同步更新决策、代码、测试、生成文件、公共契约和当前文档 |
| 完整删除代码 | 检查真实消费者，并清理旧代码、注册、导出项、配置、测试、文档和兼容行为 |

核心规则是：

> 每个非机械变更都必须创建或更新一份负责该变更的决策记录。

只有不改变行为、契约、结构、流程、测试策略、存储数据格式或理由的拼写、纯格式调整等局部机械编辑可以豁免。

## 🧭 工作方式

Skill 不要求所有仓库使用同一套目录。它会先查找当前仓库已经用什么文件承担下面的职责。

| 通用职责 | 常见形式 |
|---|---|
| 仓库工作规则 | `AGENTS.md`、`CLAUDE.md`、Copilot instructions |
| 尚未完成的决策 | Spec、RFC、工作提案、design doc、ADR 草案 |
| 当前决策 | ADR、决策记录、已实施的设计文档、已交付的 RFC |
| 当前系统说明 | architecture docs、README、API 或 package docs |
| 局部检查 | `pytest`、`cargo test`、`go test`、`pnpm test`、真实 CLI/UI/API 检查 |
| 完整检查 | GitHub Actions、Makefile、pre-commit、仓库脚本 |

Python 项目不会被要求运行 `pnpm test`。已经使用 ADR 的仓库也不会被要求再建立一套决策目录。

只有不存在同等规范时，Skill 才会建议一个最小结构，例如仓库指令、当前架构文档和 `docs/decisions/`。它不会在没有实际需要时创建分类目录、archive、索引、validator、翻译或 checksum 文件。

### 决策生命周期

这套方法保留三个含义，但不强制使用某几个状态词：

| 阶段 | 含义 |
|---|---|
| Working | 尚未交付、只完成一部分或仍在修改 |
| Current | 实现、直接检查和当前文档已经一致 |
| Declined | 经过评估但没有采用；只有拒绝理由仍然有用时才保留 |

有些仓库的 `accepted ADR` 只表示已经批准，并不表示代码已经交付。只有实现、检查结果和当前文档都一致后，该决策在本方法中才属于 Current。

替换关系（replacement）是两项决策之间的关系：

- 尚未完成的提案直接修改；
- 已交付决策被反转时创建带交叉链接的新决策记录；
- 只替换一部分时，两个决策都继续处于 Current 状态，并注明各自负责的范围；
- 只有新记录保存了旧决策的独有理由、后果、验证要求和重新引入条件，才允许完全合并旧记录。

## 仓库结构

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

`SKILL.md` 保存跨宿主的核心流程。只有任务需要时才会读取 reference。`agents/openai.yaml` 保存可选的 Codex 专用 metadata，包括默认调用提示。

## 📝 更新日志

### v0.2 — 2026-08-17

将 Spec 编程闭环进一步通用化，使其能够用于采用不同规范的项目。Skill 能够复用不同项目已有的 Spec、RFC、ADR、文档、测试和 CI 规范，同时完善需求中途变化、决策归属、生命周期转换、局部替换和验证证据等规则。本次更新已通过跨语言场景测试、结构校验和独立审查。

### v0.1 — 2026-08-15

发布首个开源版本，将 DeepSeek Harness 公开仓库中可以观察到的 Spec 编程方法整理为可复用的 Agent Skill。这个版本提供中英文说明，以及 Codex、Claude Code 和 GitHub Copilot 的安装方式。

## 参与贡献

欢迎参与完善 `ds-spec-loop`。如果你发现问题或有改进建议，可以提交 Issue 并附上便于理解或复现的背景；也欢迎补充文档、使用案例或提交范围清晰的 Pull Request。

许可信息见 [LICENSE](LICENSE)。
