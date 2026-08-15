# ds-spec-loop

[English](README.md) | **简体中文**

> 一个可复用的 Agent Skill，把 DeepSeek Harness 公开仓库中可以观察到的 Spec 编程方法应用到其他软件项目中。

`ds-spec-loop` 用于帮助编程 Agent 在开发功能、修复 Bug、调整架构或接口、改进测试与开发流程、简化或删除代码时，让需求、决策、实现、测试和文档保持一致。

这里的 Spec 编程不是“先写一份很长的计划再开始编码”，而是把仓库本身作为事实来源：仓库指令记录约束，当前文档描述系统现状，决策记录保留选择某种方案的原因，代码和测试提供可以运行或检查的证据。

## 🧭 方法来源

这个 Skill 是一个独立社区项目，方法来源于对 [DeepSeek Harness](https://github.com/deepseek-ai/deepseek-harness) 公开仓库及其 Git 历史的研究。可以从中观察到的做法包括：

- 使用仓库级和目录级指令约束 Agent；
- 用架构文档和包级文档描述当前系统；
- 使用带有 `proposed`、`implemented`、`rejected`、`superseded` 和 `archived` 状态的决策记录；
- 沿真实的集成与运行链路完成实现；
- 把验收条件与直接证据对应起来；
- 在同一次变更中同步代码、测试、生成产物和文档。

`ds-spec-loop` 把这些公开可观察的做法整理成可移植的 Agent Skill。它不是 DeepSeek 官方项目，也没有获得 DeepSeek 背书，并且不分发 DeepSeek Harness 的源代码。

## ✨ Skill 能做什么

| 功能 | Agent 会做什么 |
| --- | --- |
| 修改前理解仓库 | 阅读适用的仓库指令、当前文档、已有决策、相关源码、测试和生成文件；必要时查看 Git 历史 |
| 维护决策记录 | 创建或更新负责当前决定的记录，并在实现、否决、替换或归档时保持生命周期准确 |
| 编写可验证的验收条件 | 把每项要求与可观察行为、可能失败的位置，以及能够确认或否定完成状态的证据对应起来 |
| 完成整条集成链路 | 根据项目实际结构检查定义、provider、注册或加载、consumer、持久化，以及面向用户或模型的行为 |
| 保持仓库内容一致 | 同步更新受影响的代码、公共接口、测试、快照、生成产物、当前文档和决策理由 |
| 支持简化与删除 | 调查真实使用方，并清理已经无效的注册项、export、文件、测试、文档和兼容层，而不是只删除主要源码 |
| 只读审查 | 在不修改文件的情况下，比较当前决策、源码、测试、生成产物和文档是否一致 |
| 适配已有规范 | 复用仓库已有的 ADR、RFC、设计文档或 Spec 体系，不另建一套相互竞争的文档结构 |

它适用于功能开发、Bug 修复、API 或配置变化、架构调整、测试策略变化、开发流程变化、代码删除，以及 Spec 与代码一致性审查。拼写修正、纯格式调整等局部机械修改通常不需要使用这个 Skill。

## 🚀 快速开始

使用社区维护的跨 Agent [`skills`](https://skills.sh/) CLI 安装：

```bash
npx skills add songyang0603/ds-spec-loop
```

然后在 Codex 中调用：

```text
使用 $ds-spec-loop 实现这个功能。
修改前先检查仓库指令、当前文档、已有决策、相关源码、测试和真实集成链路。
完成后让决策记录、实现、验证证据和文档保持一致。
```

不同宿主的显式调用方式不同：

| 宿主 | 调用方式 |
| --- | --- |
| Codex | `$ds-spec-loop` |
| Claude Code | `/ds-spec-loop` |
| GitHub Copilot CLI | `/ds-spec-loop` |
| 其他兼容 Agent | 使用该宿主规定的 Skill 调用方式，或直接点名 `ds-spec-loop` |

### 常见用法

只写 Spec，不实现：

```text
使用 $ds-spec-loop 调查这个改动并编写 proposed 决策记录，不要实现。
请独立于首选方案描述问题，比较真实可行的替代方案，并为验收条件注明直接证据。
```

继续已有 proposal：

```text
使用 $ds-spec-loop 继续已有的 proposed 决策，完成实现、测试和文档更新，
并在证据与实际结果一致后更新决策记录的状态。
```

只读审查一致性：

```text
使用 $ds-spec-loop 检查当前决策、源码、公共接口、测试、生成产物和当前文档
是否一致。不要修改任何文件。
```

简化或删除代码：

```text
使用 $ds-spec-loop 调查这段代码的真实使用方并规划删除。
如果确认可以删除，请修改完整集成链路，并检查旧文件、注册项、export、测试和文档
是否已经清理干净。
```

用户指定的任务边界始终有效：只读审查不会变成修改，只写 Spec 也不会被擅自扩展成实现。在 Claude Code 或 GitHub Copilot CLI 中，请把 `$ds-spec-loop` 替换为 `/ds-spec-loop`。

## 🧩 工作原理

Skill 把 Spec 看作仓库中一组相互关联的记录：

```text
仓库指令 + 当前文档 + 决策记录
                ↕
源码 + 类型 + 配置 + 实际集成链路
                ↕
测试 + 可运行行为 + 生成产物
```

- **当前文档**说明仓库现在如何工作。
- **决策记录**说明某项决定为什么被提出、接受、否决、替换或保留。
- **源码和公共接口**落实这些决定。
- **测试和可运行链路**为可观察行为提供证据。
- **仓库专用检查**约束能够被程序直接判断的事实。

Agent 只更新本次任务真正影响到的记录。格式检查通过不等于 Spec 与实现语义一致，修改了一个模块也不等于功能已经接入完整系统。

## 📦 安装

[Agent Skills 开放规范](https://agentskills.io/specification)统一的是可移植 `SKILL.md` 包格式；发现目录与调用语法仍由各宿主决定。

### 跨 Agent 安装器

```bash
npx skills add songyang0603/ds-spec-loop
```

安装器会找到 `skills/ds-spec-loop/SKILL.md`，并让你选择目标 Agent 和安装范围。

### GitHub CLI

GitHub CLI 也提供预览版 Agent Skills 安装器：

```bash
gh skill install songyang0603/ds-spec-loop ds-spec-loop --agent codex --scope user
```

如需安装给 Claude Code 或 GitHub Copilot，请把 `codex` 替换为 `claude-code` 或 `github-copilot`。

### 手动安装

Clone 本仓库，然后把 `skills/ds-spec-loop` 复制到 Agent 支持的发现目录：

| 宿主 | 用户级目录 | 仓库级目录 |
| --- | --- | --- |
| Codex | `~/.agents/skills/ds-spec-loop` | `.agents/skills/ds-spec-loop` |
| Claude Code | `~/.claude/skills/ds-spec-loop` | `.claude/skills/ds-spec-loop` |
| GitHub Copilot CLI | `~/.copilot/skills/ds-spec-loop` 或 `~/.agents/skills/ds-spec-loop` | `.github/skills/ds-spec-loop` 或 `.agents/skills/ds-spec-loop` |

Codex 和 Claude Code 的官方文档也明确支持链接 Skill 目录。对于 GitHub Copilot CLI，请使用复制或其文档规定的目录注册机制。发现机制的最新细节请参考 [Codex](https://developers.openai.com/codex/skills/)、[Claude Code](https://code.claude.com/docs/en/skills) 与 [GitHub Copilot CLI](https://docs.github.com/en/copilot/how-tos/copilot-cli/customize-copilot/add-skills) 官方文档。

## 仓库结构

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

Agent 会先加载简洁的 `SKILL.md` 入口，再根据当前任务读取需要的 reference，避免占用不必要的上下文。

## 💬 参与贡献

欢迎分享想法、提交 Issue 或 Pull Request。如果它在你的仓库里表现得不够好，可以简单说说你原本想做什么、使用了哪个 Agent，以及实际发生了什么，我们可以从这里一起继续完善。

归属说明见 [NOTICE](NOTICE)，本仓库许可见 [LICENSE](LICENSE)。
