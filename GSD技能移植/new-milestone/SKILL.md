---
name: gsd-new-milestone
description: 当需要开始新的里程碑周期时使用——更新PROJECT.md并路由到需求收集
---

# gsd-new-milestone

## 描述

开始新里程碑：提问 → 研究（可选） → 需求 → 路线图。

new-project的棕地等价物。项目已存在，PROJECT.md有历史。收集"下一步是什么"，更新PROJECT.md，然后运行需求 → 路线图循环。

**创建/更新：**
- `.trae/gsd/planning/PROJECT.md` — 更新新里程碑目标
- `.trae/gsd/planning/research/` — 领域研究（可选，仅新功能）
- `.trae/gsd/planning/REQUIREMENTS.md` — 此里程碑的范围需求
- `.trae/gsd/planning/ROADMAP.md` — 阶段结构（延续编号）
- `.trae/gsd/planning/STATE.md` — 为新里程碑重置

**之后：** 运行`gsd-plan-phase [N]`开始执行。

## 上下文

里程碑名称：用户输入参数（可选——如未提供将提示输入）

项目和里程碑上下文文件在工作流内解析（`init new-milestone`），在使用子代理时通过`<files_to_read>`块委托。

## 指令

端到端执行。
保留所有工作流门控（验证、提问、研究、需求、路线图审批、提交）。

## 执行上下文

- `.trae/gsd/workflows/new-milestone.md`
- `.trae/gsd/references/questioning.md`
- `.trae/gsd/references/ui-brand.md`
- `.trae/gsd/templates/project.md`
- `.trae/gsd/templates/requirements.md`

## 参数

- `[milestone name]`：里程碑名称（可选——如未提供将提示输入），例如`v1.1 Notifications`

## 使用场景

- 已有项目需要开始新的里程碑
- 需要收集新功能需求并规划路线图
- 项目进入下一阶段开发

注意：本skill是GSD核心流程的一部分，在SOLO Coder中建议配合自定义智能体使用。GSD的讨论→规划→执行→验证循环与SOLO Coder的Plan模式互补。

## 不适用场景

- 全新项目（应使用gsd-new-project）
- 里程碑尚未完成（应先完成当前里程碑）
- 仅需查看项目状态

## 输出

- `.trae/gsd/planning/PROJECT.md`（更新）
- `.trae/gsd/planning/REQUIREMENTS.md`（新建）
- `.trae/gsd/planning/ROADMAP.md`（更新）
- `.trae/gsd/planning/STATE.md`（重置）
- `.trae/gsd/planning/research/`（可选）

## 依赖

- gsd-plan-phase（后续规划阶段）
