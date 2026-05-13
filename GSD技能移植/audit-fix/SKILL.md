---
name: gsd-audit-fix
description: 当需要自动执行审计到修复流水线——发现问题、分类、修复、测试、提交时使用
---

# gsd-audit-fix

## 描述

运行审计，将发现分类为可自动修复和仅手动处理，然后自主修复可自动修复的问题，并进行测试验证和原子提交。

## 指令

端到端执行。

## 执行上下文

- `.trae/gsd/workflows/audit-fix.md`

## 参数

- `--source <audit-uat>` — 运行哪个审计（默认：audit-uat）
- `--severity <medium|high|all>` — 处理的最低严重级别（默认：medium）
- `--max N` — 最多修复的发现数量（默认：5）
- `--dry-run` — 仅分类发现不修复（显示分类表）

## 使用场景

- 审计发现问题后需要自动修复可修复项
- 需要对审计结果进行分类并批量处理
- 需要在修复前后进行测试验证

注意：本skill在SOLO Coder中作为GSD工作流的辅助工具使用。

## 不适用场景

- 需要人工判断的复杂问题修复
- 尚未运行审计时（应先运行audit-uat或audit-milestone）
- 仅需查看审计报告不需修复时

## 输出

- 修复后的代码文件
- 原子提交记录

## 依赖

- gsd-audit-uat（提供审计数据源）
