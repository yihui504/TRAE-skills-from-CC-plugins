---
name: gsd-eval-review
description: 当需要审计已执行AI阶段的评估覆盖率并生成EVAL-REVIEW.md补救计划时使用
---

# gsd-eval-review

## 描述

对已完成的AI阶段进行回顾性评估覆盖率审计。
检查AI-SPEC.md中的评估策略是否已实现。
生成EVAL-REVIEW.md，包含评分、结论、差距和补救计划。

## 上下文

阶段：用户输入参数 — 可选，默认为最后完成的阶段。

## 指令

端到端执行。
保留所有工作流关卡。

## 执行上下文

- `.trae/gsd/workflows/eval-review.md`
- `.trae/gsd/references/ai-evals.md`

## 参数

- `[phase number]` — 可选的阶段编号，默认为最后完成的阶段

## 使用场景

- AI阶段执行完成后需要审查评估覆盖率
- 需要验证AI-SPEC.md中的评估策略是否已实施
- 需要生成评估差距的补救计划

注意：本skill在SOLO Coder中作为GSD工作流的辅助工具使用。

## 不适用场景

- 非AI相关的常规功能阶段
- 尚未执行AI阶段时
- 仅需查看AI-SPEC.md不需审查评估时

## 输出

- EVAL-REVIEW.md评估审查报告

## 依赖

- gsd-ai-integration-phase（需先有AI-SPEC.md）
- gsd-execute-phase（阶段需先完成执行）
