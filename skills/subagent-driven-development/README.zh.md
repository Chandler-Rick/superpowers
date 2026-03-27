---
名称: 子代理驱动开发（subagent-driven-development）
描述: 在当前会话中执行实现计划且任务相互独立时使用
---

# 子代理驱动开发

通过为每个任务分派全新子代理，并在每步后进行两阶段评审（规范合规→代码质量），高效高质地执行计划。

**为何用子代理：** 你将任务委托给专用代理，精确传递上下文，确保专注且高效。代理不继承你的会话历史，避免上下文污染，也便于你自己协调。

**核心原则：** 每任务新子代理 + 两阶段评审 = 高质量、快迭代

## 适用场景

```dot
digraph when_to_use {
    "有实现计划吗？" [shape=diamond];
    "任务大多独立吗？" [shape=diamond];
    "留在本会话？" [shape=diamond];
    "subagent-driven-development" [shape=box];
    "executing-plans" [shape=box];
    "手动执行或先头脑风暴" [shape=box];

    "有实现计划吗？" -> "任务大多独立吗？" [label="是"];
    "有实现计划吗？" -> "手动执行或先头脑风暴" [label="否"];
    "任务大多独立吗？" -> "留在本会话？" [label="是"];
    "任务大多独立吗？" -> "手动执行或先头脑风暴" [label="否-强耦合"];
    "留在本会话？" -> "subagent-driven-development" [label="是"];
    "留在本会话？" -> "executing-plans" [label="否-需并行会话"];
}
```

**与 executing-plans（并行会话）的区别：**
- 同一会话（无上下文切换）
- 每任务新子代理（无上下文污染）
- 每步后两阶段评审：先规范合规，再代码质量
- 迭代更快（任务间无需人工介入）

## 流程

```dot
digraph process {
    rankdir=TB;

    subgraph cluster_per_task {
        label="每任务";
        "分派实现子代理 (./implementer-prompt.md)" [shape=box];
        "实现子代理有疑问？" [shape=diamond];
        "答疑并补充上下文" [shape=box];
    }
}
```

（后续流程可补充）
