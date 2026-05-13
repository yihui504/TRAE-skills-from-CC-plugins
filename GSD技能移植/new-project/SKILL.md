---
name: gsd-new-project
description: 当需要初始化新项目并进行深度上下文收集时使用
---

# gsd-new-project

## 描述

通过统一流程初始化新项目：提问 → 研究（可选） → 需求 → 路线图。

**创建：**
- `.trae/gsd/planning/PROJECT.md` — 项目上下文
- `.trae/gsd/planning/config.json` — 工作流偏好
- `.trae/gsd/planning/research/` — 领域研究（可选）
- `.trae/gsd/planning/REQUIREMENTS.md` — 范围需求
- `.trae/gsd/planning/ROADMAP.md` — 阶段结构
- `.trae/gsd/planning/STATE.md` — 项目记忆

**此命令之后：** 运行`gsd-plan-phase 1`开始执行。

## 上下文

**参数：**
- `--auto` — 自动模式。配置问题后，无需进一步交互即可运行研究 → 需求 → 路线图。期望通过@引用提供想法文档。

## 指令

端到端执行。
保留所有工作流门控（验证、审批、提交、路由）。

## 执行上下文

- `.trae/gsd/workflows/new-project.md`
- `.trae/gsd/references/questioning.md`
- `.trae/gsd/references/ui-brand.md`
- `.trae/gsd/templates/project.md`
- `.trae/gsd/templates/requirements.md`

## 参数

- `--auto`：自动模式，配置问题后无需交互即可完成研究→需求→路线图

## 使用场景

- 从零开始初始化新项目
- 需要通过深度提问收集项目上下文
- 需要生成完整的项目规划（需求+路线图）

注意：本skill是GSD核心流程的一部分，在SOLO Coder中建议配合自定义智能体使用。GSD的讨论→规划→执行→验证循环与SOLO Coder的Plan模式互补。

## 不适用场景

- 项目已存在（应使用gsd-new-milestone）
- 仅需查看或修改已有项目配置
- 不需要完整的项目初始化流程

## 输出

- `.trae/gsd/planning/PROJECT.md`
- `.trae/gsd/planning/config.json`
- `.trae/gsd/planning/REQUIREMENTS.md`
- `.trae/gsd/planning/ROADMAP.md`
- `.trae/gsd/planning/STATE.md`
- `.trae/gsd/planning/research/`（可选）

## 依赖

- gsd-plan-phase（后续规划阶段）
