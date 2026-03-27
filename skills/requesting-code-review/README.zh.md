---
名称: 请求代码评审（requesting-code-review）
描述: 在完成任务、实现主要功能或合并前，需验证工作是否符合要求时使用
---

# 请求代码评审

调度 superpowers:code-reviewer 子代理，提前发现问题，防止后续连锁反应。评审者只获取精确编写的上下文，不包含你的会话历史，确保专注于工作成果，也便于你继续工作。

**核心原则：** 早评审，常评审。

## 何时请求评审

**强制：**
- 每个 subagent-driven-development 任务后
- 主要功能完成后
- 合并到主分支前

**可选但有价值：**
- 卡住时（换个视角）
- 重构前（基线检查）
- 修复复杂 bug 后

## 如何请求

**1. 获取 git SHA：**
```bash
BASE_SHA=$(git rev-parse HEAD~1)  # 或 origin/main
HEAD_SHA=$(git rev-parse HEAD)
```

**2. 调度 code-reviewer 子代理：**

使用 Task 工具，类型为 superpowers:code-reviewer，填写 code-reviewer.md 模板

**占位符：**
- `{WHAT_WAS_IMPLEMENTED}` - 刚刚实现的内容
- `{PLAN_OR_REQUIREMENTS}` - 应实现的内容
- `{BASE_SHA}` - 起始提交
- `{HEAD_SHA}` - 结束提交
- `{DESCRIPTION}` - 简要说明

**3. 处理反馈：**
- 立即修复关键问题
- 继续前修复重要问题
- 次要问题记录后续处理
- 评审者有误时据理力争

## 示例
（可补充具体例子）
