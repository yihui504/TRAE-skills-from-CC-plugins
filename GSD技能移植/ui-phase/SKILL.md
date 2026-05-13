---
name: gsd-ui-phase
description: 当需要为前端阶段生成UI设计契约（UI-SPEC.md）时使用
---

# gsd-ui-phase

## 描述

为前端阶段创建UI设计契约（UI-SPEC.md）。
编排gsd-ui-researcher和gsd-ui-checker。
流程：验证 → 研究UI → 验证UI-SPEC → 完成

## 上下文

阶段编号：用户输入参数 — 可选，如果省略则自动检测下一个未规划的阶段。

## 指令

端到端执行。
保留所有工作流门控。

## 执行上下文

- `.trae/gsd/workflows/ui-phase.md`
- `.trae/gsd/references/ui-brand.md`

## 参数

- **[阶段编号]**：可选，指定要生成UI-SPEC的阶段，默认自动检测

## 使用场景

- 前端阶段需要明确的UI设计契约时
- 需要在实现前研究UI模式和最佳实践时
- 需要验证UI设计规格的完整性时

注意：本skill在SOLO Coder中作为GSD工作流的辅助工具使用。

## 不适用场景

- 纯后端阶段不需要UI设计时
- UI设计已经非常明确不需要额外研究时

## 输出

- UI-SPEC.md文件，包含UI设计契约

## 依赖

- gsd-plan-phase（阶段需已规划）
