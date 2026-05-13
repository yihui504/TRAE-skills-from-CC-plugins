---
name: gsd-config
description: 当需要配置GSD设置——工作流开关、高级旋钮、集成和模型配置时使用
---

# gsd-config

## 描述

通过单一整合命令交互式配置GSD设置。

模式路由：
- **默认**（无标志）：常用开关（模型、研究、plan_check、验证器、分支） → settings工作流
- **--advanced**：高级用户旋钮（规划调优、超时、分支模板、跨AI执行） → settings-advanced工作流
- **--integrations**：第三方API密钥、代码审查CLI路由、代理技能注入 → settings-integrations工作流
- **--profile <name>**：切换模型配置（quality|balanced|budget|inherit） → set-profile（内联）

| 标志 | 动作 | 工作流 |
|------|------|--------|
| (无) | 交互式5问常用配置提示 | settings |
| --advanced | 高级旋钮：规划、执行、讨论、跨AI、git、运行时 | settings-advanced |
| --integrations | API密钥（Brave/Firecrawl/Exa）、审查CLI路由、代理技能 | settings-integrations |
| --profile <name> | 无需交互提示切换模型配置 | gsd-sdk config-set-model-profile |

## 上下文

参数：用户输入参数

解析用户输入参数的第一个标记：
- 如果是 `--advanced`：去除标志，执行settings-advanced工作流
- 如果是 `--integrations`：去除标志，执行settings-integrations工作流
- 如果以 `--profile` 开头：提取配置名称（`--profile`后的剩余部分），然后：
  1. **预检 (#2439)：** 通过 `command -v gsd-sdk` 验证 `gsd-sdk` 在PATH上。
     如不存在，发出安装提示 `Install GSD via 'npm i -g get-shit-done'` 并停止 —
     不要直接调用 `gsd-sdk`（避免不透明的 `command not found: gsd-sdk` 失败）。
  2. 运行：`gsd-sdk query config-set-model-profile <profile-name> --raw` 并逐字显示输出。
- 否则：执行settings工作流（无需参数）

## 指令

> **TRAE适配说明**：原文中引用的 `gsd-sdk` CLI工具在TRAE环境中不可用。在TRAE SOLO模式中，请直接读取 `.trae/gsd/planning/config.json` 和相关规划文件来获取配置信息，或使用TRAE的文件读取工具替代CLI查询。

1. 从用户输入参数中解析前导标志（如有）。
2. 端到端加载并执行适当的工作流，或为--profile运行内联SDK命令。
3. 保留目标工作流的所有关卡。

## 执行上下文

- `.trae/gsd/workflows/settings.md`
- `.trae/gsd/workflows/settings-advanced.md`
- `.trae/gsd/workflows/settings-integrations.md`

## 参数

- `--advanced` — 高级配置模式
- `--integrations` — 集成配置模式
- `--profile <name>` — 切换模型配置（quality|balanced|budget|inherit）

## 使用场景

- 首次使用GSD需要配置工作流设置
- 需要调整模型、研究、验证等常用开关
- 需要配置第三方API密钥或高级参数

注意：本skill在SOLO Coder中作为GSD工作流的辅助工具使用。

## 不适用场景

- 项目执行过程中无需调整配置时
- 不了解GSD配置项的新手（建议先用默认配置）
- 需要修改项目代码而非配置时

## 输出

- 更新的 `.trae/gsd/planning/config.json` 配置文件

## 依赖

- 无（独立配置skill）
