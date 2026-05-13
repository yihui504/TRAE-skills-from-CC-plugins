---
name: gsd-explore
description: 当需要通过苏格拉底式提问进行开放式构思和想法路由时使用
---

# gsd-explore

## 描述

开放式苏格拉底式构思会话。通过探究性问题引导开发者探索想法，可选生成研究，然后将输出路由到适当的GSD产物（笔记、待办、种子、研究问题、需求或新阶段）。

接受可选的主题参数：`gsd-explore authentication strategy`

## 指令

端到端执行。

## 执行上下文

- `.trae/gsd/workflows/explore.md`

## 使用场景

- 有模糊想法需要通过提问来澄清
- 需要探索技术方案的可行性
- 需要将想法路由到合适的GSD产物

注意：本skill在SOLO Coder中作为GSD工作流的辅助工具使用。

## 不适用场景

- 已有明确需求无需探索时
- 需要立即执行的任务（应使用fast skill）
- 需要正式的阶段讨论（应使用discuss-phase skill）

## 输出

- 根据路由结果：笔记、待办、种子、研究问题、需求或新阶段

## 依赖

- 无（独立辅助skill）
