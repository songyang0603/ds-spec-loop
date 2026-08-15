# ds-spec-loop

[English](README.md) | **简体中文**

> 一个仓库原生的 Agent Skill，让非平凡的 AI 辅助编程任务中的决策、代码、测试与当前文档始终保持一致。

`ds-spec-loop` 把 Spec 编程变成编程 Agent 可以持续执行的工程方法，而不是在写代码前生成一份庞大计划。它提炼并重新表达了 [DeepSeek Harness](https://github.com/deepseek-ai/deepseek-harness) 公开仓库和 Git 历史中可以观察到的模式：仓库级指令、当前事实文档、带生命周期的决策记录、贯穿完整组装路径的实现、可被证伪的验收条件及其直接证据，以及受变更影响的全部事实载体重新一致。

它的目标是提高 vibe coding 的可靠性，而不是让每次修改都变成仪式。Agent 会先还原仓库已经规定了什么，再确立负责本次变更的决策记录，沿真实运行链路完成实现，并且只有在 Spec、代码、证据与当前事实一致后才结束任务。

## 快速开始

使用社区维护的跨 Agent [`skills`](https://skills.sh/) CLI 安装：

```bash
npx skills add songyang0603/ds-spec-loop
```

然后对你的编码 Agent 说：

```text
使用 $ds-spec-loop 设计并实现这个非平凡变更。
先还原仓库现有的权威信息，建立或更新负责该变更的决策记录，沿完整组装路径实现；
只有在 Spec、代码、测试、证据和当前文档全部收敛后，才可以声称完成。
```

不同宿主的显式调用方式不同：

| 宿主 | 调用方式 |
| --- | --- |
| Codex | `$ds-spec-loop` |
| Claude Code | `/ds-spec-loop` |
| GitHub Copilot CLI | `/ds-spec-loop` |
| 其他兼容 Agent | 使用该宿主规定的 Skill 调用方式，或直接点名 `ds-spec-loop` |

## 为什么使用它

快速生成的 AI patch 经常只在被修改的文件里看起来正确。一个变更可能表面已经完成，实际上却：

- 回答了提示词，却违反仓库真正的契约；
- 只实现叶子模块，没有接入 provider、loader、consumer、持久化或用户可见路径；
- 让架构文档或长期决策理由停留在旧状态；
- 重复创建已有决策，或者再次尝试仓库已经否决的方案；
- 删除了源码，却留下 export、注册项、manifest、快照、文档或持久化格式；
- 把格式检查或单元测试通过误当成端到端行为成立。

`ds-spec-loop` 给 Agent 一个覆盖整个仓库的“完成”定义。它也会提高后续 Agent 会话的效率：新的 Agent 可以从维护过的仓库材料中恢复当前事实与历史理由，不必每次都从头猜测意图。

## 核心方法

Spec 是一个分布式权威系统，而不是单独一份 Markdown：

```text
仓库指令 + 当前事实文档 + 决策记录
                  ↕
源码 + 类型 + package/config/组装拓扑
                  ↕
测试 + 快照 + 可运行路径 + 生成产物 + 机械检查
```

这套权威系统要求六项相互耦合的责任始终一致：

- **还原仓库权威信息。** 在偏好某种实现之前，先阅读适用的指令、当前事实文档、既有决策、公共契约、入口、组装路径、测试、生成产物和相关历史。
- **确立主决策记录。** 如果变更会影响行为、契约、架构、流程、测试策略、持久格式或长期理由，就复用已经负责该决策的记录，或创建新的记录。每个长期决策只保留一份主记录，避免重复描述同一决定。
- **让验收可以被证伪。** 每条验收声明都要指出可观察结果、可能失败的层、能够否证它的直接证据，以及产生该证据的准确命令或运行路径。
- **修改完整组装路径。** 在实际存在的地方追踪并更新定义、provider、注册或 loader、consumer、持久化，以及面向模型或用户的接口与呈现层，而不是只完成叶子实现。
- **站在真实使用者角度复核。** 脱离 patch 重新阅读需求与决策，验证正向和负向保证，并严格区分已执行检查、人工检查和未验证边界。
- **收敛生命周期与当前事实。** 只有当实现和证据一致后，才能把 proposal 转为 `implemented`；随后将其改写为当前事实、同步当前文档，并保留 rejected 或 superseded 的理由，但不把历史当成当前权威。

决策记录具有明确的生命周期：

```text
proposed ──→ implemented ──→ archived
    └──────→ rejected
```

只有当 implemented 记录不再负责解释仍然有效的决策理由时，才应归档。决策发生变化时，应创建与旧记录相互链接的后继记录，并把旧记录标记为 superseded；不要把旧记录改写成相反的决定。

Skill 使用六种决策类型：`feature`、`bug-fix`、`simplification`、`architecture`、`process` 和 `testing`。分类不是为了整理文件夹，而是因为不同类型具有不同的高概率失败面和证据需求。如果仓库已经有等价的 ADR、RFC 或 Spec 约定，Skill 会沿用原有体系，不会额外建立一套平行文档系统。

完全机械且局部的修改可以豁免，但前提是它不改变行为、契约、结构、流程、测试策略、持久格式或长期理由。是否需要 Spec 不由 diff 大小或文件数量决定。

## 能做什么

| 任务 | Agent 会做什么 |
| --- | --- |
| 设计变更 | 调查仓库，并在实现前编写或修复负责该变更的 proposed 决策 |
| 实现已有 proposal | 沿真实组装路径完成实现、直接证据与生命周期收敛 |
| 修复 bug | 记录被破坏的契约、根因与回归面，并用回归证据证明缺陷已被修复 |
| 简化或删除 | 调查目标功能及其真实消费者，确定保留下来的责任归属，定义“完全不存在”，并清理残留拓扑与文档 |
| 审查或核验 | 只读检查活跃决策、源码、测试、生成产物和当前文档是否一致 |
| 在仓库中引入 Spec 编程 | 把方法映射到仓库已有约定，而不是强加一套平行文档体系 |

用户要求的任务边界始终有效：verify-only 必须保持只读，specify-only 不会被擅自扩展成实现。

## 安装

[Agent Skills 开放规范](https://agentskills.io/specification)统一的是可移植 `SKILL.md` 包格式；发现目录与调用语法仍由各宿主决定。

### 跨 Agent 安装器

对于 Codex、Claude Code、GitHub Copilot、Cursor、Gemini CLI、OpenCode、Windsurf 等受支持的 Agent，最快的安装方式是：

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

Codex 和 Claude Code 的官方文档也明确支持链接 Skill 目录。对于 GitHub Copilot CLI，应使用复制或其文档规定的目录注册机制，不要假定它会直接发现软链接。发现机制的最新细节请参考 [Codex](https://developers.openai.com/codex/skills/)、[Claude Code](https://code.claude.com/docs/en/skills) 与 [GitHub Copilot CLI](https://docs.github.com/en/copilot/how-tos/copilot-cli/customize-copilot/add-skills) 官方文档。如果新建的顶层 Skill 目录没有立刻被识别，请重启或重新加载 Agent。

对于其他兼容 Agent Skills 的宿主，请按照对应产品的文档安装可移植目录 `skills/ds-spec-loop`。本仓库有意把跨平台指令保存在 `SKILL.md` 和 `references/` 中；`agents/openai.yaml` 只提供可选的 Codex UI metadata。

## 使用示例

### 完整实施

```text
使用 $ds-spec-loop 设计并实现这个变更。先阅读仓库自己的指令、当前文档、决策、
源码和测试。只有当每条验收标准都有直接证据或明确的未验证边界后，才可以声称完成。
```

### 只写 Spec

```text
使用 $ds-spec-loop 调查这个变更并编写负责它的 proposed Agent Note，不要实现。
问题描述必须独立于具体方案，并为每条验收标准注明能够反驳它的证据。
```

### 继续已有 proposal

```text
使用 $ds-spec-loop 继续现有的 proposed 决策，完成实现、完整组装路径验证、
文档更新与生命周期收敛。
```

### 只读核验漂移

```text
使用 $ds-spec-loop 核验活跃决策、源码、公共契约、生成的参考资料、测试与用户文档
是否一致。不要修改任何文件。
```

### 简化或删除

```text
使用 $ds-spec-loop 根据真实消费者判断这个表面是否值得继续维护。如果仓库证据支持删除，
请定义并验证它在源码、注册项、export、manifest、测试和文档中的完全不存在。
```

在 Claude Code 或 GitHub Copilot CLI 中，请把 `$ds-spec-loop` 替换为 `/ds-spec-loop`。

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

Agent 会先加载紧凑的 `SKILL.md` 入口，再按当前任务需要读取对应 reference，避免一次性占用不必要的上下文。

## 来源与独立性

这是一个独立的社区项目，是对 DeepSeek Harness 公开、MIT 许可仓库及其 Git 历史中可观察工程模式的重新表达。它不是 DeepSeek 官方项目，也没有获得 DeepSeek 背书。本 Skill 是对这些模式的全新可复用表达，不分发 DeepSeek Harness 源码。

归属说明见 [NOTICE](NOTICE)，本仓库许可见 [LICENSE](LICENSE)。

## 参与贡献

欢迎提交 Issue 和 Pull Request。最有价值的问题报告应包含真实仓库任务、使用的 Agent 与版本、调用方式、实际行为、期望行为，以及能够说明缺口的仓库证据。
