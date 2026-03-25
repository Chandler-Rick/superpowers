# Superpowers

Superpowers 是一套面向编码代理的完整软件开发工作流。它建立在一组可组合的“技能”之上，并配合一套初始指令，确保代理会在合适的时机自动使用这些技能。

## 它是怎么工作的

它从你启动编码代理的那一刻就开始发挥作用。只要代理发现你正在构建某个功能，它不会立刻冲上来写代码，而是先退一步，弄清楚你真正想解决的问题是什么。

当它从对话里逐步整理出需求规格后，会把设计内容拆成一段一段足够短的部分展示给你，方便你逐步阅读和确认。

在你确认设计之后，代理会整理出一份实现计划。这份计划足够清晰，哪怕交给一位热情但经验不足、判断力一般、不了解项目背景且不喜欢测试的初级工程师，也能照着执行。整个过程强调真正的红绿测试驱动开发、YAGNI（你不会需要它）和 DRY（不要重复自己）。

接下来，当你说“开始”之后，它会进入一种由子代理驱动的开发流程：把工程任务分发出去，让不同代理完成、检查、评审，再继续推进。Claude 这类代理经常可以连续自主工作几个小时，并且仍然沿着你批准的计划前进。

系统里还有不少其他机制，但上面这些就是核心。因为技能会自动触发，所以你不需要做额外操作。你的编码代理会自然获得这些 Superpowers。

## 赞助

如果 Superpowers 帮你完成了能带来收益的事情，并且你愿意支持开源作者，可以考虑赞助 [Jesse 的开源工作](https://github.com/sponsors/obra)。

谢谢。

- Jesse

## 安装

**注意：** 不同平台的安装方式不同。Claude Code 和 Cursor 有内置插件市场；Codex 与 OpenCode 需要手动配置。

### Claude Code 官方市场

Superpowers 已经发布在 [Claude 官方插件市场](https://claude.com/plugins/superpowers)。

从 Claude 市场安装：

```bash
/plugin install superpowers@claude-plugins-official
```

### Claude Code（通过插件市场）

在 Claude Code 中，先注册插件市场：

```bash
/plugin marketplace add obra/superpowers-marketplace
```

然后从这个市场安装插件：

```bash
/plugin install superpowers@superpowers-marketplace
```

### Cursor（通过插件市场）

在 Cursor Agent 聊天中执行：

```text
/add-plugin superpowers
```

或者直接在插件市场里搜索 `superpowers`。

### Codex

告诉 Codex：

```text
Fetch and follow instructions from https://raw.githubusercontent.com/obra/superpowers/refs/heads/main/.codex/INSTALL.md
```

详细文档：`docs/README.codex.md`

### OpenCode

告诉 OpenCode：

```text
Fetch and follow instructions from https://raw.githubusercontent.com/obra/superpowers/refs/heads/main/.opencode/INSTALL.md
```

详细文档：`docs/README.opencode.md`

### Gemini CLI

```bash
gemini extensions install https://github.com/obra/superpowers
```

更新命令：

```bash
gemini extensions update superpowers
```

### 验证安装

在你选择的平台中开启一个新会话，然后让代理做一件本应触发某项技能的事情，例如“帮我规划这个功能”或者“我们来排查这个问题”。如果安装正常，代理应该会自动调用对应的 Superpowers 技能。

## 基础工作流

1. **brainstorming**：在写代码之前触发。通过提问打磨想法，探索备选方案，把设计拆成若干段供你确认，并保存设计文档。
2. **using-git-worktrees**：设计通过后触发。创建独立工作目录和分支，执行项目初始化，并确认测试基线是干净的。
3. **writing-plans**：设计批准后触发。把工作拆成 2 到 5 分钟级别的小任务。每个任务都包含精确文件路径、完整代码和验证步骤。
4. **subagent-driven-development** 或 **executing-plans**：有计划后触发。为每个任务分派新的子代理，并经过两轮评审（规格符合性、代码质量）；或者按批次执行并在人类检查点暂停。
5. **test-driven-development**：实现过程中触发。强制执行 RED-GREEN-REFACTOR：先写失败测试，确认失败，再写最少代码，确认通过，然后重构。对于“先写代码后补测试”的做法会严格纠正。
6. **requesting-code-review**：任务之间触发。按照计划执行审查，并按严重程度报告问题。严重问题会阻止继续推进。
7. **finishing-a-development-branch**：任务完成后触发。验证测试、提供后续选项（合并、提 PR、保留、丢弃），并清理工作树。

**代理在执行任何任务之前，都会先检查是否存在相关技能。** 这些是强制性的工作流，而不是可选建议。

## 项目包含什么

### 技能库

**测试**

- **test-driven-development**：RED-GREEN-REFACTOR 测试驱动循环（附带测试反模式参考资料）

**调试**

- **systematic-debugging**：四阶段根因排查流程（包含 root-cause-tracing、defense-in-depth、condition-based-waiting 等技巧）
- **verification-before-completion**：确保问题真的被修复，而不是口头宣称已解决

**协作**

- **brainstorming**：苏格拉底式设计澄清
- **writing-plans**：详细实现计划
- **executing-plans**：带检查点的批量执行
- **dispatching-parallel-agents**：并行子代理工作流
- **requesting-code-review**：提交审查前检查
- **receiving-code-review**：如何回应评审意见
- **using-git-worktrees**：并行开发分支
- **finishing-a-development-branch**：合并与 PR 决策流程
- **subagent-driven-development**：基于双阶段审查的快速迭代开发

**元能力**

- **writing-skills**：按最佳实践创建新技能（包含测试方法）
- **using-superpowers**：技能系统入门

## 设计理念

- **测试驱动开发**：永远先写测试
- **系统化胜过临时拍脑袋**：流程优先于猜测
- **降低复杂度**：把简单作为首要目标
- **证据胜过宣称**：在宣布成功之前先验证

延伸阅读：[Superpowers for Claude Code](https://blog.fsck.com/2025/10/09/superpowers/)

## 如何参与贡献

技能文件直接保存在这个仓库中。参与方式如下：

1. Fork 这个仓库
2. 为你的技能创建分支
3. 按照 `writing-skills` 技能的流程创建并测试新技能
4. 提交 PR

完整指南见：`skills/writing-skills/SKILL.md`

## 更新

更新插件后，技能会自动更新：

```bash
/plugin update superpowers
```

## 许可证

MIT License，详见 `LICENSE` 文件。

## 社区

Superpowers 由 [Jesse Vincent](https://blog.fsck.com) 与 [Prime Radiant](https://primeradiant.com) 的团队共同构建。

如果你想获得社区支持、提问或分享你在做的项目，可以加入 [Discord 社区](https://discord.gg/Jd8Vphy9jq)。

## 支持渠道

- **Discord**：<https://discord.gg/Jd8Vphy9jq>
- **Issues**：<https://github.com/obra/superpowers/issues>
- **Marketplace**：<https://github.com/obra/superpowers-marketplace>
