---
name: gsd-extract-learnings
description: 当需要从已完成的阶段产物中提取决策、经验教训、模式和意外发现时使用
---

# gsd-extract-learnings

## 描述

从已完成的阶段产物（PLAN.md、SUMMARY.md、VERIFICATION.md、UAT.md、STATE.md）中提取结构化经验教训到LEARNINGS.md文件，捕获做出的决策、学到的教训、发现的模式和遇到的意外。

## 指令

端到端执行工作流。

## 执行上下文

- `.trae/gsd/workflows/extract-learnings.md`

端到端执行 `.trae/gsd/workflows/extract-learnings.md` 工作流。

## 参数

- `<phase-number>` — 阶段编号（必需）

## 使用场景

- 阶段完成后需要总结经验教训
- 需要捕获项目中的决策和模式以供未来参考
- 需要记录意外发现以避免重复犯错

注意：本skill在SOLO Coder中作为GSD工作流的辅助工具使用。

## 不适用场景

- 阶段尚未完成时
- 仅需查看阶段摘要不需提取教训时
- 项目初期尚无已完成阶段时

## 输出

- LEARNINGS.md经验教训文件

## 依赖

- gsd-execute-phase（阶段需先完成执行）
