---
name: skillify
description: Turn a repeatable workflow from the current session into a reusable skill draft. Use when the session uncovered a repeatable workflow that should become a reusable skill.
---

# Skillify

## 描述

当当前会话揭示了一个可重复的工作流，应该成为一个可复用技能时，使用此技能。

目标：将成功的多步骤工作流捕获为具体的技能草案，而不是以后重新发现它。

## 使用场景

- 当前会话完成了一个可重复的任务
- 用户说 "skillify"、"make this a skill"、"save this workflow"
- 发现了一个值得复用的模式或工作流
- 想要将临时操作固化为可复用技能

## 指令

1. 识别会话完成的可重复任务
2. 提取：
   - 输入
   - 有序步骤
   - 成功标准
   - 约束 / 陷阱
   - 技能的最佳目标位置
3. 决定工作流属于：
   - 仓库内置技能
   - 用户/项目学习技能
   - 仅文档
4. 起草学习技能文件时，输出以 YAML frontmatter 开头的完整技能文件
   - 绝不发出纯 markdown 技能文件
   - 最低 frontmatter：
     ```yaml
     ---
     name: <skill-name>
     description: <one-line description>
     triggers:
       - <trigger 1>
       - <trigger 2>
     ---
     ```
   - 将学习/用户/项目技能写入：
     - `.trae/skills/omc-learned/<skill-name>.md`
     - `.trae/skills/<skill-name>.md`
5. 起草技能文件的其余部分，包含清晰的触发器、步骤和成功标准
6. 指出仍然太模糊而无法安全编码的任何内容

### 规则

- 只捕获真正可重复的工作流
- 保持技能实用和有范围
- 优先使用明确的成功标准而非模糊的散文
- 如果工作流仍有未解决的分支决策，在起草前注明

## 示例

**输出格式：**
- 提议的技能名称
- 目标位置
- 草案工作流结构
- 开放问题（如有）