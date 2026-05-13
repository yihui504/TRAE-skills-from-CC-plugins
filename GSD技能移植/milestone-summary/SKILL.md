---
name: gsd-milestone-summary
description: 当需要从里程碑产物生成综合项目摘要用于团队入职和审查时使用
---

# gsd-milestone-summary

## 描述

为团队入职和项目审查生成结构化的里程碑摘要。读取已完成的里程碑产物（ROADMAP、REQUIREMENTS、CONTEXT、SUMMARY、VERIFICATION文件），生成人类友好的概览，说明构建了什么、如何构建以及为什么。

目的：使新团队成员能够通过阅读一份文档并提问后续问题来理解已完成的项目。
输出：MILESTONE_SUMMARY写入`.trae/gsd/planning/reports/`，内联展示，可选交互式问答。

## 上下文

**项目文件：**
- `.trae/gsd/planning/ROADMAP.md`
- `.trae/gsd/planning/PROJECT.md`
- `.trae/gsd/planning/STATE.md`
- `.trae/gsd/planning/RETROSPECTIVE.md`
- `.trae/gsd/planning/milestones/v{version}-ROADMAP.md`（如已归档）
- `.trae/gsd/planning/milestones/v{version}-REQUIREMENTS.md`（如已归档）
- `.trae/gsd/planning/phases/*-*/`（SUMMARY.md、VERIFICATION.md、CONTEXT.md、RESEARCH.md）

**用户输入：**
- 版本：用户输入参数（可选——默认为当前/最新里程碑）

## 指令

端到端执行。

## 执行上下文

- `.trae/gsd/workflows/milestone-summary.md`

## 参数

- `[version]`：里程碑版本号（可选——默认为当前/最新里程碑）

## 使用场景

- 需要为新团队成员生成项目入职文档
- 需要回顾已完成里程碑的成果
- 需要一份综合的项目状态报告

注意：本skill在SOLO Coder中作为GSD工作流的辅助工具使用。

## 不适用场景

- 里程碑尚未完成
- 仅需查看单个阶段的状态
- 项目没有里程碑

## 输出

- `.trae/gsd/planning/reports/MILESTONE_SUMMARY-v{version}.md`
- 内联展示摘要
- 可选交互式问答

## 依赖

- 需要已完成的里程碑产物
