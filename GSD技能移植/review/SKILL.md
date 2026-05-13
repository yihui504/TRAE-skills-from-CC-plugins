---
name: gsd-review
description: 当需要请求外部AI CLI对阶段计划进行跨AI同行评审时使用
---

# gsd-review

## 描述

调用外部AI CLI（Gemini、Claude、Codex、OpenCode、Qwen Code、Cursor）独立审查阶段计划。
生成结构化的REVIEWS.md，包含每个审查者的反馈，可通过`gsd-plan-phase --reviews`反馈到规划中。

**流程：** 检测CLI → 构建审查提示 → 调用每个CLI → 收集响应 → 写入REVIEWS.md

## 上下文

阶段编号：从用户输入参数中提取（必需）

**标志：**
- `--gemini` — 包含Gemini CLI审查
- `--claude` — 包含Claude CLI审查（使用独立会话）
- `--codex` — 包含Codex CLI审查
- `--opencode` — 包含OpenCode审查（使用用户OpenCode配置中的模型）
- `--qwen` — 包含Qwen Code审查（阿里Qwen模型）
- `--cursor` — 包含Cursor代理审查
- `--all` — 包含所有可用CLI

## 指令

端到端执行。

## 执行上下文

- `.trae/gsd/workflows/review.md`

## 参数

- **--phase N**：指定要审查的阶段编号（必需）
- **--gemini**：包含Gemini CLI审查
- **--claude**：包含Claude CLI审查
- **--codex**：包含Codex CLI审查
- **--opencode**：包含OpenCode审查
- **--qwen**：包含Qwen Code审查
- **--cursor**：包含Cursor代理审查
- **--all**：包含所有可用CLI

## 使用场景

- 阶段计划完成后需要多角度审查时
- 想要获取不同AI模型的独立评审意见时
- 计划复杂度高，需要交叉验证时

注意：本skill在SOLO Coder中作为GSD工作流的辅助工具使用。

## 不适用场景

- 没有安装任何外部AI CLI时
- 阶段尚未规划完成时（应先完成plan-phase）

## 输出

- REVIEWS.md文件，包含各审查者的结构化反馈

## 依赖

- gsd-plan-phase（审查结果可反馈到规划中）
