---
name: gsd-cleanup
description: 当需要归档已完成里程碑的累积阶段目录时使用
---

# gsd-cleanup

## 描述

将已完成里程碑的阶段目录归档到 `.trae/gsd/planning/milestones/v{X.Y}-phases/`。

当 `.trae/gsd/planning/phases/` 中积累了过去里程碑的目录时使用。

## 指令

端到端执行。
识别已完成的里程碑，显示试运行摘要，确认后归档。

## 执行上下文

- `.trae/gsd/workflows/cleanup.md`

## 使用场景

- 已完成里程碑的阶段目录占用空间需要归档
- `.trae/gsd/planning/phases/` 目录积累了多个里程碑的产物
- 里程碑完成后需要整理规划目录

注意：本skill在SOLO Coder中作为GSD工作流的辅助工具使用。

## 不适用场景

- 当前里程碑尚未完成时
- 需要保留阶段目录以便参考时
- 项目初期尚无已完成里程碑时

## 输出

- 归档后的阶段目录（移至milestones/下）
- 清理后的phases/目录

## 依赖

- gsd-complete-milestone（里程碑需先完成）
