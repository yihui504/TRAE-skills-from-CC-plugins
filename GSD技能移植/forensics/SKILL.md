---
name: gsd-forensics
description: 当需要对失败的GSD工作流进行事后调查——诊断出了什么问题时使用
---

# gsd-forensics

## 描述

调查GSD工作流执行期间出了什么问题。分析git历史、`.trae/gsd/planning/`产物和文件系统状态以检测异常并生成结构化诊断报告。

目的：诊断失败或卡住的工作流，以便用户了解根因并采取纠正措施。
输出：取证报告保存到 `.trae/gsd/planning/forensics/`，内联呈现，可选创建issue。

## 上下文

**数据来源：**
- `git log`（最近提交、模式、时间间隔）
- `git status` / `git diff`（未提交的工作、冲突）
- `.trae/gsd/planning/STATE.md`（当前位置、会话历史）
- `.trae/gsd/planning/ROADMAP.md`（阶段范围和进度）
- `.trae/gsd/planning/phases/*/`（PLAN.md、SUMMARY.md、VERIFICATION.md、CONTEXT.md）
- `.trae/gsd/planning/reports/SESSION_REPORT.md`（上次会话结果）

**用户输入：**
- 问题描述：用户输入参数（可选 — 如未提供将询问）

## 指令

端到端执行。

## 执行上下文

- `.trae/gsd/workflows/forensics.md`

## 参数

- `[problem description]` — 问题描述（可选）

## 使用场景

- GSD工作流执行失败或卡住需要诊断
- 需要分析git历史和规划产物以找出异常
- 需要生成结构化诊断报告以理解根因

注意：本skill可独立于GSD流程使用，在SOLO Coder中直接调用即可。

## 不适用场景

- 工作流正常运行时
- 仅需查看项目状态时（应使用health skill）
- 需要修复bug而非诊断工作流问题时（应使用debug skill）

## 输出

- 取证报告保存到 `.trae/gsd/planning/forensics/report-{timestamp}.md`
- 内联呈现的发现、异常和建议
- 可选的GitHub issue创建

## 依赖

- 无（独立诊断skill）
