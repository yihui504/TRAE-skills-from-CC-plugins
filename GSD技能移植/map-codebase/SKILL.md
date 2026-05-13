---
name: gsd-map-codebase
description: 当需要使用并行映射代理分析代码库并生成结构化代码库文档时使用
---

# gsd-map-codebase

## 描述

使用并行的gsd-codebase-mapper代理分析已有代码库，生成结构化的代码库文档。

每个映射代理探索一个关注区域并**直接写入**文档到`.trae/gsd/planning/codebase/`。编排器仅接收确认，保持上下文使用最小化。

输出：`.trae/gsd/planning/codebase/`文件夹，包含7份关于代码库状态的结构化文档。

## 上下文

参数：用户输入参数

解析用户输入参数的第一个标记：
- 如果是`--fast`：去除标志，运行扫描工作流（传递剩余参数包括可选的--focus）
- 如果是`--query`：去除标志，运行智能工作流（传递剩余参数作为子命令）
- 否则：将所有用户输入参数作为关注区域传递给map-codebase工作流

**加载项目状态（如存在）：**
检查`.trae/gsd/planning/STATE.md`——如果项目已初始化则加载上下文

**此命令可运行于：**
- gsd:new-project之前（棕地代码库）——先创建代码库映射
- gsd:new-project之后（绿地代码库）——随代码演进更新代码库映射
- 随时刷新代码库理解

## 指令

1. 检查`.trae/gsd/planning/codebase/`是否已存在（提供刷新或跳过选项）
2. 创建`.trae/gsd/planning/codebase/`目录结构
3. 生成4个并行的gsd-codebase-mapper代理：
   - 代理1：tech关注 → 写入STACK.md、INTEGRATIONS.md
   - 代理2：arch关注 → 写入ARCHITECTURE.md、STRUCTURE.md
   - 代理3：quality关注 → 写入CONVENTIONS.md、TESTING.md
   - 代理4：concerns关注 → 写入CONCERNS.md
4. 等待代理完成，收集确认（不是文档内容）
5. 验证所有7个文档存在且有行数
6. 提交代码库映射
7. 提供下一步建议（通常是：gsd-new-project或gsd-plan-phase）

## 执行上下文

- `.trae/gsd/workflows/map-codebase.md`

## 参数

- **--fast**：轻量扫描模式——生成1个映射代理而非4个。接受可选的`--focus`值：`tech`、`arch`、`quality`、`concerns`或`tech+arch`（默认）。比完整映射更快、上下文更低。
- **--query**：代码库智能查询模式。子命令：`query <term>`、`status`、`diff`、`refresh`。需要在配置中启用intel（`intel.enabled: true`）。query/status/diff内联运行；refresh生成代理。
- **(无标志)**：完整并行映射——生成4个映射代理生成所有7个代码库文档。
- `[area]`：可选的关注区域

## 使用场景

- 棕地项目初始化前需要理解已有代码
- 重大变更后需要刷新代码库映射
- 入职不熟悉的代码库
- 重大重构前需要理解当前状态
- STATE.md引用了过时的代码库信息

注意：本skill在SOLO Coder中作为GSD工作流的辅助工具使用。

## 不适用场景

- 绿地项目尚无代码（无内容可映射）
- 微不足道的代码库（少于5个文件）
- 仅需查看单个文件

## 输出

- `.trae/gsd/planning/codebase/STACK.md`
- `.trae/gsd/planning/codebase/INTEGRATIONS.md`
- `.trae/gsd/planning/codebase/ARCHITECTURE.md`
- `.trae/gsd/planning/codebase/STRUCTURE.md`
- `.trae/gsd/planning/codebase/CONVENTIONS.md`
- `.trae/gsd/planning/codebase/TESTING.md`
- `.trae/gsd/planning/codebase/CONCERNS.md`

## 依赖

- gsd-codebase-mapper（映射代理）
