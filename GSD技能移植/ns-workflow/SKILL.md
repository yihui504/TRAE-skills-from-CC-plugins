---
name: gsd-ns-workflow
description: 当需要路由到工作流相关skill时使用——讨论、规划、执行、验证、阶段、进度
---

# gsd-ns-workflow

## 描述

根据用户意图路由到适当的阶段流水线skill。
以下子skill名称为合并后的目标——`gsd-phase`吸收了原有的add/insert/remove/edit-phase命令，`gsd-progress`吸收了原有的next/do命令。

| 用户意图 | 调用 |
|---|---|
| 规划前收集上下文 | gsd-discuss-phase |
| 明确阶段交付内容 | gsd-spec-phase |
| 创建PLAN.md | gsd-plan-phase |
| 执行阶段计划 | gsd-execute-phase |
| 通过UAT验证构建的功能 | gsd-verify-work |
| 添加/插入/移除/编辑阶段 | gsd-phase |
| 推进到下一个逻辑步骤 | gsd-progress |
| 将规划卸载到ultraplan云 | gsd-ultraplan-phase |
| 跨AI计划审查收敛循环 | gsd-plan-review-convergence |

使用Skill工具直接调用匹配的skill。

## 上下文

无特殊上下文要求。根据用户意图选择对应的skill。

## 指令

根据用户意图，使用Skill工具直接调用匹配的skill。

## 使用场景

- 用户需要执行GSD工作流的核心步骤（讨论→规划→执行→验证）
- 用户需要管理阶段（添加/插入/移除/编辑）
- 用户需要推进到下一个逻辑步骤

注意：本skill在SOLO Coder中作为GSD工作流的辅助工具使用。

## 不适用场景

- 用户已明确指定要使用的具体skill
- 不涉及工作流阶段的需求

## 输出

路由到对应的skill，产出取决于被调用的skill。

## 依赖

- gsd-discuss-phase
- gsd-spec-phase
- gsd-plan-phase
- gsd-execute-phase
- gsd-verify-work
- gsd-phase
- gsd-progress
- gsd-ultraplan-phase
- gsd-plan-review-convergence
