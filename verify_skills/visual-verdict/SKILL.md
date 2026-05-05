---
name: visual-verdict
description: Structured visual QA verdict for screenshot-to-reference comparisons. Use when comparing generated UI screenshots against reference images with deterministic pass/fail guidance.
---

# Visual Verdict

## 描述

使用此技能将生成的 UI 截图与一个或多个参考图像进行比较，并返回严格的 JSON 判定结果，可驱动下一次编辑迭代。

## 使用场景

- 任务包含视觉保真度要求（布局、间距、排版、组件样式）
- 你有生成的截图和至少一张参考图像
- 你需要在继续编辑前获得确定性的通过/失败指导

## 指令

### 输入

- `reference_images[]`（一个或多个图像路径）
- `generated_screenshot`（当前输出图像）
- 可选：`category_hint`（例如 `hackernews`、`sns-feed`、`dashboard`）

### 输出

仅返回 **JSON**，具有以下精确结构：

```json
{
  "score": 0,
  "verdict": "revise",
  "category_match": false,
  "differences": ["..."],
  "suggestions": ["..."],
  "reasoning": "short explanation"
}
```

规则：
- `score`：整数 0-100
- `verdict`：简短状态（`pass`、`revise` 或 `fail`）
- `category_match`：当生成的截图匹配预期的 UI 类别/风格时为 `true`
- `differences[]`：具体的视觉不匹配（布局、间距、排版、颜色、层次）
- `suggestions[]`：与差异关联的可操作下一步编辑
- `reasoning`：1-2 句摘要

### 通过阈值

- 目标通过阈值为 **90+**
- 如果 `score < 90`，继续编辑并重新运行 visual-verdict 再进行任何进一步的视觉审查
- 在下一次截图通过阈值之前，**不要**将视觉任务视为完成

### 困难不匹配诊断

当不匹配诊断困难时：
1. 保持 visual-verdict 作为权威决策
2. 使用像素级差异工具（像素差异 / pixelmatch 叠加）作为**辅助调试手段**来定位热点
3. 将像素差异热点转换为具体的 `differences[]` 和 `suggestions[]` 更新

## 示例

```json
{
  "score": 87,
  "verdict": "revise",
  "category_match": true,
  "differences": [
    "Top nav spacing is tighter than reference",
    "Primary button uses smaller font weight"
  ],
  "suggestions": [
    "Increase nav item horizontal padding by 4px",
    "Set primary button font-weight to 600"
  ],
  "reasoning": "Core layout matches, but style details still diverge."
}
```