---
name: gsd-workspace
description: 当需要管理GSD工作空间——创建、列出或删除隔离的工作空间环境时使用
---

# gsd-workspace

## 描述

使用单一整合命令管理GSD工作空间。

模式路由：
- **--new**：创建隔离工作空间，包含仓库副本和独立的`.trae/gsd/planning/` → new-workspace工作流
- **--list**：列出活跃的GSD工作空间及其状态 → list-workspaces工作流
- **--remove**：删除GSD工作空间并清理worktree → remove-workspace工作流

## 上下文

用户输入参数：`[--new | --list | --remove] [name]`

解析用户输入参数的第一个标记：
- 如果是`--new`：去除该标志，将剩余部分（--name、--repos、--path、--strategy、--branch、--auto标志）传递给new-workspace工作流
- 如果是`--list`：执行list-workspaces工作流（无需参数）
- 如果是`--remove`：去除该标志，将剩余部分（工作空间名称）传递给remove-workspace工作流
- 否则（无标志）：显示用法 — 需要--new、--list或--remove之一

## 指令

1. 从用户输入参数中解析前导标志。
2. 根据上述路由表加载并端到端执行相应的工作流。
3. 保留目标工作流中的所有工作流门控（验证、审批、提交、路由）。

## 执行上下文

- `.trae/gsd/workflows/new-workspace.md`
- `.trae/gsd/workflows/list-workspaces.md`
- `.trae/gsd/workflows/remove-workspace.md`
- `.trae/gsd/references/ui-brand.md`

## 参数

- **--new**：创建新工作空间（支持--name、--repos、--path、--strategy、--branch、--auto标志）
- **--list**：列出所有活跃工作空间
- **--remove**：删除指定工作空间

| 标志 | 操作 | 工作流 |
|------|------|--------|
| --new | 使用worktree/clone策略创建工作空间 | new-workspace |
| --list | 扫描~/gsd-workspaces/，显示摘要表 | list-workspaces |
| --remove | 确认并删除工作空间目录 | remove-workspace |

## 使用场景

- 需要为不同功能分支创建隔离的工作空间时
- 需要同时管理多个并行工作流时
- 需要查看或清理现有工作空间时

注意：本skill在SOLO Coder中作为GSD工作流的辅助工具使用。

## 不适用场景

- 单一项目不需要工作空间隔离时
- 不了解worktree概念时（应先了解git worktree）

## 输出

- 根据模式：创建的工作空间目录、工作空间列表、或删除确认

## 依赖

- 无直接依赖其他GSD skill
