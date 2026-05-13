---
name: gsd-fast
description: 当需要内联执行简单任务——无子代理、无规划开销时使用
---

# gsd-fast

## 描述

在当前上下文中直接执行简单任务，不生成子代理或PLAN.md文件。适用于不值得规划开销的任务：拼写修复、配置更改、小型重构、遗漏的提交、简单添加。

这不是 `gsd-quick skill` 的替代品 — 对于需要研究、多步规划或验证的任务请使用 `gsd-quick skill`。`gsd-fast skill` 适用于你可以在一句话中描述并在2分钟内执行的任务。

## 指令

端到端执行。

## 执行上下文

- `.trae/gsd/workflows/fast.md`

## 参数

- `[task description]` — 任务描述

## 使用场景

- 需要执行一句话就能描述的简单任务
- 拼写修复、配置更改、小型重构等
- 不值得启动完整规划流程的快速改动

注意：本skill可独立于GSD流程使用，在SOLO Coder中直接调用即可。

## 不适用场景

- 需要研究或多步规划的任务（应使用quick skill）
- 需要验证的复杂功能（应使用execute-phase skill）
- 需要讨论决策的任务（应使用discuss-phase skill）

## 输出

- 直接完成的任务结果
- 提交记录（如适用）

## 依赖

- 无（独立skill）
