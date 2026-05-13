---
name: gsd-ns-ideate
description: 当需要路由到探索或捕获相关skill时使用——探索、草图、spike、规格、捕获
---

# gsd-ns-ideate

## 描述

根据用户意图路由到适当的探索/捕获skill。
`gsd-note`、`gsd-add-todo`、`gsd-add-backlog`和`gsd-plant-seed`已被合并到`gsd-capture`（含`--note`、默认、`--backlog`、`--seed`模式）。捕获目标列表通过`--list`查看待办。

| 用户意图 | 调用 |
|---|---|
| 探索想法或机会 | gsd-explore |
| 勾勒粗略设计或计划 | gsd-sketch |
| 限时技术spike | gsd-spike |
| 为阶段编写规格 | gsd-spec-phase |
| 捕获想法（todo / note / backlog / seed） | gsd-capture |

使用Skill工具直接调用匹配的skill。

## 上下文

无特殊上下文要求。根据用户意图选择对应的skill。

## 指令

根据用户意图，使用Skill工具直接调用匹配的skill。

## 使用场景

- 用户想探索新想法或机会
- 用户需要快速记录想法、待办或backlog项
- 用户需要为阶段编写技术规格

注意：本skill在SOLO Coder中作为GSD工作流的辅助工具使用。

## 不适用场景

- 用户已明确指定要使用的具体skill
- 不涉及探索或捕获的需求

## 输出

路由到对应的skill，产出取决于被调用的skill。

## 依赖

- gsd-explore
- gsd-sketch
- gsd-spike
- gsd-spec-phase
- gsd-capture
