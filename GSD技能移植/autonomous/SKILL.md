---
name: gsd-autonomous
description: 当需要自主运行所有剩余阶段——每个阶段执行讨论→规划→执行时使用
---

# gsd-autonomous

## 描述

自主执行所有剩余的里程碑阶段。对每个阶段：讨论 → 规划 → 执行。仅在需要用户决策时暂停（灰色区域接受、阻碍项、验证请求）。

使用ROADMAP.md阶段发现和Skill()扁平调用执行每个阶段命令。所有阶段完成后：里程碑审计 → 完成 → 清理。

**创建/更新：**
- `.trae/gsd/planning/STATE.md` — 每个阶段后更新
- `.trae/gsd/planning/ROADMAP.md` — 每个阶段后更新进度
- 阶段产物 — 每个阶段的CONTEXT.md、PLANs、SUMMARYs

**完成后：** 里程碑完成并已清理。

## 上下文

可选标志：
- `--from N` — 从阶段N开始，而非第一个未完成阶段。
- `--to N` — 阶段N完成后停止（停止而非继续下一阶段）。
- `--only N` — 仅执行阶段N（单阶段模式）。
- `--interactive` — 内联运行讨论（问题不自动回答），然后将规划→执行派发为后台子代理。保持主上下文精简，同时保留用户对决策的输入。

项目上下文、阶段列表和状态在工作流中使用init命令（`gsd-sdk query init.milestone-op`、`gsd-sdk query roadmap.analyze`）解析。无需预先加载上下文。

## 指令

> **TRAE适配说明**：原文中引用的 `gsd-sdk` CLI工具在TRAE环境中不可用。在TRAE SOLO模式中，请直接读取 `.trae/gsd/planning/config.json` 和相关规划文件来获取配置信息，或使用TRAE的文件读取工具替代CLI查询。

端到端执行。
保留所有工作流关卡（阶段发现、逐阶段执行、阻碍项处理、进度显示）。

## 执行上下文

- `.trae/gsd/workflows/autonomous.md`
- `.trae/gsd/references/ui-brand.md`

## 参数

- `--from N` — 从阶段N开始
- `--to N` — 在阶段N完成后停止
- `--only N` — 仅执行阶段N
- `--interactive` — 交互模式，内联讨论，后台执行

## 使用场景

- 需要自动完成所有剩余里程碑阶段
- 有明确的阶段规划且无需频繁人工干预
- 需要在无人值守情况下推进项目

注意：本skill在SOLO Coder中作为GSD工作流的辅助工具使用。

## 不适用场景

- 需要频繁人工决策的复杂阶段
- 阶段间存在强依赖需逐步确认时
- 项目初期尚未建立路线图时

## 输出

- 所有阶段的完整产物（CONTEXT.md、PLAN.md、SUMMARY.md）
- 更新的STATE.md和ROADMAP.md
- 里程碑审计和归档

## 依赖

- gsd-discuss-phase
- gsd-plan-phase
- gsd-execute-phase
- gsd-audit-milestone
- gsd-complete-milestone
- gsd-cleanup
