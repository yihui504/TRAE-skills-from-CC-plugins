---
name: gsd-spike
description: 当需要通过体验式探索验证想法，或建议下一步要探索的内容（前沿模式）时使用
---

# gsd-spike

## 描述

通过体验式探索验证想法 — 构建专注的实验来感受未来应用的各个部分，
验证可行性，并为真正的构建产生经过验证的知识。
Spike存放在`.trae/gsd/planning/spikes/`中，集成GSD提交模式、状态跟踪和交接工作流。

两种模式：
- **想法模式**（默认）— 描述一个想法进行spike
- **前沿模式**（无参数或"frontier"）— 分析现有spike景观并提出集成和前沿spike

不需要`gsd-new-project` — 如需要会自动创建`.trae/gsd/planning/spikes/`。

## 上下文

想法：用户输入参数

**可用标志：**
- `--quick` — 跳过分解/对齐，直接构建。当你已经知道要spike什么时使用。
- `--text` — 使用纯文本编号列表代替向用户提问（用于非Claude运行时）。
- `--wrap-up` — 将spike发现打包为持久的项目技能，用于未来的构建对话。运行spike-wrap-up工作流。

## 指令

解析用户输入参数的第一个标记：
- 如果是`--wrap-up`：去除该标志，执行spike-wrap-up工作流
- 否则：将全部用户输入参数作为想法传递给spike工作流端到端执行。

保留所有工作流门控（先前spike检查、分解、研究、风险排序、可观测性评估、验证、MANIFEST更新、提交模式）。

## 执行上下文

- `.trae/gsd/workflows/spike.md`
- `.trae/gsd/workflows/spike-wrap-up.md`
- `.trae/gsd/references/ui-brand.md`

## 参数

- **[想法]**：描述要验证的想法
- **--quick**：跳过分解/对齐，直接构建
- **--text**：使用纯文本列表代替向用户提问
- **--wrap-up**：打包spike发现为项目技能
- **frontier**：分析现有spike景观并提出前沿spike

## 使用场景

- 在正式开发前需要验证技术可行性时
- 想要快速探索某个想法但不确定是否可行时
- 需要将探索发现固化为可复用的项目知识时

注意：本skill在SOLO Coder中作为GSD工作流的辅助工具使用。

## 不适用场景

- 需求明确且可行性无争议时（应直接进入plan-phase）
- 需要完整功能实现时（应使用execute-phase）

## 输出

- `.trae/gsd/planning/spikes/` 目录中的实验代码
- MANIFEST更新
- 使用`--wrap-up`时生成项目技能文件

## 依赖

- 无直接依赖其他GSD skill
