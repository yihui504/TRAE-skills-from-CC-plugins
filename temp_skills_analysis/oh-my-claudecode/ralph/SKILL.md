---
name: ralph
description: Use when task requires guaranteed completion with verification — PRD-driven persistence loop that keeps working until all acceptance criteria pass and are reviewer-verified. Say "ralph", "don't stop", "must complete", or "keep going until done".
---

# Ralph

## 描述

Ralph是PRD驱动的持久化循环，持续工作直到所有验收标准通过并经审查者验证。它在ultrawork的并行执行之上添加了会话持久化、失败自动重试、结构化故事追踪和完成前强制验证。

## 使用场景

- 任务需要保证完成并带验证（不只是"尽力而为"）
- 用户说 "ralph"、"don't stop"、"must complete"、"finish this"、"keep going until done"
- 工作可能跨越多次迭代，需要跨重试的持久化
- 任务受益于结构化PRD驱动执行和审查者签字

## 不适用场景

- 用户想要从想法到代码的完整自主管道 → 使用 autopilot
- 用户想要在提交前探索或规划 → 使用 omc-plan
- 用户想要快速一次性修复 → 直接委派给执行代理
- 用户想要手动控制完成 → 直接使用 ultrawork

## 指令

### 1. PRD设置（仅首次迭代）

a. 检查活跃的PRD文件。会话级路径：`.trae/state/sessions/prd.json`；项目级路径：`.trae/prd.json`。

b. 如果没有现有PRD，自动生成脚手架到 `.trae/prd.json`。

c. **关键：精炼脚手架。** 自动生成的PRD有通用验收标准（如"实现完成"）。你必须替换为任务特定标准：
   - 分析原始任务，分解为合适大小的用户故事
   - 为每个故事编写具体、可验证的验收标准
   - 按优先级排序故事（基础工作优先，依赖工作在后）
   - 将精炼后的PRD写回

d. 初始化 `progress.txt`（如果不存在）

### 2. 选择下一个故事

读取PRD文件，选择 `passes: false` 的最高优先级故事作为当前焦点。

### 3. 实现当前故事

使用 Task 工具委派给专业子代理：

| 任务复杂度 | subagent_type | 用途 |
|-----------|---------------|------|
| 简单查找 | search | "这个函数返回什么？" |
| 标准实现 | backend-architect / frontend-architect | "给这个模块添加错误处理" |
| 复杂分析 | backend-architect | "调试这个竞态条件" |

实现过程中发现子任务时，将其作为新故事添加到PRD。

### 4. 验证当前故事的验收标准

对每个验收标准：
a. 用新鲜证据验证是否满足
b. 运行相关检查（测试、构建、lint、类型检查）并读取输出
c. 如果任何标准不满足，继续工作——不要标记故事为完成

### 5. 标记故事完成

当所有验收标准验证通过：
a. 在PRD中设置 `passes: true`
b. 在 `progress.txt` 中记录进度

### 6. 检查PRD完成

a. 读取PRD——所有故事都标记为 `passes: true` 吗？
b. 如果不是全部完成，回到步骤2
c. 如果全部完成，进入步骤7

### 7. 审查者验证

使用 Task 工具派遣审查子代理：

- <5个文件、<100行变更且有完整测试：使用 `backend-architect`
- 标准变更：使用 `backend-architect`
- >20个文件或安全/架构变更：使用 `backend-architect`（提供更详细的审查指令）

审查者验证**具体的验收标准**，而非模糊的"是否完成"。

**审查通过后**：立即进入步骤8，不要暂停向用户报告。

### 8. 完成退出

- 清理所有状态文件
- 向用户报告完成摘要

### 9. 审查被拒绝时

修复提出的问题，用同一审查者重新验证，然后回到步骤6检查故事是否需要标记为未完成。

## 状态管理

使用文件系统管理状态（替代OMC MCP工具）：

- **PRD状态**：`.trae/prd.json`
- **进度记录**：`.trae/progress.txt`
- **Ralph活跃状态**：`.trae/state/ralph-state.json`

ralph-state.json格式：
```json
{
  "active": true,
  "iteration": 1,
  "current_story": "US-001",
  "started_at": "2026-05-04T12:00:00Z"
}
```

## 执行策略

- 独立的代理调用同时发射——永远不要顺序等待独立工作
- 长操作使用 `blocking: false`（安装、构建、测试套件）
- 交付完整实现：不缩减范围、不部分完成、不删除测试来让它们通过

## 停止条件

| 条件 | 动作 |
|------|------|
| 用户说 "stop"、"cancel"、"abort" | 清理状态文件并退出 |
| 同一问题在3+次迭代中重复 | 报告为潜在根本问题 |
| 基本阻塞需要用户输入 | 停止并报告 |

## 完成检查清单

- [ ] 所有prd.json故事标记为 `passes: true`
- [ ] 验收标准是任务特定的（非通用模板）
- [ ] 原始任务的所有需求已满足
- [ ] 新鲜的测试运行输出显示所有测试通过
- [ ] 新鲜的构建输出显示成功
- [ ] progress.txt记录了实现细节和学习
- [ ] 审查者验证通过
- [ ] 状态文件已清理
