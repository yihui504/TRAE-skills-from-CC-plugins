---
name: debug
description: Diagnose session or repo state problems using logs, traces, state inspection, and focused reproduction. Use when encountering bugs, workflow breakage, or confusing runtime behavior.
---

# Debug

## 描述

使用此技能帮助诊断当前会话或仓库状态的问题、工作流中断或令人困惑的运行时行为。

目标：快速找到真正的失败信号并解释下一步纠正措施。

## 使用场景

使用此技能当：
- 用户遇到 bug、错误或意外行为需要诊断
- 工作流中断或产生不正确结果
- 运行时行为令人困惑或不符合预期
- 需要区分症状和根因

## 指令

1. 仔细阅读用户的问题描述
2. 首先检查最相关的本地证据：
   - 跟踪工具
   - 状态工具
   - 笔记本 / 项目记忆（当相关时）
   - 失败的测试或命令
3. 尽可能窄地重现问题
4. 区分症状和根因
5. 推荐最小的下一步修复或验证步骤

### 规则

- 优先使用真实证据而非猜测
- 当问题涉及编排、钩子或代理流程时，使用跟踪/状态表面
- 如果问题实际上是产品/运行时 bug 而非应用代码问题，直接说明
- 在隔离失败之前，不要开出广泛重写的处方

## 示例

**输出格式：**
- 观察到的失败
- 根因假设
- 支持该假设的证据
- 最小的下一步行动