---
name: gsd-execute-phase
description: 当需要使用基于波次的并行化执行阶段中所有计划时使用
---

# gsd-execute-phase

## 描述

使用基于波次的并行执行来执行阶段中的所有计划。

编排器保持精简：发现计划、分析依赖、分组为波次、生成子代理、收集结果。每个子代理加载完整的execute-plan上下文并处理自己的计划。

可选波次过滤器：
- `--wave N` 仅执行波次 `N`，用于节奏控制、配额管理或分阶段推出
- 阶段验证/完成仅在选定波次完成后没有未完成计划时发生

标志处理规则：
- 下面记录的可选标志是可用行为，不是隐含的活动行为
- 标志仅当其字面标记出现在用户输入参数中时才处于活动状态
- 如果记录的标志未出现在用户输入参数中，将其视为非活动状态

上下文预算：约15%编排器，每个子代理100%全新。

## 上下文

阶段：用户输入参数

**可用的可选标志（仅作文档记录 — 不自动激活）：**
- `--wave N` — 仅执行阶段中的波次 `N`。用于需要控制执行节奏或保持在用量限制内时。
- `--gaps-only` — 仅执行差距关闭计划（前置信息中带有 `gap_closure: true` 的计划）。在verify-work创建修复计划后使用。
- `--interactive` — 内联顺序执行计划（无子代理），任务间有用户检查点。较低的token使用量，结对编程风格。最适合小阶段、bug修复和验证差距。

**活动标志必须从用户输入参数推导：**
- `--wave N` 仅当字面 `--wave` 标记出现在用户输入参数中时才活动
- `--gaps-only` 仅当字面 `--gaps-only` 标记出现在用户输入参数中时才活动
- `--interactive` 仅当字面 `--interactive` 标记出现在用户输入参数中时才活动
- 如果这些标记都不出现，运行标准的全阶段执行流程，无标志特定过滤
- 不要仅因为标志在此提示中记录就推断其为活动状态

上下文文件在工作流中通过 `gsd-sdk query init.execute-phase` 和每个子代理的 `<files_to_read>` 块解析。

## 指令

> **TRAE适配说明**：原文中引用的 `gsd-sdk` CLI工具在TRAE环境中不可用。在TRAE SOLO模式中，请直接读取 `.trae/gsd/planning/config.json` 和相关规划文件来获取配置信息，或使用TRAE的文件读取工具替代CLI查询。

端到端执行。
保留所有工作流关卡（波次执行、检查点处理、验证、状态更新、路由）。

## 执行上下文

- `.trae/gsd/workflows/execute-phase.md`
- `.trae/gsd/references/ui-brand.md`

## 参数

- `<phase-number>` — 阶段编号（必需）
- `--wave N` — 仅执行指定波次
- `--gaps-only` — 仅执行差距关闭计划
- `--interactive` — 交互式顺序执行
- `--tdd` — TDD模式

## 使用场景

- 阶段讨论和规划完成后需要执行实现
- 需要并行执行多个计划以提高效率
- 需要分波次控制执行节奏

注意：本skill是GSD核心流程的一部分，在SOLO Coder中建议配合自定义智能体使用。GSD的讨论→规划→执行→验证循环与SOLO Coder的Plan模式互补。

## 不适用场景

- 尚未完成阶段规划时（应先使用plan-phase skill）
- 仅需执行简单任务时（应使用fast skill）
- 需要先讨论阶段决策时（应先使用discuss-phase skill）

## 输出

- 实现的代码文件
- SUMMARY.md阶段摘要
- VERIFICATION.md验证文档
- 更新的STATE.md状态

## 依赖

- gsd-discuss-phase（需先完成讨论）
- gsd-plan-phase（需先完成规划）
