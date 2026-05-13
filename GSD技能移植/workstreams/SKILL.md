---
name: gsd-workstreams
description: 当需要管理并行工作流——列出、创建、切换、查看状态、进度、完成和恢复时使用
---

# gsd-workstreams

## 描述

管理并行里程碑工作的并行工作流。

## 上下文

用户输入参数：`[子命令] [参数]`

### 子命令

| 命令 | 描述 |
|------|------|
| `list` | 列出所有工作流及其状态 |
| `create <name>` | 创建新工作流 |
| `status <name>` | 一个工作流的详细状态 |
| `switch <name>` | 设置活跃工作流 |
| `progress` | 所有工作流的进度摘要 |
| `complete <name>` | 归档已完成的工作流 |
| `resume <name>` | 恢复工作流中的工作 |

## 指令

> **TRAE适配说明**：原文中引用的 `gsd-sdk` CLI工具在TRAE环境中不可用。在TRAE SOLO模式中，请直接读取 `.trae/gsd/planning/config.json` 和相关规划文件来获取配置信息，或使用TRAE的文件读取工具替代CLI查询。

### 步骤1：解析子命令

解析用户输入以确定要执行的工作流操作。
如果未给出子命令，默认为`list`。

### 步骤2：执行操作

#### list
运行：`gsd-sdk query workstream.list --raw --cwd "$CWD"`
以表格格式显示工作流，展示名称、状态、当前阶段和进度。

#### create
运行：`gsd-sdk query workstream.create <name> --raw --cwd "$CWD"`
创建后，显示新工作流路径并建议下一步：
- `gsd-new-milestone --ws <name>` 来设置里程碑

#### status
运行：`gsd-sdk query workstream.status <name> --raw --cwd "$CWD"`
显示详细的阶段分解和状态信息。

#### switch
运行：`gsd-sdk query workstream.set <name> --raw --cwd "$CWD"`
当运行时支持时，也为当前会话设置`GSD_WORKSTREAM`。
如果运行时暴露了会话标识符，GSD还会在会话本地存储活跃工作流，
以便并发会话不会互相覆盖。

#### progress
运行：`gsd-sdk query workstream.progress --raw --cwd "$CWD"`
显示所有工作流的进度概览。

#### complete
运行：`gsd-sdk query workstream.complete <name> --raw --cwd "$CWD"`
将工作流归档到milestones/。

#### resume
设置工作流为活跃，并建议`gsd-resume-work --ws <name>`。

### 步骤3：显示结果

将gsd-sdk query的JSON输出格式化为人类可读的显示。
在任何路由建议中包含`${GSD_WS}`标志。

## 执行上下文

- 无独立工作流文件（逻辑内联）

## 参数

- **list**：列出所有工作流
- **create <name>**：创建新工作流
- **status <name>**：查看指定工作流详细状态
- **switch <name>**：切换到指定工作流
- **progress**：查看所有工作流进度概览
- **complete <name>**：归档已完成的工作流
- **resume <name>**：恢复指定工作流的工作

## 使用场景

- 需要并行处理多个里程碑时
- 需要在不同工作流之间切换时
- 需要查看所有并行工作的整体进度时

注意：本skill在SOLO Coder中作为GSD工作流的辅助工具使用。

## 不适用场景

- 单一里程碑顺序开发时（不需要工作流管理）
- 工作流概念不适用的小型项目时

## 输出

- 工作流管理操作结果（列表/创建/切换/进度/完成/恢复）
- 格式化的工作流状态表

## 依赖

- gsd-resume-work（resume子命令建议使用）
- gsd-new-milestone（create后建议使用）
