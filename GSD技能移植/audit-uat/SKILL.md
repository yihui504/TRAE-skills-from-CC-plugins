---
name: gsd-audit-uat
description: 当需要跨阶段审计所有未完成的UAT和验证项时使用
---

# gsd-audit-uat

## 描述

扫描所有阶段的待处理、已跳过、已阻止和需要人工处理的UAT项。与代码库交叉引用以检测过时文档。生成优先级排序的人工测试计划。

## 上下文

核心规划文件通过CLI在工作流中加载。

**范围：**
- Glob: `.trae/gsd/planning/phases/*/*-UAT.md`
- Glob: `.trae/gsd/planning/phases/*/*-VERIFICATION.md`

## 指令

端到端执行工作流。

## 执行上下文

- `.trae/gsd/workflows/audit-uat.md`

## 使用场景

- 需要全面了解所有阶段的UAT待办状态
- 需要检测过时的验证文档
- 需要生成人工测试计划以集中处理遗留UAT项

注意：本skill在SOLO Coder中作为GSD工作流的辅助工具使用。

## 不适用场景

- 只需检查单个阶段的验证状态时
- 项目初期尚无UAT文档时
- 需要自动修复问题时（应使用audit-fix）

## 输出

- 优先级排序的人工测试计划
- 过时文档检测报告

## 依赖

- gsd-execute-phase（阶段需先完成执行以产生UAT文档）
