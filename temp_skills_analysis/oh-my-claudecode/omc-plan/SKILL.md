---
name: omc-plan
description: Use when planning before implementing — creates comprehensive work plans through intelligent interaction with optional consensus mode (Planner/Architect/Critic loop). Say "plan this", "let's plan", or use --consensus for multi-perspective validation.
---

# omc-plan

## 描述

Plan通过智能交互创建全面的、可执行的工作计划。自动检测是应该访谈用户（需求模糊时）还是直接规划（需求明确时），并支持共识模式（Planner/Architect/Critic循环）和审查模式。

## 使用场景

- 用户想要在实现前规划——"plan this"、"plan the"、"let's plan"
- 用户想要为模糊想法进行结构化需求收集
- 用户想要审查现有计划——"review this plan"、`--review`
- 用户想要多视角共识——`--consensus`
- 任务宽泛或模糊，需要在写代码前确定范围

## 不适用场景

- 用户想要端到端自主执行 → 使用 autopilot
- 用户想要立即开始编码且任务明确 → 使用 ralph 或直接委派
- 简单问题可以直接回答 → 直接回答
- 单一聚焦修复且范围明确 → 跳过规划，直接做

## 指令

### 模式选择

| 模式 | 触发条件 | 行为 |
|------|---------|------|
| 访谈 | 宽泛请求（默认） | 交互式需求收集 |
| 直接 | `--direct` 或详细请求 | 跳过访谈，直接生成计划 |
| 共识 | `--consensus` | Planner→Architect→Critic循环 |
| 审查 | `--review` | Critic评估现有计划 |

### 访谈模式（宽泛/模糊请求）

1. **分类请求**：宽泛（模糊动词、无具体文件、涉及3+领域）触发访谈模式
2. **一次只问一个聚焦问题**，使用 `AskUserQuestion`
3. **先收集代码库事实**：在问用户之前，先用 `search` 子代理查找
4. **基于答案构建**：每个问题建立在前一个答案之上
5. **咨询分析师**：使用 `backend-architect` 子代理发现隐藏需求、边缘情况和风险
6. 当用户表示准备好时创建计划

### 直接模式（详细请求）

1. **快速分析**：可选的简短分析师咨询
2. **创建计划**：立即生成全面工作计划
3. **审查**（可选）：如果请求则进行Critic审查

### 共识模式（`--consensus`）

1. **Planner** 创建初始计划 + RALPLAN-DR摘要：
   - 原则（3-5个）
   - 决策驱动因素（前3个）
   - 可行选项（≥2个）及有界的优缺点
   - 如果只有一个可行选项，提供明确的替代方案无效理由

2. **Architect** 使用 `Task(subagent_type="backend-architect")` 审查架构合理性：
   - 必须提供最强反论（反题）
   - 至少一个有意义的权衡张力
   - 可能的话提供综合路径
   - **等待此步骤完成后再进入步骤3**

3. **Critic** 使用 `Task(subagent_type="backend-architect")` 评估质量标准：
   - 验证原则-选项一致性
   - 公平的替代方案探索
   - 风险缓解清晰度
   - 可测试的验收标准
   - 具体的验证步骤
   - **必须在步骤2完成后运行**

4. **重新审查循环**（最多5次迭代）：
   - 收集Architect + Critic的所有拒绝反馈
   - 传递给Planner生成修订计划
   - 回到步骤2（Architect审查修订计划）
   - 回到步骤3（Critic评估修订计划）
   - 重复直到Critic通过或达到5次迭代

5. **应用改进**：当审查者通过但有改进建议时，合并所有接受的改进

6. **最终输出**包含ADR部分：决策、驱动因素、考虑的替代方案、选择原因、后果、后续事项

7. 使用 `AskUserQuestion` 呈现计划，提供选项：
   - **批准并通过ralph执行**
   - **批准并通过ultrawork执行**
   - **请求修改**
   - **拒绝**

### 审查模式（`--review`）

1. 从 `.trae/plans/` 读取计划文件
2. 使用 `Task(subagent_type="backend-architect")` 通过Critic评估
3. 返回裁定：APPROVED、REVISE（附具体反馈）、或 REJECT

### 计划输出格式

每个计划包含：
- 需求摘要
- 验收标准（可测试）
- 实现步骤（附文件引用）
- 风险和缓解措施
- 验证步骤
- 共识模式：RALPLAN-DR摘要 + ADR

计划保存到 `.trae/plans/`。草稿保存到 `.trae/drafts/`。

## 子代理路由映射

| OMC原始类型 | Trae Solo替代 | 用途 |
|------------|--------------|------|
| architect | backend-architect | 架构审查和技术设计 |
| critic | backend-architect（带审查指令） | 质量评估和计划审查 |
| analyst | backend-architect | 需求分析和隐藏需求发现 |
| explore | search | 代码库事实收集 |

## 状态管理

使用文件系统管理状态：

- **计划状态**：`.trae/state/ralplan-state.json`

ralplan-state.json格式：
```json
{
  "active": true,
  "mode": "consensus",
  "iteration": 1,
  "started_at": "2026-05-04T12:00:00Z"
}
```

## 质量标准

| 标准 | 标准 |
|------|------|
| 清晰度 | 80%+的声明引用文件/行号 |
| 可测试性 | 90%+的标准是具体的 |
| 验证 | 所有文件引用存在 |
| 具体性 | 无模糊术语（"fast" → "p99 < 200ms"） |

## 注意事项

- 使用 `AskUserQuestion` 进行偏好问题——提供可点击的UI
- 使用纯文本进行需要具体值的问题
- 使用 `search` 子代理在问用户之前收集代码库事实
- **共识模式代理调用必须顺序执行，不可并行**
- 需求足够清晰时停止访谈——不要过度访谈
- 共识模式最多5次Planner/Architect/Critic迭代
- 如果用户说 "just do it" 或 "skip planning"，直接使用 ralph 执行
