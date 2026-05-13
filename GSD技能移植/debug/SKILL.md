---
name: gsd-debug
description: 当需要使用科学方法进行系统性调试，且支持跨上下文重置的持久状态时使用
---

# gsd-debug

## 描述

使用科学方法和子代理隔离来调试问题。

**编排器角色：** 收集症状、生成gsd-debugger子代理、处理检查点、生成续接。

**标志：**
- `--diagnose` — 仅诊断。返回根因报告而不应用修复。

**子命令：** `list` · `status <slug>` · `continue <slug>`

## 可用代理类型

有效的GSD子代理类型（使用精确名称 — 不要回退到'general-purpose'）：
- gsd-debug-session-manager — 在隔离上下文中管理调试检查点/续接循环
- gsd-debugger — 使用科学方法调查bug

## 上下文

用户输入：用户输入参数

在活动会话检查之前从用户输入参数解析子命令和标志：
- 如果用户输入参数以"list"开头：SUBCMD=list，无进一步参数
- 如果用户输入参数以"status "开头：SUBCMD=status，SLUG=剩余部分（去除空白）
- 如果用户输入参数以"continue "开头：SUBCMD=continue，SLUG=剩余部分（去除空白）
- 如果用户输入参数包含 `--diagnose`：SUBCMD=debug，diagnose_only=true，从描述中去除 `--diagnose`
- 否则：SUBCMD=debug，diagnose_only=false

检查活动会话（用于非list/status/continue流程）：
```bash
ls .trae/gsd/planning/debug/*.md 2>/dev/null | grep -v resolved | head -5
```

## 指令

端到端执行。

## 执行上下文

- `.trae/gsd/workflows/debug.md`

## 参数

- `list` — 列出所有调试会话
- `status <slug>` — 查看指定调试会话状态
- `continue <slug>` — 续接指定调试会话
- `--diagnose` — 仅诊断不修复
- `[issue description]` — 问题描述

## 使用场景

- 遇到需要系统性排查的bug
- 需要跨上下文重置保持调试状态
- 需要仅诊断根因而不自动修复

注意：本skill可独立于GSD流程使用，在SOLO Coder中直接调用即可。

## 不适用场景

- 简单的语法错误或明显问题（应使用fast skill）
- 需要代码审查而非调试时（应使用code-review skill）
- 需要性能优化而非bug修复时

## 输出

- 调试会话文件（`.trae/gsd/planning/debug/` 目录下）
- 根因报告（--diagnose模式）
- 修复后的代码（非--diagnose模式）

## 依赖

- 无（独立调试skill）
