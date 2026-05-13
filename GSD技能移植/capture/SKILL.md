---
name: gsd-capture
description: 当需要捕获想法、任务、笔记和种子到其目标位置时使用
---

# gsd-capture

## 描述

将想法、任务、笔记和种子捕获到GSD系统中适当的目标位置。

模式路由：
- **默认**（无标志）：捕获为结构化待办事项供后续工作 → add-todo工作流
- **--note**：零摩擦想法捕获（追加/列表/提升） → note工作流
- **--backlog**：将想法添加到待办停车场（999.x编号） → add-backlog工作流
- **--seed**：捕获带有触发条件的前瞻性想法 → plant-seed工作流
- **--list**：列出待办事项并选择一个进行处理 → check-todos工作流

| 标志 | 目标位置 | 工作流 |
|------|----------|--------|
| (无) | `.trae/gsd/planning/todos/` 中的结构化待办 | add-todo |
| --note | 带时间戳的笔记文件、列表或提升 | note |
| --backlog | ROADMAP.md待办部分（999.x） | add-backlog |
| --seed | `.trae/gsd/planning/seeds/SEED-NNN-slug.md` | plant-seed |
| --list | 交互式待办浏览器 + 动作路由 | check-todos |

## 上下文

参数：用户输入参数

解析用户输入参数的第一个标记：
- 如果是 `--note`：去除标志，将剩余部分传递给note工作流
- 如果是 `--backlog`：去除标志，将剩余部分传递给add-backlog工作流
- 如果是 `--seed`：去除标志，将剩余部分传递给plant-seed工作流
- 如果是 `--list`：将剩余部分（可选区域过滤器）传递给check-todos工作流
- 否则：将所有用户输入参数传递给add-todo工作流

## 指令

1. 从用户输入参数中解析前导标志（如有）。
2. 根据上述路由表加载并端到端执行适当的工作流。
3. 保留目标工作流的所有关卡（目录结构、重复检测、提交等）。

## 执行上下文

- `.trae/gsd/workflows/add-todo.md`
- `.trae/gsd/workflows/note.md`
- `.trae/gsd/workflows/add-backlog.md`
- `.trae/gsd/workflows/plant-seed.md`
- `.trae/gsd/workflows/check-todos.md`
- `.trae/gsd/references/ui-brand.md`

## 参数

- `--note` — 捕获为零摩擦笔记
- `--backlog` — 添加到待办停车场
- `--seed` — 捕获前瞻性想法
- `--list` — 列出并选择待办事项
- `[text]` — 捕获内容文本

## 使用场景

- 快速记录想法、任务或笔记到GSD系统
- 需要将灵感捕获为种子以便未来触发
- 需要查看并选择待办事项进行处理

注意：本skill在SOLO Coder中作为GSD工作流的辅助工具使用。

## 不适用场景

- 需要立即执行的任务（应使用fast或quick skill）
- 需要深入讨论的需求（应使用discuss-phase skill）
- 已有明确规划的阶段任务（应使用execute-phase skill）

## 输出

- 根据模式不同：待办文件、笔记文件、种子文件或待办列表

## 依赖

- 无（独立辅助skill）
