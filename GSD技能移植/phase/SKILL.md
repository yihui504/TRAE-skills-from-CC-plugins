---
name: gsd-phase
description: 当需要在ROADMAP.md中对阶段进行增删改查操作时使用
---

# gsd-phase

## 描述

使用单个合并命令管理ROADMAP.md中的阶段。

模式路由：
- **默认**（无标志）：在当前里程碑末尾添加新的整数阶段 → add-phase工作流
- **--insert**：作为小数阶段（如72.1）在已有阶段之间插入紧急工作 → insert-phase工作流
- **--remove**：移除未来阶段并重新编号后续阶段 → remove-phase工作流
- **--edit**：就地编辑已有阶段的任何字段 → edit-phase工作流

## 上下文

参数：用户输入参数

解析用户输入参数的第一个标记：
- 如果是`--insert`：去除标志，将剩余部分（格式：<after-phase-number> <description>）传递给insert-phase工作流
- 如果是`--remove`：去除标志，将剩余部分（阶段编号）传递给remove-phase工作流
- 如果是`--edit`：去除标志，将剩余部分（phase-number [--force]）传递给edit-phase工作流
- 否则：将所有用户输入参数（阶段描述）传递给add-phase工作流

Roadmap和状态在工作流内通过`init phase-op`和有针对性的读取解析。

## 指令

1. 从用户输入参数中解析前导标志（如有）。
2. 根据上面的路由表加载并端到端执行适当的工作流。
3. 保留目标工作流的所有验证门控。

## 执行上下文

- `.trae/gsd/workflows/add-phase.md`
- `.trae/gsd/workflows/insert-phase.md`
- `.trae/gsd/workflows/remove-phase.md`
- `.trae/gsd/workflows/edit-phase.md`

## 参数

- `(无标志) <phase-description>`：在里程碑末尾添加新的整数阶段
- `--insert <after-phase-number> <description>`：插入小数阶段
- `--remove <phase-number>`：移除阶段并重新编号
- `--edit <phase-number> [--force]`：编辑已有阶段字段

## 使用场景

- 需要在里程碑中添加新阶段
- 需要在已有阶段之间插入紧急工作
- 需要移除或编辑已有阶段

注意：本skill在SOLO Coder中作为GSD工作流的辅助工具使用。

## 不适用场景

- 需要规划阶段内容（应使用gsd-plan-phase）
- 需要执行阶段（应使用gsd-execute-phase）
- 项目没有ROADMAP.md

## 输出

- 更新的ROADMAP.md
- 更新的STATE.md

## 依赖

- 需要已有的ROADMAP.md
