---
名称: 使用 Git worktree（using-git-worktrees）
描述: 在需要与当前工作区隔离的特性开发或执行实现计划前，创建隔离的 git worktree
---

# 使用 Git worktree

## 概述

Git worktree 可创建隔离的工作区，共享同一仓库，允许同时在多个分支上工作，无需切换。

**核心原则：** 系统化目录选择 + 安全校验 = 可靠隔离。

**开始时声明：**“我正在使用 using-git-worktrees 技能设置隔离工作区。”

## 目录选择流程

优先顺序如下：

### 1. 检查现有目录

```bash
# 按优先顺序检查
ls -d .worktrees 2>/dev/null     # 首选（隐藏）
ls -d worktrees 2>/dev/null      # 备选
```

**如存在：** 直接使用。若两者都存在，优先 .worktrees。

### 2. 检查 CLAUDE.md

```bash
grep -i "worktree.*director" CLAUDE.md 2>/dev/null
```

**如有偏好：** 直接采用，无需询问。

### 3. 询问用户

如无现有目录且无 CLAUDE.md 偏好：

```
未找到 worktree 目录。应在哪里创建 worktree？

1. .worktrees/（项目本地，隐藏）
2. ~/.config/superpowers/worktrees/<项目名>/（全局）

你更倾向于哪种？
```
