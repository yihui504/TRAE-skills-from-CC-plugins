---
name: gsd-mvp-phase
description: 当需要将阶段规划为垂直MVP切片时使用——用户故事、SPIDR拆分、然后plan-phase
---

# gsd-mvp-phase

## 描述

引导用户完成阶段的MVP模式规划。该命令：

1. 提示输入"As a / I want to / So that"用户故事（三个结构化问题）
2. 运行SPIDR拆分检查——如果故事太大，引导完成Spike/Paths/Interfaces/Data/Rules并提供拆分为多个阶段的选项
3. 将`**Mode:** mvp`和重新格式化的`**Goal:**`写入阶段的ROADMAP.md部分
4. 委托给`gsd-plan-phase <N>`，该命令自动通过roadmap字段检测MVP模式

## 上下文

阶段编号：用户输入参数（必需——整数或小数如`2.1`）

该阶段必须已存在于ROADMAP.md中（通过gsd-new-project、gsd-phase创建）。此命令不创建新阶段——它将已有阶段转换为MVP模式。

## 指令

端到端执行`.trae/gsd/workflows/mvp-phase.md`中的mvp-phase工作流。
保留所有门控：阶段存在性、状态守卫（拒绝in_progress/completed）、用户故事格式验证、SPIDR拆分检查、ROADMAP写入确认、plan-phase委托。

## 执行上下文

- `.trae/gsd/workflows/mvp-phase.md`
- `.trae/gsd/references/spidr-splitting.md`
- `.trae/gsd/references/user-story-template.md`

## 参数

- `<phase-number>`：阶段编号（必需——整数或小数如2.1）

## 使用场景

- 需要将阶段规划为垂直MVP切片
- 需要编写用户故事并检查是否需要拆分
- 需要以功能切片方式（UI→API→DB）而非水平层方式组织任务

注意：本skill在SOLO Coder中作为GSD工作流的辅助工具使用。

## 不适用场景

- 阶段尚未在ROADMAP.md中创建
- 阶段已处于in_progress或completed状态
- 不需要MVP模式的常规规划

## 输出

- 更新的ROADMAP.md（添加MVP模式和目标）
- 委托给gsd-plan-phase生成PLAN.md

## 依赖

- gsd-plan-phase（规划阶段）
- gsd-new-project或gsd-phase（创建阶段）
