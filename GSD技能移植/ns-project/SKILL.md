---
name: gsd-ns-project
description: 当需要路由到项目生命周期相关skill时使用——里程碑、审计、摘要
---

# gsd-ns-project

## 描述

根据用户意图路由到适当的项目/里程碑skill。
`gsd-plan-milestone-gaps`已被删除——差距规划现在作为`gsd-audit-milestone`输出的一部分内联进行。

| 用户意图 | 调用 |
|---|---|
| 开始新项目 | gsd-new-project |
| 创建新里程碑 | gsd-new-milestone |
| 完成当前里程碑 | gsd-complete-milestone |
| 审计里程碑问题 | gsd-audit-milestone |
| 汇总里程碑状态 | gsd-milestone-summary |

使用Skill工具直接调用匹配的skill。

## 上下文

无特殊上下文要求。根据用户意图选择对应的skill。

## 指令

根据用户意图，使用Skill工具直接调用匹配的skill。

## 使用场景

- 用户需要开始新项目或创建新里程碑
- 用户需要审计或完成里程碑
- 用户需要汇总里程碑状态

注意：本skill在SOLO Coder中作为GSD工作流的辅助工具使用。

## 不适用场景

- 用户已明确指定要使用的具体skill
- 不涉及项目生命周期管理的需求

## 输出

路由到对应的skill，产出取决于被调用的skill。

## 依赖

- gsd-new-project
- gsd-new-milestone
- gsd-complete-milestone
- gsd-audit-milestone
- gsd-milestone-summary
