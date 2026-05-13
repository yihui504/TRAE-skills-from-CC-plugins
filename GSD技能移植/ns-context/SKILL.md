---
name: gsd-ns-context
description: 当需要路由到代码库智能相关skill时使用——映射、图谱、文档、学习
---

# gsd-ns-context

## 描述

根据用户意图路由到适当的代码库智能skill。
`gsd-scan`和`gsd-intel`已被合并到`gsd-map-codebase`的标志中。

| 用户意图 | 调用 |
|---|---|
| 映射完整代码库结构 | gsd-map-codebase |
| 快速轻量代码库扫描 | gsd-map-codebase --fast |
| 查询已映射的智能文件 | gsd-map-codebase --query |
| 生成知识图谱 | gsd-graphify |
| 更新项目文档 | gsd-docs-update |
| 从已完成阶段提取学习 | gsd-extract-learnings |

使用Skill工具直接调用匹配的skill。

## 上下文

无特殊上下文要求。根据用户意图选择对应的skill。

## 指令

根据用户意图，使用Skill工具直接调用匹配的skill。

## 使用场景

- 用户提到代码库映射、扫描、智能查询等需求但未指定具体skill
- 需要生成代码库知识图谱
- 需要更新项目文档或提取学习

注意：本skill在SOLO Coder中作为GSD工作流的辅助工具使用。

## 不适用场景

- 用户已明确指定要使用的具体skill
- 不涉及代码库智能的需求

## 输出

路由到对应的skill，产出取决于被调用的skill。

## 依赖

- gsd-map-codebase
- gsd-graphify
- gsd-docs-update
- gsd-extract-learnings
