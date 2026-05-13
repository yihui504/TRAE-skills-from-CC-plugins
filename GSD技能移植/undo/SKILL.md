---
name: gsd-undo
description: 当需要安全回滚GSD阶段或计划提交时使用——使用阶段清单进行依赖检查
---

# gsd-undo

## 描述

安全git回滚 — 使用阶段清单回滚GSD阶段或计划提交，带有依赖检查和执行前的确认门控。

三种模式：
- **--last N**：显示最近的GSD提交供交互式选择
- **--phase NN**：回滚一个阶段的所有提交（清单 + git日志回退）
- **--plan NN-MM**：回滚特定计划的所有提交

## 上下文

用户输入参数：`--last N | --phase NN | --plan NN-MM`

## 指令

端到端执行。

## 执行上下文

- `.trae/gsd/workflows/undo.md`
- `.trae/gsd/references/ui-brand.md`
- `.trae/gsd/references/gate-prompts.md`

## 参数

- **--last N**：显示最近N个GSD提交供交互式选择
- **--phase NN**：回滚指定阶段的所有提交
- **--plan NN-MM**：回滚指定计划的所有提交

## 使用场景

- 阶段执行出错需要回滚时
- 需要撤销最近的GSD提交时
- 需要安全地回退到之前的项目状态时

注意：本skill在SOLO Coder中作为GSD工作流的辅助工具使用。

## 不适用场景

- 非GSD管理的提交需要回滚时（应直接使用git命令）
- 不确定回滚影响范围时（应先查看stats或progress）

## 输出

- git回滚操作结果
- 依赖检查报告

## 依赖

- 无直接依赖其他GSD skill
