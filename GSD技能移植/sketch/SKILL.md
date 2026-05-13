---
name: gsd-sketch
description: 当需要用一次性HTML原型探索UI/设计想法，或建议下一步要草图的内容（前沿模式）时使用
---

# gsd-sketch

## 描述

通过一次性HTML原型探索设计方向，在提交实现之前进行比较。
每个草图生成2-3个变体供比较。草图存放在`.trae/gsd/planning/sketches/`中，
集成GSD提交模式、状态跟踪和交接工作流。加载spike发现以将原型建立在真实数据形态和验证的交互模式上。

两种模式：
- **想法模式**（默认）— 描述一个设计想法进行草图
- **前沿模式**（无参数或"frontier"）— 分析现有草图景观并提出一致性和前沿草图

不需要`gsd-new-project` — 如需要会自动创建`.trae/gsd/planning/sketches/`。

## 上下文

设计想法：用户输入参数

**可用标志：**
- `--quick` — 跳过情绪/方向收集，直接进入分解和构建。当设计方向已经明确时使用。
- `--wrap-up` — 将草图设计发现打包为持久的项目技能，用于未来的构建对话。运行sketch-wrap-up工作流。

## 指令

解析用户输入参数的第一个标记：
- 如果是`--wrap-up`：去除该标志，端到端执行sketch-wrap-up工作流。
- 否则：端到端执行sketch工作流。

保留所有工作流门控（收集、分解、目标栈研究、变体评估、MANIFEST更新、提交模式）。

## 执行上下文

- `.trae/gsd/workflows/sketch.md`
- `.trae/gsd/workflows/sketch-wrap-up.md`
- `.trae/gsd/references/ui-brand.md`
- `.trae/gsd/references/sketch-theme-system.md`
- `.trae/gsd/references/sketch-interactivity.md`
- `.trae/gsd/references/sketch-tooling.md`
- `.trae/gsd/references/sketch-variant-patterns.md`

## 参数

- **[设计想法]**：描述要探索的设计想法
- **--quick**：跳过情绪/方向收集，直接构建
- **--wrap-up**：打包草图设计发现为项目技能
- **frontier**：分析现有草图景观并提出前沿草图

## 使用场景

- 在正式实现前需要快速探索UI设计方向时
- 想要比较多个设计变体时
- 需要将设计发现固化为可复用的项目技能时

注意：本skill在SOLO Coder中作为GSD工作流的辅助工具使用。

## 不适用场景

- 需要直接实现功能时（应使用execute-phase）
- 纯后端逻辑开发不需要UI探索时

## 输出

- `.trae/gsd/planning/sketches/` 目录中的HTML原型文件
- MANIFEST更新
- 使用`--wrap-up`时生成项目技能文件

## 依赖

- gsd-spike（草图可加载spike发现）
