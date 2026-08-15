# ds-spec-loop

一个可复用的 Agent Skill，用于运行完整的、仓库原生的 Spec 编程闭环。

`ds-spec-loop` 提炼自 [DeepSeek Harness](https://github.com/deepseek-ai/deepseek-harness) 公开仓库中可以直接观察到的工程方法：长期有效的仓库指令、描述当前事实的架构文档、带生命周期的 Agent Note、贯穿真实组装路径的实现、可反驳验收声明的执行证据、机械 gate，以及代码与文档的最终收敛。

它不是一个“先写 Spec，再生成代码”的提示词。这里的 Spec 是一套分布式权威系统：

```text
仓库指令 + 当前事实文档 + 决策 Note
                 ↕
源码 + 类型 + package/config 拓扑
                 ↕
测试 + 快照 + 真实运行路径 + 机械 gate
```

## 能力范围

- feature、bug-fix、simplification、architecture、process、testing 六类决策；
- proposed → implemented 或 proposed → rejected 生命周期；
- supersession、consolidation 与 archive 纪律；
- 每个非平凡变更只有一个 owning decision；
- 把可观察验收映射到能够反驳它的证据；
- 实现真实 assembled path，而不是只完成一个叶子模块；
- 只读核验 Spec、源码、测试、生成产物和用户文档之间的漂移；
- 适配已有 ADR/RFC 体系或尚无 Spec 约定的仓库。

只有完全机械、局部，并且不改变行为、契约、结构、流程、测试策略或长期决策理由的修改，才不需要 Agent Note。

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

可移植核心是 `skills/ds-spec-loop/SKILL.md` 和 `references/`。`agents/openai.yaml` 只提供 Codex UI metadata，其他 Agent 可以忽略。

## 安装

[Agent Skills 开放规范](https://agentskills.io/specification)统一了 Skill 包格式，但不同 Agent 的发现目录不同。

### Codex

让 Codex 从下面的 GitHub 目录安装：

```text
https://github.com/songyang0603/ds-spec-loop/tree/main/skills/ds-spec-loop
```

也可以 clone 本仓库，把 `skills/ds-spec-loop` 链接或复制到：

```text
~/.agents/skills/ds-spec-loop
```

Codex 也会发现仓库内 `.agents/skills/` 下的项目级 Skill。详见 [OpenAI Build skills 官方文档](https://developers.openai.com/codex/skills/)。如果 Skill 没有立刻出现，请重启 Codex。

### Claude Code

把可移植 Skill 目录链接或复制到个人或项目目录：

```text
~/.claude/skills/ds-spec-loop
.claude/skills/ds-spec-loop
```

详见 [Claude Code Skills 官方文档](https://code.claude.com/docs/en/slash-commands)。

### GitHub Copilot CLI

把可移植 Skill 目录链接或复制到：

```text
~/.copilot/skills/ds-spec-loop
.github/skills/ds-spec-loop
```

GitHub Copilot CLI 也支持 `.agents/skills/`；详见 [GitHub Copilot Agent Skills 官方文档](https://docs.github.com/en/copilot/how-tos/copilot-cli/customize-copilot/add-skills)。

### 其他兼容 Agent Skills 的 Agent

让 Agent 的 Skill 发现机制指向 `skills/ds-spec-loop`，或把该目录复制到产品文档指定的位置。`SKILL.md` frontmatter 只使用标准的 `name` 与 `description` 字段。

可移植 Skill 包不保证不同宿主具有相同的隐式触发、shell/Git 权限或工具命名；这些仍由各产品决定。

## 使用方法

完整实施：

```text
Use $ds-spec-loop to design and implement this non-trivial change. Work from the repository's own instructions, current docs, decision notes, source, and tests. Stop only when every claimed acceptance criterion has direct evidence or an explicit verification boundary.
```

只写 Spec，不实现：

```text
Use $ds-spec-loop to write the owning proposed Agent Note for this change. Investigate the repository and history, but do not implement it.
```

继续已有 proposed Spec：

```text
Use $ds-spec-loop to continue the existing proposed spec through implementation, executable evidence, and lifecycle convergence.
```

只读核验：

```text
Use $ds-spec-loop to verify whether the active spec, source, generated references, tests, and user-facing docs agree. Do not modify files.
```

简化与删除：

```text
Use $ds-spec-loop to determine whether this surface earns its maintenance cost through real consumers. Remove or narrow it only if the repository evidence supports that decision, and specify complete absence.
```

Skill 会尊重用户指定的停止边界：verify-only 保持只读，specify-only 不会被擅自扩展成实现。

## 为什么不附带通用校验器和合成评测

这套方法需要机械 gate，但 gate 必须编码目标仓库真实的路径、生命周期、生成产物、依赖拓扑和 CI 命令。通用格式校验器最多证明标题和状态合法，容易让人误以为 Spec 与实现语义一致。

v1 的决定是：

- 开发阶段用官方 Skill validator 校验 Skill 包；
- 在目标仓库里，为重要且可机械判断的规则增加 repo-specific gate；
- fresh-agent forward test 只作为开发证据，不作为用户运行时文件发布；
- GitHub 不包含测试编排、golden output、合成仓库或复制来的 validator。

只有当真实用户反复遇到同一种可机械判断的错误时，才值得增加一个小型公开校验器。它应当只读、可配置，并明确不负责判断语义质量。

## 来源与独立性

这是一个独立社区项目，方法来源于对公开、MIT 许可的 DeepSeek Harness 仓库的研究。它不是 DeepSeek 官方项目，也没有获得 DeepSeek 背书。Skill 是对方法论的重新表达，不分发 DeepSeek Harness 源码。

归属说明见 [NOTICE](NOTICE)，本仓库许可见 [LICENSE](LICENSE)。

English documentation: [README.md](README.md)
