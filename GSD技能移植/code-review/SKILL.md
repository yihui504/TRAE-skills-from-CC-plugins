---
name: gsd-code-review
description: 当需要审查阶段中变更的源文件以发现bug、安全问题和代码质量问题时使用
---

# gsd-code-review

## 描述

审查阶段中变更的源文件以发现bug、安全漏洞和代码质量问题。

生成gsd-code-reviewer子代理以指定深度级别分析代码。在阶段目录中生成REVIEW.md产物，包含按严重程度分类的发现。

参数：
- 阶段编号（必需）— 审查哪个阶段的变更（如"2"或"02"）
- `--depth=quick|standard|deep`（可选）— 审查深度级别，覆盖workflow.code_review_depth配置
  - quick：仅模式匹配（约2分钟）
  - standard：逐文件分析及语言特定检查（约5-15分钟，默认）
  - deep：跨文件分析包括导入图和调用链（约15-30分钟）
- `--files file1,file2,...`（可选）— 显式逗号分隔文件列表，跳过SUMMARY/git范围界定（范围界定的最高优先级）
- `--fix`（可选）— 审查完成后（或REVIEW.md已存在时），自动应用发现的修复。生成gsd-code-fixer子代理。接受子标志：
  - `--all` — 将Info级别发现纳入修复范围（默认：仅Critical + Warning）
  - `--auto` — 启用修复 + 重新审查迭代循环，最多3次迭代

输出：阶段目录中的 `{padded_phase}-REVIEW.md` + 发现的内联摘要

## 上下文

阶段：用户输入参数（第一个位置参数为阶段编号）

从用户输入参数解析的可选标志：
- `--depth=VALUE` — 深度覆盖（quick|standard|deep）。如提供，覆盖workflow.code_review_depth配置。
- `--files=file1,file2,...` — 显式文件列表覆盖。对文件范围界定具有最高优先级。提供时，工作流跳过SUMMARY.md提取和git diff回退。

上下文文件（CLAUDE.md、SUMMARY.md、阶段状态）在工作流中通过 `gsd-sdk query init.phase-op` 解析，并通过 `<files_to_read>` 块委托给子代理。

## 指令

> **TRAE适配说明**：原文中引用的 `gsd-sdk` CLI工具在TRAE环境中不可用。在TRAE SOLO模式中，请直接读取 `.trae/gsd/planning/config.json` 和相关规划文件来获取配置信息，或使用TRAE的文件读取工具替代CLI查询。

此命令是薄派发层。它解析参数并委托给工作流。

端到端执行。

工作流（非此命令）执行以下关卡：
- 阶段验证（配置关卡之前）
- 配置关卡检查（workflow.code_review）
- 文件范围界定（--files覆盖 > SUMMARY.md > git diff回退）
- 空范围检查（无文件则跳过）
- 子代理生成（gsd-code-reviewer）
- 结果呈现（内联摘要 + 下一步操作）

## 执行上下文

- `.trae/gsd/workflows/code-review.md`

## 参数

- `<phase-number>` — 阶段编号（必需）
- `--depth=quick|standard|deep` — 审查深度
- `--files file1,file2,...` — 显式文件列表
- `--fix` — 自动应用修复
- `--fix --all` — 包含Info级别修复
- `--fix --auto` — 修复+重新审查迭代

## 使用场景

- 阶段实现完成后需要代码审查
- 需要检查安全漏洞和代码质量问题
- 需要自动修复审查发现的问题

注意：本skill可独立于GSD流程使用，在SOLO Coder中直接调用即可。

## 不适用场景

- 代码尚未完成编写时
- 仅需快速语法检查时
- 需要人工深度架构审查时（此skill侧重自动化检查）

## 输出

- `{padded_phase}-REVIEW.md` 审查报告
- 内联发现摘要
- 可选的自动修复提交

## 依赖

- gsd-execute-phase（阶段需先完成执行以产生变更文件）
