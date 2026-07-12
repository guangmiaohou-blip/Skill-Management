# 自动图片路由流程

## 适用场景

用户上传图片后，Agent 自动判断任务类型并选择 skill。

## 流程

1. 读取用户上传图片和文字需求。
2. 判断图片类型。
3. 判断用户意图。
4. 根据 `framework/ROUTING.md` 选择 skill。
5. 执行对应 skill。
6. 输出分析结果、提示词、负面提示词和推荐参数。
7. 按 `records/templates/image-analysis-record.yaml` 或 `records/templates/generation-run-record.yaml` 记录本次结果。

## 默认策略

如果用户只上传图片，没有明确说明用途：

1. 执行 `reference-image-to-prompt`。
2. 输出图片分析和提示词。
3. 标记 `next_action: 等待用户确认是否生成图片`。

## 输出格式

```yaml
router_result:
  image_type:
  task_intent:
  selected_skill:
  confidence:
  reason:
  next_action:
```
