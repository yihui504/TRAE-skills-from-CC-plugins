---
name: gsd-update
description: 当需要更新GSD到最新版本并显示变更日志时使用
---

# gsd-update

## 描述

检查GSD更新，如果有可用则安装，并显示变更内容。

路由到update工作流，处理：
- 版本检测（本地 vs 全局安装）
- npm版本检查
- 变更日志获取和显示
- 用户确认（含全新安装警告）
- 更新执行和缓存清除
- 重启提醒

## 上下文

用户输入参数：`[--sync | --reapply]`

## 指令

解析用户输入参数的第一个标记：
- 如果是`--sync`：去除该标志，执行sync-skills工作流（传递剩余参数如--from/--to/--dry-run/--apply）。
- 如果是`--reapply`：去除该标志，执行reapply-patches工作流。
- 否则：端到端执行update工作流。

## 执行上下文

- `.trae/gsd/workflows/update.md`
- `.trae/gsd/workflows/sync-skills.md`
- `.trae/gsd/workflows/reapply-patches.md`

## 参数

- **--sync**：跨运行时根目录同步管理的GSD技能，使多运行时用户在更新后保持一致。运行sync-skills工作流（支持--from、--to、--dry-run、--apply标志）。
- **--reapply**：在GSD更新后重新应用本地修改。使用三方比较（原始基线、用户修改备份、新安装版本）来合并用户自定义。运行reapply-patches工作流。
- **（无标志）**：标准更新 — 检查新版本、显示变更日志、安装。

## 使用场景

- 需要检查并安装GSD最新版本时
- 更新后需要跨运行时同步技能时
- 更新后需要重新应用本地自定义修改时

注意：本skill在SOLO Coder中作为GSD工作流的辅助工具使用。

## 不适用场景

- 项目正在执行关键阶段时（应先完成当前工作再更新）
- 不了解更新影响时（应先查看变更日志）

## 输出

- GSD更新结果
- 变更日志显示
- 使用`--sync`时同步结果
- 使用`--reapply`时补丁重新应用结果

## 依赖

- 无直接依赖其他GSD skill
