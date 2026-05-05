---
name: skill-creator
description: Use when creating new skills, editing existing skills, or verifying skills work before deployment. Guides the full skill creation lifecycle with TDD-inspired validation.
---

# Skill Creator

## 描述

技能创建器引导你完成技能的完整创建生命周期：从识别可复用模式，到编写SKILL.md，再到验证技能在实际场景中有效。

## 使用场景

- 用户说 "create a skill"、"make a skill"、"new skill"
- 用户想要将重复的工作流固化为可复用技能
- 用户想要编辑或改进现有技能
- 用户想要验证技能是否按预期工作

## 不适用场景

- 用户只是想执行一个一次性任务（不需要创建技能）
- 用户想要创建项目规则（使用规则而非技能）

## 指令

### Step 1: 识别技能需求

确认以下条件：
- 工作流是否可重复？（至少会在不同场景下使用2次以上）
- 是否无法在5分钟内Google到答案？
- 是否包含项目特定的知识或模式？

如果以上任一条件不满足，不需要创建技能。

### Step 2: 确定技能类型

| 类型 | 描述 | 示例 |
|------|------|------|
| **技术型** | 有具体步骤的可执行方法 | 条件等待、根因追踪 |
| **模式型** | 思考问题的方式 | 标志扁平化、测试不变量 |
| **参考型** | API文档、语法指南 | 工具文档 |

### Step 3: 编写SKILL.md

必须包含YAML frontmatter：

```yaml
---
name: skill-name-with-hyphens
description: Use when [具体触发条件和症状]
---
```

description规则：
- 以 "Use when..." 开头，聚焦触发条件
- 用第三人称
- 包含具体的触发词、症状、场景
- **绝不**在description中总结技能的工作流程

SKILL.md正文结构：

```markdown
# 技能名称

## 描述
核心原则，1-2句话。

## 使用场景
- 触发条件列表
- 不适用场景

## 指令
分步说明，告诉智能体具体怎么做。

## 示例（可选）
输入/输出示例，展示预期效果。
```

### Step 4: 质量检查

- [ ] name只包含字母、数字和连字符
- [ ] description以"Use when..."开头
- [ ] description不包含工作流程总结
- [ ] 有清晰的描述和使用场景
- [ ] 指令是可执行的步骤
- [ ] 关键词覆盖（错误消息、症状、工具名）

### Step 5: 验证技能

用一个典型的使用场景测试技能：
1. 构造一个触发该技能的任务描述
2. 按照技能指令执行
3. 确认输出符合预期
4. 如果不符合，修改技能并重新测试

### Step 6: 保存技能

保存到适当位置：
- **项目技能**：`.trae/skills/<skill-name>/SKILL.md`
- **全局技能**：`~/.trae/skills/<skill-name>/SKILL.md`（Windows: `%userprofile%\.trae\skills\<skill-name>\SKILL.md`）

## 常见错误

| 错误 | 修正 |
|------|------|
| description中包含工作流程 | 只写触发条件 |
| 技能太通用（5分钟能Google到） | 聚焦项目特定知识 |
| 技能太具体（只适用一次） | 提取可复用的原则 |
| 缺少触发条件 | 添加具体的触发词和症状 |
| name包含特殊字符 | 只用字母、数字、连字符 |

## 示例

**好的技能：**
```yaml
---
name: async-race-condition-debugging
description: Use when tests have race conditions, timing dependencies, or pass/fail inconsistently across runs
---
```

**差的技能：**
```yaml
---
name: debugging
description: Use when you need to debug code by reading errors, reproducing issues, and fixing root causes
---
```
（太通用，description总结了工作流程）
