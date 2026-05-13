---
name: gsd-import
description: 当需要导入外部计划文件并进行冲突检测时使用，支持从GSD-2项目反向迁移
---

# gsd-import

## 描述

将外部计划文件导入GSD规划系统，并与PROJECT.md中的决策进行冲突检测。

- **--from**：导入外部计划文件，检测冲突，写入为GSD PLAN.md，通过gsd-plan-checker验证。
- **--from-gsd2**：将GSD-2项目（`.gsd/`目录）反向迁移为GSD v1（`.trae/gsd/planning/`）格式。运行`gsd-tools.cjs from-gsd2`。传入`--path <dir>`可迁移不同路径下的项目。

## 上下文

用户输入参数

## 指令

> **TRAE适配说明**：原文中引用的 `gsd-tools` CLI工具在TRAE环境中不可用。在TRAE SOLO模式中，请直接读取 `.trae/gsd/planning/` 下的配置和数据文件，或使用TRAE的文件读取工具替代CLI操作。

如果`--from-gsd2`在用户输入参数中：
运行：`node "$HOME/.trae/gsd/bin/gsd-tools.cjs" from-gsd2`
如果提供了`--path <dir>`则传入。向用户展示迁移结果。
到此停止（不运行标准导入工作流）。

否则，端到端执行导入工作流。

## 执行上下文

- `.trae/gsd/workflows/import.md`
- `.trae/gsd/references/ui-brand.md`
- `.trae/gsd/references/gate-prompts.md`
- `.trae/gsd/references/doc-conflict-engine.md`

## 参数

- `--from <filepath>`：指定要导入的外部计划文件路径
- `--from-gsd2`：反向迁移GSD-2项目
- `--path <dir>`：指定迁移项目的路径（与--from-gsd2配合使用）

## 使用场景

- 需要将外部计划文件导入当前GSD项目
- 需要将GSD-2项目迁移到GSD v1格式
- 导入前需要检测与现有项目决策的冲突

注意：本skill在SOLO Coder中作为GSD工作流的辅助工具使用。

## 不适用场景

- 从零开始创建新项目（应使用gsd-new-project）
- 仅需查看现有计划（应直接读取文件）
- 不涉及外部计划导入的场景

## 输出

- 导入的PLAN.md文件（写入`.trae/gsd/planning/`）
- 冲突检测报告
- 迁移结果（--from-gsd2模式）

## 依赖

- gsd-plan-checker（验证导入的计划）
