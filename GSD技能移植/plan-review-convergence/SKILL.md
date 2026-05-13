---
name: gsd-plan-review-convergence
description: 当需要跨AI计划收敛循环时使用——用审查反馈重新规划直到无HIGH级别问题
---

# gsd-plan-review-convergence

## 描述

跨AI计划收敛循环——gsd-review和gsd-planner的外部修订门控。
重复执行：用外部AI CLI审查计划 → 如果发现HIGH级别问题 → 用--reviews反馈重新规划 → 重新审查。当无HIGH级别问题或达到最大循环次数时停止。

**流程：** Agent→Skill("gsd-plan-phase") → Agent→Skill("gsd-review") → 检查HIGHs → Agent→Skill("gsd-plan-phase --reviews") → Agent→Skill("gsd-review") → ... → 收敛或升级

用外部AI审查器（codex、gemini等）替代gsd-plan-phase内部的gsd-plan-checker。每步在隔离的Agent内运行，调用对应的已有Skill——编排器仅做循环控制。

**编排器角色：** 解析参数，验证阶段，为已有Skill生成Agent，检查HIGHs，停滞检测，升级门控。

## 上下文

阶段编号：从用户输入参数中提取（必需）

**参数：**
- `--codex` — 使用Codex CLI作为审查器（如未指定审查器则为默认）
- `--gemini` — 使用Gemini CLI作为审查器
- `--claude` — 使用Claude CLI作为审查器（独立会话）
- `--opencode` — 使用OpenCode作为审查器
- `--ollama` — 使用本地Ollama服务器作为审查器（OpenAI兼容，默认主机`http://localhost:11434`；通过`review.models.ollama`配置模型）
- `--lm-studio` — 使用本地LM Studio服务器作为审查器（OpenAI兼容，默认主机`http://localhost:1234`；通过`review.models.lm_studio`配置模型）
- `--llama-cpp` — 使用本地llama.cpp服务器作为审查器（OpenAI兼容，默认主机`http://localhost:8080`；通过`review.models.llama_cpp`配置模型）
- `--all` — 使用所有可用的CLI和运行中的本地模型服务器
- `--max-cycles N` — 最大重新规划→审查循环次数（默认：3）

**功能门控：** 此命令需要`workflow.plan_review_convergence=true`。启用方式：
`gsd config-set workflow.plan_review_convergence true`

## 指令

端到端执行。
保留所有工作流门控（预检、修订循环、停滞检测、升级）。

## 执行上下文

- `.trae/gsd/workflows/plan-review-convergence.md`
- `.trae/gsd/references/revision-loop.md`
- `.trae/gsd/references/gates.md`
- `.trae/gsd/references/agent-contracts.md`

## 参数

- `<phase>`：阶段编号（必需）
- `--codex`：使用Codex CLI审查
- `--gemini`：使用Gemini CLI审查
- `--claude`：使用Claude CLI审查
- `--opencode`：使用OpenCode审查
- `--ollama`：使用本地Ollama审查
- `--lm-studio`：使用本地LM Studio审查
- `--llama-cpp`：使用本地llama.cpp审查
- `--all`：使用所有可用的审查器
- `--max-cycles N`：最大循环次数（默认3）
- `--text`：纯文本模式
- `--ws <name>`：工作区名称

## 使用场景

- 需要用多个AI审查器验证计划质量
- 需要通过跨AI审查收敛到高质量计划
- 单一审查器不足以发现所有问题

注意：本skill在SOLO Coder中作为GSD工作流的辅助工具使用。

## 不适用场景

- 没有可用的外部AI CLI
- 不需要跨AI验证的简单计划
- 功能门控未启用

## 输出

- 收敛后的PLAN.md
- REVIEWS.md（审查反馈记录）
- 收敛/升级状态报告

## 依赖

- gsd-plan-phase（规划阶段）
- gsd-review（审查计划）
- 外部AI CLI（codex、gemini等）
