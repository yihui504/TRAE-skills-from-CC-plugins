---
name: gsd-spec-phase
description: 当需要在discuss-phase之前通过歧义评分明确阶段交付内容时使用；生成SPEC.md
---

# gsd-spec-phase

## 描述

通过结构化苏格拉底式提问和量化歧义评分来明确阶段需求。

**在工作流中的位置：** `spec-phase → discuss-phase → plan-phase → execute-phase → verify`

**工作原理：**
1. 加载阶段上下文（PROJECT.md、REQUIREMENTS.md、ROADMAP.md、STATE.md）
2. 侦察代码库 — 在提问前了解当前状态
3. 运行苏格拉底式访谈循环（最多6轮，轮换视角）
4. 每轮后在4个加权维度上评分歧义
5. 门控：歧义 ≤ 0.20 且所有维度满足最低要求 → 写入SPEC.md
6. 提交SPEC.md — discuss-phase在下次运行时自动拾取

**输出：** `{phase_dir}/{padded_phase}-SPEC.md` — 在discuss-phase处理"如何做"之前锁定"做什么/为什么"的可证伪需求

## 上下文

阶段编号：用户输入参数（必需）

**标志：**
- `--auto` — 跳过交互式问题；Claude选择推荐默认值并写入SPEC.md
- `--text` — 使用纯文本编号列表代替TUI菜单（`/rc`远程会话必需）

上下文文件在工作流中使用`init phase-op`解析。

## 指令

端到端执行。

**强制要求：** 在采取任何操作之前先读取工作流文件。工作流包含完整的逐步流程，包括苏格拉底式访谈循环、歧义评分门控和SPEC.md生成。不要从上面的目标摘要中即兴发挥。

## 执行上下文

- `.trae/gsd/workflows/spec-phase.md`
- `.trae/gsd/templates/spec.md`

## 参数

- **<阶段编号>**：必需，指定要明确需求的阶段
- **--auto**：跳过交互式问题，使用推荐默认值
- **--text**：使用纯文本列表代替TUI菜单

## 使用场景

- 阶段需求模糊，需要通过结构化提问明确"做什么"时
- 想要在规划前量化需求歧义程度时
- 需要生成可证伪的需求规格（SPEC.md）时

注意：本skill是GSD核心流程的一部分，在SOLO Coder中建议配合自定义智能体使用。GSD的讨论→规划→执行→验证循环与SOLO Coder的Plan模式互补。

## 不适用场景

- 需求已经非常明确时（可直接进入discuss-phase）
- 阶段尚未在ROADMAP中定义时

## 输出

- `{phase_dir}/{padded_phase}-SPEC.md` 文件，包含可证伪需求、明确边界和验收标准

## 依赖

- gsd-discuss-phase（SPEC.md会被discuss-phase自动拾取）
- gsd-plan-phase（后续规划依赖SPEC.md）
