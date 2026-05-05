---
name: learner
description: Extract a learned skill from the current conversation. Use when solving tricky bugs, discovering non-obvious workarounds, or finding hidden gotchas specific to the codebase.
---

# Learner Skill

## 描述

这是一个自改进型技能。它有两个不同部分：
- **专业知识**：关于什么构成好技能的领域知识。随着模式发现自动更新。
- **工作流**：稳定的提取程序。很少变化。

只有专业知识部分应在改进周期中更新。

## 使用场景

仅在以下情况后提取技能：
- 解决了需要深入调查的棘手 bug
- 发现了特定于此代码库的非显而易见的变通方法
- 找到了遗忘时会浪费时间的隐藏陷阱
- 揭示了影响此项目的未文档化行为

## 指令

### 质量门

提取技能前，以下三个条件必须全部满足：
- "有人能在 5 分钟内 Google 到这个吗？" → 不能
- "这是特定于此代码库的吗？" → 是
- "这需要真正的调试努力才能发现吗？" → 是

### 核心原则

可复用技能不是复制粘贴的代码片段，而是**原则和决策启发式方法**，教导如何思考一类问题。

**区别：**
- 差（模仿）："当你看到 ConnectionResetError，添加这个 try/except 块"
- 好（可复用技能）："在异步网络代码中，任何 I/O 操作都可能因客户端/服务器生命周期不匹配而独立失败。原则：分别包装每个 I/O 操作，因为操作之间的失败是常见情况，而非例外。"

### 什么构成有用的技能

1. **不可 Google**：不容易通过搜索找到的内容
   - 差："如何在 TypeScript 中读取文件" ❌
   - 好："此代码库在 ESM 中使用自定义路径解析，需要 fileURLToPath + 特定相对路径" ✓

2. **上下文特定**：引用此代码库中的实际文件、错误消息或模式
   - 差："使用 try/catch 进行错误处理" ❌
   - 好："server.py:42 中的 aiohttp 代理在 ClientDisconnectedError 上崩溃 - 在 try/except 中包装 StreamResponse" ✓

3. **精确可操作**：准确告诉你做什么和在哪里做
   - 差："处理边缘情况" ❌
   - 好："当在 dist/ 中看到 'Cannot find module' 时，检查 tsconfig.json 的 moduleResolution 是否匹配 package.json 的 type 字段" ✓

4. **来之不易**：需要大量调试努力才能发现
   - 差：通用编程模式 ❌
   - 好："worker.ts 中的竞态条件 - 第 89 行的 Promise.all 需要在 map 回调返回前 await" ✓

### 反模式（不要提取）

- 通用编程模式（使用文档）
- 重构技术（这些是通用的）
- 库使用示例（使用库文档）
- 类型定义或样板代码
- 初级开发者 5 分钟内能 Google 到的任何东西

### Step 1: 收集必要信息

- **问题陈述**：发生的具体错误、症状或困惑
  - 包含实际错误消息、文件路径、行号
  - 示例："TypeError in src/hooks/session.ts:45 when sessionId is undefined after restart"

- **解决方案**：精确修复，而非一般建议
  - 包含代码片段、文件路径、配置变更
  - 示例："Add null check before accessing session.user, regenerate session on 401"

- **触发器**：再次遇到此问题时会出现的关键词
  - 使用错误消息片段、文件名、症状描述
  - 示例：["sessionId undefined", "session.ts TypeError", "401 session"]

- **范围**：几乎总是项目级，除非是真正通用的洞察

### Step 2: 质量验证

系统拒绝以下技能：
- 太通用（没有文件路径、行号或特定错误消息）
- 容易 Google 到（标准模式、库使用）
- 模糊的解决方案（没有代码片段或精确指令）
- 差的触发器（匹配一切的通用词）

### Step 3: 分类为专业知识或工作流

保存前，确定学习内容是：
- **专业知识**（领域知识、模式、陷阱）→ 保存为 `{topic}-expertise.md`
- **工作流**（操作程序、步骤序列）→ 保存为 `{topic}-workflow.md`

此分类确保专业知识可以独立更新而不破坏工作流稳定性。

### Step 4: 保存位置

- **用户级**：`.trae/skills/omc-learned/<skill-name>.md` - 罕见。仅用于真正可移植的洞察。
- **项目级**：`.trae/skills/<skill-name>.md` - 默认。旨在与仓库一起提交，当您希望团队保留该技能时。

### 必需的文件格式

每个学习技能文件必须以 YAML frontmatter 开头，以便学习技能的平面文件发现可以加载它。
不要写没有 frontmatter 的纯 markdown。

最低要求的 frontmatter：

```yaml
---
name: <skill-name>
description: <one-line description>
triggers:
  - <trigger 1>
  - <trigger 2>
---
```

### 技能正文模板

```markdown
---
name: <skill-name>
description: <one-line description>
triggers:
  - <trigger 1>
  - <trigger 2>
---

# [Skill Name]

## The Insight
What is the underlying PRINCIPLE you discovered? Not the code, but the mental model.

## Why This Matters
What goes wrong if you don't know this? What symptom led you here?

## Recognition Pattern
How do you know when this skill applies? What are the signs?

## The Approach
The decision-making heuristic, not just code. How should you THINK about this?

## Example (Optional)
If code helps, show it - but as illustration of the principle, not copy-paste material.
```

**关键**：如果技能可以应用于新情况（而非仅相同情况），则它是可复用的。

## 示例

**好的学习技能：**
```
名称: esm-path-resolution
描述: This codebase uses custom path resolution in ESM that requires fileURLToPath + specific relative paths
触发器: ["Cannot find module in ESM", "fileURLToPath", "__dirname alternative ESM"]
洞察: ESM modules don't have __dirname. The codebase uses a custom resolvePath() utility that must be used instead of raw relative imports.
```

**差的学习技能：**
```
名称: try-catch
描述: Use try/catch for error handling
→ 太通用，5 分钟内能 Google 到
```