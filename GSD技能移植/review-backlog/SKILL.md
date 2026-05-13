---
name: gsd-review-backlog
description: 当需要审查待办事项并将积压项提升到活跃里程碑时使用
---

# gsd-review-backlog

## 描述

审查所有999.x积压项，并可选地将它们提升到活跃里程碑序列或删除过期条目。

## 上下文

无需额外参数，自动扫描积压目录。

## 指令

> **TRAE适配说明**：原文中引用的 `gsd-sdk` CLI工具在TRAE环境中不可用。在TRAE SOLO模式中，请直接读取 `.trae/gsd/planning/config.json` 和相关规划文件来获取配置信息，或使用TRAE的文件读取工具替代CLI查询。

1. **列出积压项：**
   ```bash
   ls -d .trae/gsd/planning/phases/999* 2>/dev/null || echo "No backlog items found"
   ```

2. **读取ROADMAP.md**并提取所有999.x阶段条目：
   ```bash
   cat .trae/gsd/planning/ROADMAP.md
   ```
   显示每个积压项的描述、累积上下文（CONTEXT.md、RESEARCH.md）和创建日期。

3. **通过向用户提问展示列表**：
   - 对于每个积压项，显示：阶段编号、描述、累积产物
   - 每个项目的选项：**提升**（移到活跃）、**保留**（留在积压）、**删除**

4. **对于要提升的项目：**
   - 找到活跃里程碑中的下一个顺序阶段编号
   - 将目录从`999.x-slug`重命名为`{new_num}-slug`：
     ```bash
     NEW_NUM=$(gsd-sdk query phase.add "${DESCRIPTION}" --raw)
     ```
   - 将累积产物移到新阶段目录
   - 更新ROADMAP.md：将条目从`## Backlog`部分移到活跃阶段列表
   - 删除`(BACKLOG)`标记
   - 添加适当的`**Depends on:**`字段

5. **对于要删除的项目：**
   - 删除阶段目录
   - 从ROADMAP.md的`## Backlog`部分删除条目

6. **提交更改：**
   ```bash
   gsd-sdk query commit "docs: review backlog — promoted N, removed M" --files .trae/gsd/planning/ROADMAP.md
   ```

7. **报告摘要：**
   ```
   ## 📋 Backlog Review Complete

   Promoted: {list of promoted items with new phase numbers}
   Kept: {list of items remaining in backlog}
   Removed: {list of deleted items}
   ```

## 使用场景

- 积压项积累到需要整理时
- 里程碑规划时需要将积压项纳入正式计划
- 需要清理过时或不再相关的积压项时

注意：本skill在SOLO Coder中作为GSD工作流的辅助工具使用。

## 不适用场景

- 项目没有积压项时
- 需要创建新的积压项时（应直接在plan-phase中处理）

## 输出

- 更新后的ROADMAP.md
- 积压项审查摘要报告

## 依赖

- 无直接依赖其他GSD skill
