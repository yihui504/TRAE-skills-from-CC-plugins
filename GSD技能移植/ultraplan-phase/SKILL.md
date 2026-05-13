---
name: gsd-ultraplan-phase
description: 当需要将规划阶段卸载到Claude Code的ultraplan云基础设施时使用——在浏览器中审查并导入回来
---

# gsd-ultraplan-phase

## 描述

将GSD的规划阶段卸载到Claude Code的ultraplan云基础设施。

Ultraplan在远程云会话中起草计划，而你的终端保持空闲。
在浏览器中审查和评论计划，然后通过`gsd-import --from`导入回来。

BETA：ultraplan处于研究预览阶段。使用`gsd-plan-phase`进行稳定的本地规划。
要求：Claude Code v2.1.91+、claude.ai账户、GitHub仓库。

## 上下文

用户输入参数：`[阶段编号]`

## 指令

端到端执行ultraplan-phase工作流。

## 执行上下文

- `.trae/gsd/workflows/ultraplan-phase.md`
- `.trae/gsd/references/ui-brand.md`

## 参数

- **[阶段编号]**：指定要规划的阶段编号

## 使用场景

- 需要利用云基础设施进行大规模规划时
- 想要在浏览器中交互式审查计划时
- 本地规划资源不足时

注意：本skill在SOLO Coder中作为GSD工作流的辅助工具使用。

## 不适用场景

- 需要稳定可靠的本地规划时（应使用plan-phase）
- 没有Claude Code v2.1.91+或GitHub仓库时
- 网络不可用时

## 输出

- 云端生成的计划，可通过`gsd-import --from`导入

## 依赖

- gsd-import（导入云端计划）
- gsd-plan-phase（稳定的本地规划替代方案）
