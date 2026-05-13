---
name: gsd-manager
description: 当需要在一个终端中交互式管理多个阶段时使用
---

# gsd-manager

## 描述

单终端命令中心，用于管理里程碑。显示所有阶段的仪表板（带可视化状态指示器），推荐最优下一步操作，并分派工作——discuss内联运行，plan/execute作为后台代理运行。

为希望在一个终端中跨阶段并行化工作的高级用户设计：在一个阶段讨论的同时，另一个阶段在后台规划或执行。

**创建/更新：**
- 不直接创建文件——通过Skill()和后台Task代理分派到已有的GSD命令。
- 读取`.trae/gsd/planning/STATE.md`、`.trae/gsd/planning/ROADMAP.md`、阶段目录获取状态。

**之后：** 用户完成管理后退出，或所有阶段完成并建议里程碑生命周期。

## 上下文

无需参数。需要活跃的里程碑（包含ROADMAP.md和STATE.md）。

项目上下文、阶段列表、依赖和建议在工作流内通过`gsd-sdk query init.manager`解析。无需前置上下文加载。

## 指令

> **TRAE适配说明**：原文中引用的 `gsd-sdk` CLI工具在TRAE环境中不可用。在TRAE SOLO模式中，请直接读取 `.trae/gsd/planning/config.json` 和相关规划文件来获取配置信息，或使用TRAE的文件读取工具替代CLI查询。

如果`--analyze-deps`在用户输入参数中：
读取并端到端执行`~/.trae/gsd/workflows/analyze-dependencies.md`。

端到端执行。
维护仪表板刷新循环，直到用户退出或所有阶段完成。

## 执行上下文

- `.trae/gsd/workflows/manager.md`
- `.trae/gsd/references/ui-brand.md`

## 参数

- `--analyze-deps`：分析阶段间依赖关系

## 使用场景

- 需要在一个终端中查看和管理多个阶段的进度
- 需要并行化跨阶段的工作
- 需要获取下一步操作建议

注意：本skill在SOLO Coder中作为GSD工作流的辅助工具使用。

## 不适用场景

- 项目没有活跃的里程碑
- 仅需管理单个阶段（应直接使用对应阶段skill）
- 不需要并行化工作

## 输出

- 交互式仪表板显示
- 阶段状态和建议
- 分派到其他GSD命令

## 依赖

- gsd-discuss-phase
- gsd-plan-phase
- gsd-execute-phase
