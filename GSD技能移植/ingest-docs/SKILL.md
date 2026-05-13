---
name: gsd-ingest-docs
description: 当需要从仓库中已有的ADR、PRD、SPEC等文档引导创建或合并规划目录时使用
---

# gsd-ingest-docs

## 描述

从多个已有的规划文档——ADR、PRD、SPEC、DOC——一次性构建完整的`.trae/gsd/planning/`配置（或合并到已有配置中）。

- **全新引导**（`--mode new`，`.trae/gsd/planning/`不存在时的默认值）：从合成的文档内容生成PROJECT.md + REQUIREMENTS.md + ROADMAP.md + STATE.md，将最终生成委托给`gsd-roadmapper`。
- **合并到已有**（`--mode merge`，`.trae/gsd/planning/`存在时的默认值）：追加从导入文档派生的阶段和需求；对与已有锁定决策的任何矛盾进行硬阻断。

使用优先级规则`ADR > SPEC > PRD > DOC`自动合成大多数冲突（可通过manifest覆盖）。将未解决的案例展示在`.trae/gsd/planning/INGEST-CONFLICTS.md`中，分为三个桶：auto-resolved、competing-variants、unresolved-blockers。共享冲突引擎的BLOCKER门在存在未解决矛盾时阻止写入任何目标文件。

**输入：** 目录约定发现（`docs/adr/`、`docs/prd/`、`docs/specs/`、`docs/rfc/`、根级`{ADR,PRD,SPEC,RFC}-*.md`），或显式的`--manifest <file>` YAML，列出每个文档的`{path, type, precedence?}`。

**v1约束：** 每次调用硬上限50个文档；`--resolve interactive`保留给未来版本。

## 上下文

用户输入参数

## 指令

端到端执行ingest-docs工作流。保留所有审批门（发现、冲突报告、路由）和BLOCKER安全规则。

## 执行上下文

- `.trae/gsd/workflows/ingest-docs.md`
- `.trae/gsd/references/ui-brand.md`
- `.trae/gsd/references/gate-prompts.md`
- `.trae/gsd/references/doc-conflict-engine.md`

## 参数

- `[path]`：项目路径
- `--mode new|merge`：引导模式（new=全新，merge=合并）
- `--manifest <file>`：显式指定文档清单YAML文件
- `--resolve auto|interactive`：冲突解决模式（当前仅支持auto）

## 使用场景

- 项目已有ADR/PRD/SPEC等文档，需要将其纳入GSD规划体系
- 需要将多个规划文档合并到已有的GSD项目中
- 需要检测已有文档与GSD项目决策之间的冲突

注意：本skill在SOLO Coder中作为GSD工作流的辅助工具使用。

## 不适用场景

- 从零开始的项目（应使用gsd-new-project）
- 项目没有任何已有的规划文档
- 仅需查看单个文档

## 输出

- `.trae/gsd/planning/PROJECT.md`（全新模式）
- `.trae/gsd/planning/REQUIREMENTS.md`
- `.trae/gsd/planning/ROADMAP.md`
- `.trae/gsd/planning/STATE.md`
- `.trae/gsd/planning/INGEST-CONFLICTS.md`（如有冲突）

## 依赖

- gsd-roadmapper（生成路线图）
