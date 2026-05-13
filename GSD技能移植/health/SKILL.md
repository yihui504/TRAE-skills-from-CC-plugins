---
name: gsd-health
description: 当需要诊断规划目录健康状况并可选修复问题时使用
---

# gsd-health

## 描述

验证 `.trae/gsd/planning/` 目录完整性并报告可操作的问题。检查缺失文件、无效配置、不一致状态和孤立计划。

`--context` 运行正交检查：运行会话的上下文利用率。工作流请求模型的tokensUsed + contextWindow，调用 `gsd-sdk query validate.context`，并渲染三种状态之一：

| 利用率 | 状态 | 动作 |
|--------|------|------|
| < 60% | healthy | 无需操作 — 上下文充裕 |
| 60% – 70% | warning | 建议运行 `gsd-thread` 以重新开始 |
| >= 70% | critical | 推理质量可能在断裂点之后下降 |

## 指令

> **TRAE适配说明**：原文中引用的 `gsd-sdk` CLI工具在TRAE环境中不可用。在TRAE SOLO模式中，请直接读取 `.trae/gsd/planning/config.json` 和相关规划文件来获取配置信息，或使用TRAE的文件读取工具替代CLI查询。

端到端执行。
从参数中解析 `--repair` 和 `--context` 标志并传递给工作流。

## 执行上下文

- `.trae/gsd/workflows/health.md`

## 参数

- `--repair` — 自动修复发现的问题
- `--context` — 检查上下文利用率

## 使用场景

- 需要检查GSD规划目录的完整性
- 遇到工作流异常需要诊断目录状态
- 需要检查当前会话的上下文利用率

注意：本skill可独立于GSD流程使用，在SOLO Coder中直接调用即可。

## 不适用场景

- 项目正常运行无需诊断时
- 需要调试具体bug时（应使用debug skill）
- 需要诊断工作流失败原因时（应使用forensics skill）

## 输出

- 健康检查报告（缺失文件、无效配置、不一致状态、孤立计划）
- 上下文利用率状态（--context模式）
- 修复后的文件（--repair模式）

## 依赖

- 无（独立诊断skill）
