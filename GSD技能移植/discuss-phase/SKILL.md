---
name: gsd-discuss-phase
description: 当需要在规划前通过适应性提问收集阶段上下文时使用
---

# gsd-discuss-phase

## 描述

提取下游代理需要的实现决策 — 研究者和规划者将使用CONTEXT.md了解需要调查什么以及哪些选择已锁定。

**工作方式：**
1. 加载先前上下文（PROJECT.md、REQUIREMENTS.md、STATE.md、先前的CONTEXT.md文件）
2. 侦察代码库以发现可复用资产和模式
3. 分析阶段 — 跳过先前阶段已决定的灰色区域
4. 展示剩余灰色区域 — 用户选择哪些需要讨论
5. 深入每个选定区域直到满意
6. 创建CONTEXT.md，包含指导研究和规划的决策

**输出：** `{phase_num}-CONTEXT.md` — 决策足够清晰，下游代理无需再次询问用户即可行动

## 上下文

阶段编号：用户输入参数（必需）

上下文文件在工作流中使用 `init phase-op` 和 roadmap/state 工具调用解析。

## 指令

> **TRAE适配说明**：原文中引用的 `gsd-sdk` CLI工具在TRAE环境中不可用。在TRAE SOLO模式中，请直接读取 `.trae/gsd/planning/config.json` 和相关规划文件来获取配置信息，或使用TRAE的文件读取工具替代CLI查询。

**模式路由：**
```bash
DISCUSS_MODE=$(gsd-sdk query config-get workflow.discuss_mode 2>/dev/null || echo "discuss")
```

如果 `--assumptions` 在用户输入参数中：
读取并端到端执行 `.trae/gsd/workflows/list-phase-assumptions.md`。
在此停止。

否则，如果 `DISCUSS_MODE` 为 `"assumptions"`：
读取并端到端执行 `.trae/gsd/workflows/discuss-phase-assumptions.md`。

否则（`"discuss"` / 未设置 / 任何其他值）：
读取并端到端执行 `.trae/gsd/workflows/discuss-phase.md`。

**强制要求：** 在采取任何行动之前先读取适当的工作流文件。此命令文件中的objective和success_criteria部分是摘要 — 工作流文件包含完整的逐步过程及所有必需行为、配置检查和交互模式。不要从摘要即兴发挥。

**延迟加载：** `templates/context.md` 在活动工作流的 `write_context` 步骤中加载。`discuss-phase-power.md` 在检测到 `--power` 时在 `discuss-phase.md` 中加载。不要在此处加载。

## 执行上下文

工作流文件在下方 `<process>` 部分按需加载 — 不预先加载。
不要在读取模式路由指令之前预加载任何工作流文件。

## 参数

- `<phase>` — 阶段编号（必需）
- `--all` — 讨论所有灰色区域
- `--auto` — 自动回答灰色区域
- `--chain` — 链式讨论模式
- `--batch` — 批量讨论模式
- `--analyze` — 分析模式
- `--text` — 文本输出模式
- `--power` — 深度讨论模式
- `--assumptions` — 列出阶段假设

## 使用场景

- 阶段规划前需要明确实现决策
- 需要识别并讨论灰色区域
- 需要为下游研究和规划创建上下文文档

注意：本skill是GSD核心流程的一部分，在SOLO Coder中建议配合自定义智能体使用。GSD的讨论→规划→执行→验证循环与SOLO Coder的Plan模式互补。

## 不适用场景

- 阶段决策已明确无需讨论时
- 需要直接执行简单任务时（应使用fast skill）
- 尚未创建项目时（应先使用new-project skill）

## 输出

- `{phase_num}-CONTEXT.md` 上下文文档

## 依赖

- gsd-new-project（项目需先创建）
