---
name: gsd-ai-integration-phase
description: 当需要为涉及AI系统构建的阶段生成AI-SPEC.md设计合约时使用
---

# gsd-ai-integration-phase

## 描述

为涉及AI系统开发的阶段创建AI设计合约（AI-SPEC.md）。
编排 gsd-framework-selector → gsd-ai-researcher → gsd-domain-researcher → gsd-eval-planner。
流程：选择框架 → 研究文档 → 研究领域 → 设计评估策略 → 完成

## 上下文

阶段编号：用户输入参数 — 可选，省略时自动检测下一个未规划的阶段。

## 指令

端到端执行。
保留所有工作流关卡。

## 执行上下文

- `.trae/gsd/workflows/ai-integration-phase.md`
- `.trae/gsd/references/ai-frameworks.md`
- `.trae/gsd/references/ai-evals.md`

## 参数

- `[phase number]` — 可选的阶段编号，省略时自动检测

## 使用场景

- 阶段涉及AI/ML系统开发需要设计合约
- 需要选择AI框架并研究其文档
- 需要为AI功能设计评估策略

注意：本skill在SOLO Coder中作为GSD工作流的辅助工具使用。

## 不适用场景

- 非AI相关的常规功能开发阶段
- 已有AI-SPEC.md且无需更新时
- 纯前端或纯后端API开发阶段

## 输出

- AI-SPEC.md设计合约文件

## 依赖

- gsd-discuss-phase（需先完成讨论阶段）
