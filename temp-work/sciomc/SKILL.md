---
name: sciomc
description: Use when conducting comprehensive multi-faceted research that benefits from parallel investigation. Orchestrates parallel specialist agents for decomposition, execution, verification, and synthesis. Say "research" or use AUTO mode for fully autonomous execution.
---

# sciomc

## 描述

编排并行专家代理进行全面研究工作流。将复杂研究目标分解为独立阶段，并行派遣专家子代理调查，交叉验证发现，最终综合成结构化报告。

## 使用场景

- 需要多角度、多方面的深度研究
- 用户说 "research"、"analyze comprehensively"、"investigate"
- 研究目标可以分解为3-7个独立调查方向
- 需要AUTO模式全自动运行直到完成

## 不适用场景

- 简单的单一问题 → 直接使用 search 子代理
- 只需要快速代码查找 → 直接使用搜索工具
- 研究目标无法分解为独立阶段 → 直接分析

## 指令

### Step 1: 阶段分解

将研究目标分解为3-7个独立阶段：

```markdown
## 研究分解

**目标：** <原始研究目标>

### 阶段1: <名称>
- **焦点：** 本阶段调查什么
- **假设：** 预期发现（如适用）
- **范围：** 要检查的文件/区域
- **复杂度：** LOW | MEDIUM | HIGH

### 阶段2: <名称>
...
```

### Step 2: 并行专家调用

通过 Task 工具并行发射独立阶段：

```
Task(subagent_type="search", query="[RESEARCH_STAGE:1] 调查认证实现模式...")

Task(subagent_type="backend-architect", query="[RESEARCH_STAGE:2] 分析API层的错误处理...")

Task(subagent_type="backend-architect", query="[RESEARCH_STAGE:3] 深度分析缓存策略...")
```

### Step 3: 智能模型路由

| 任务复杂度 | subagent_type | 用途 |
|-----------|---------------|------|
| 数据收集 | search | 文件枚举、模式计数、简单查找 |
| 标准分析 | backend-architect | 代码分析、模式检测、文档审查 |
| 复杂推理 | backend-architect（带详细指令） | 架构分析、跨领域关注、假设验证 |

### Step 4: 验证循环

并行执行完成后，验证发现：

```
Task(subagent_type="backend-architect", query="
[RESEARCH_VERIFICATION]
交叉验证以下发现的一致性：

阶段1发现：<摘要>
阶段2发现：<摘要>
阶段3发现：<摘要>

检查：
1. 阶段间的矛盾
2. 缺失的关联
3. 覆盖范围的空白
4. 证据质量

输出: [VERIFIED] 或 [CONFLICTS: <具体冲突>]
")
```

### Step 5: 综合报告

生成结构化研究报告：

```markdown
# 研究报告: <目标>

**会话ID:** <id>
**日期:** <date>
**状态:** <status>

## 执行摘要

<2-3段关键发现摘要>

## 方法论

### 研究阶段

| 阶段 | 焦点 | 复杂度 | 状态 |
|------|------|--------|------|
| ... | ... | ... | ... |

## 关键发现

### 发现1: <标题>

**置信度:** HIGH | MEDIUM | LOW

<详细发现及证据>

### 发现2: <标题>
...

## 交叉验证结果

<验证摘要，已解决的冲突>

## 局限性

- <局限1>
- <局限2>

## 建议

1. <可操作的建议>
2. <可操作的建议>
```

## AUTO模式

AUTO模式全自动运行完整研究工作流。

### 循环控制

- 最大迭代次数：10
- 继续直到：所有阶段完成并验证，或达到最大迭代
- 取消：用户说 "stop research"、"cancel research"、"abort"

### AUTO模式规则

1. 分解后立即并行发射所有独立阶段
2. 每个阶段完成后更新状态
3. 所有阶段完成后运行验证
4. 验证通过后生成综合报告
5. 如果验证发现冲突，重新运行冲突阶段

## 会话管理

### 目录结构

```
.trae/research/{session-id}/
  state.json
  stages/
    stage-1.md
    stage-2.md
    ...
  report.md
```

### 状态文件格式

```json
{
  "id": "research-20260504-abc123",
  "goal": "原始研究目标",
  "status": "in_progress | complete | blocked | cancelled",
  "mode": "standard | auto",
  "iteration": 1,
  "maxIterations": 10,
  "stages": [
    {
      "id": 1,
      "name": "阶段名称",
      "tier": "LOW | MEDIUM | HIGH",
      "status": "pending | running | complete | failed"
    }
  ]
}
```

### 会话命令

| 操作 | 方法 |
|------|------|
| 查看状态 | 读取 `.trae/research/{session-id}/state.json` |
| 恢复会话 | 读取状态文件，从最后完成的阶段继续 |
| 列出会话 | 扫描 `.trae/research/` 目录 |
| 取消 | 更新状态为 "cancelled" |

## 并发限制

最多同时运行5个并行子代理，防止资源耗尽。

如果超过5个阶段，分批执行：
```
批次1: 阶段1-5（并行）
[等待完成]
批次2: 阶段6-7（并行）
```

## 子代理路由映射

| OMC原始类型 | Trae Solo替代 | 用途 |
|------------|--------------|------|
| scientist (haiku) | search | 简单数据收集和查找 |
| scientist (sonnet) | backend-architect | 标准代码分析和模式检测 |
| scientist (opus) | backend-architect（带详细指令） | 复杂推理和架构分析 |

## 故障排除

**验证循环卡住？**
- 检查阶段间是否有冲突发现
- 审查state.json中的具体冲突
- 可能需要用不同方法重新运行特定阶段

**专家返回低质量发现？**
- 检查复杂度分配——复杂分析需要 HIGH 级别
- 确保提示包含清晰的范围和预期输出格式
- 审查研究目标是否太宽泛

**AUTO模式耗尽迭代？**
- 审查状态查看卡在哪里
- 检查目标是否可用现有数据实现
- 考虑分解为更小的研究会话
