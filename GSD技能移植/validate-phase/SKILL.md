---
name: gsd-validate-phase
description: 当需要追溯审计并填补已完成阶段的Nyquist验证缺口时使用
---

# gsd-validate-phase

## 描述

审计已完成阶段的Nyquist验证覆盖。三种状态：
- (A) VALIDATION.md存在 — 审计并填补缺口
- (B) 无VALIDATION.md，SUMMARY.md存在 — 从产物重建
- (C) 阶段未执行 — 退出并给出指导

输出：更新后的VALIDATION.md + 生成的测试文件。

## 上下文

阶段：用户输入参数 — 可选，默认为最后完成的阶段。

## 指令

端到端执行。
保留所有工作流门控。

## 执行上下文

- `.trae/gsd/workflows/validate-phase.md`

## 参数

- **[阶段编号]**：可选，指定要审计验证覆盖的阶段，默认为最后完成的阶段

## 使用场景

- 阶段完成后需要审计验证覆盖是否充分时
- 需要填补验证缺口并生成缺失的测试时
- 需要从阶段产物重建验证文档时

注意：本skill在SOLO Coder中作为GSD工作流的辅助工具使用。

## 不适用场景

- 阶段尚未执行时（应先完成execute-phase）
- 需要在规划阶段定义验证标准时（应在plan-phase中处理）

## 输出

- 更新后的VALIDATION.md文件
- 生成的测试文件

## 依赖

- gsd-execute-phase（阶段需已完成）
