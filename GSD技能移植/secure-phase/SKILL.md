---
name: gsd-secure-phase
description: 当需要追溯验证已完成阶段的安全威胁缓解措施时使用
---

# gsd-secure-phase

## 描述

验证已完成阶段的威胁缓解措施。三种状态：
- (A) SECURITY.md存在 — 审计并验证缓解措施
- (B) 无SECURITY.md，PLAN.md中存在威胁模型 — 从产物运行
- (C) 阶段未执行 — 退出并给出指导

输出：更新后的SECURITY.md。

## 上下文

阶段：用户输入参数 — 可选，默认为最后完成的阶段。

## 指令

端到端执行。
保留所有工作流门控。

## 执行上下文

- `.trae/gsd/workflows/secure-phase.md`

## 参数

- **[阶段编号]**：可选，指定要审计的阶段，默认为最后完成的阶段

## 使用场景

- 阶段完成后需要验证安全威胁是否已正确缓解时
- 需要审计已有SECURITY.md的完整性时
- 安全合规要求需要追溯验证时

注意：本skill在SOLO Coder中作为GSD工作流的辅助工具使用。

## 不适用场景

- 阶段尚未执行时（应先完成execute-phase）
- 需要在规划阶段进行威胁建模时（应在plan-phase中处理）

## 输出

- 更新后的SECURITY.md文件

## 依赖

- gsd-execute-phase（阶段需已完成）
