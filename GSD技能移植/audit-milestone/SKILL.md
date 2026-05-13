---
name: gsd-audit-milestone
description: 当需要在归档前审计里程碑完成情况与原始意图的符合度时使用
---

# gsd-audit-milestone

## 描述

验证里程碑是否达成了其完成定义。检查需求覆盖率、跨阶段集成和端到端流程。

**此命令即为编排器。** 读取现有的VERIFICATION.md文件（阶段在execute-phase期间已验证），汇总技术债务和延迟差距，然后生成集成检查器用于跨阶段连接。

## 上下文

版本：用户输入参数（可选 — 默认为当前里程碑）

核心规划文件在工作流中解析（`init milestone-op`）并按需加载。

**已完成的工作：**
- Glob: `.trae/gsd/planning/phases/*/*-SUMMARY.md`
- Glob: `.trae/gsd/planning/phases/*/*-VERIFICATION.md`

## 指令

端到端执行。
保留所有工作流关卡（范围确定、验证读取、集成检查、需求覆盖率、路由）。

## 执行上下文

- `.trae/gsd/workflows/audit-milestone.md`

## 参数

- `[version]` — 可选的里程碑版本号，默认为当前里程碑

## 使用场景

- 里程碑所有阶段完成后需要验证整体达成情况
- 归档前需要检查需求覆盖率和跨阶段集成
- 需要发现技术债务和延迟差距

注意：本skill在SOLO Coder中作为GSD工作流的辅助工具使用。

## 不适用场景

- 里程碑尚有未完成阶段时
- 仅需检查单个阶段时（应使用verify-work）
- 项目初期尚未有里程碑时

## 输出

- 里程碑审计报告（MILESTONE-AUDIT.md）
- 需求覆盖率分析
- 跨阶段集成问题列表

## 依赖

- gsd-execute-phase（阶段需先完成执行）
- gsd-verify-work（验证文档作为审计来源）
