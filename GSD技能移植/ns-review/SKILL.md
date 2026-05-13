---
name: gsd-ns-review
description: 当需要路由到质量审查相关skill时使用——代码审查、调试、审计、安全、评估
---

# gsd-ns-review

## 描述

根据用户意图路由到适当的质量/审查skill。
`gsd-code-review-fix`已被`gsd-code-review --fix`吸收。

| 用户意图 | 调用 |
|---|---|
| 审查代码质量和正确性 | gsd-code-review |
| 自动修复代码审查发现 | gsd-code-review --fix |
| 审计UAT/验收测试 | gsd-audit-uat |
| 阶段安全审查 | gsd-secure-phase |
| 评估AI响应质量 | gsd-eval-review |
| 审查UI设计和可访问性 | gsd-ui-review |
| 验证阶段输出 | gsd-validate-phase |
| 调试失败的功能或错误 | gsd-debug |
| 损坏系统的取证调查 | gsd-forensics |

使用Skill工具直接调用匹配的skill。

## 上下文

无特殊上下文要求。根据用户意图选择对应的skill。

## 指令

根据用户意图，使用Skill工具直接调用匹配的skill。

## 使用场景

- 用户需要代码审查或质量检查
- 用户需要调试错误或进行安全审查
- 用户需要验证阶段输出或审计UAT

注意：本skill可独立于GSD流程使用，在SOLO Coder中直接调用即可。

## 不适用场景

- 用户已明确指定要使用的具体skill
- 不涉及质量审查的需求

## 输出

路由到对应的skill，产出取决于被调用的skill。

## 依赖

- gsd-code-review
- gsd-audit-uat
- gsd-secure-phase
- gsd-eval-review
- gsd-ui-review
- gsd-validate-phase
- gsd-debug
- gsd-forensics
