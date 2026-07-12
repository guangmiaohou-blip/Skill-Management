# Agent 输出契约

## 用途

当 Agent 完成一次被动训练访谈后，必须生成以下后台结果。

## 给设计师看的结果

只输出自然语言：

```text
已整理完成。

这张图会作为【好案例/失败案例】训练【xxx】能力。
Agent 将学习【xxx】。
之后遇到类似任务时，会优先保留【xxx】，避免【xxx】。
```

## 给负责人看的结果

输出摘要：

```yaml
training_summary:
  skill:
  case_type:
  image_type:
  task_intent:
  designer:
  date:
  reusable_value:
  review_status: 待审核
```

## 写入 records 的结果

必须包含：

```yaml
record_type:
version:
date:
operator:
classification:
  image_type:
  task_intent:
  selected_skill:
prompts:
  positive_prompt:
  negative_prompt:
recommended_parameters:
  platform:
  model:
  similarity_level:
reusable_tags:
knowledge_capture:
  save_to_prompt_patterns:
  save_to_failure_cases:
```

## 写入知识库的候选内容

Agent 不直接覆盖正式知识库，而是先生成候选：

```yaml
knowledge_candidate:
  target_file:
  change_type: 新增 | 更新 | 合并
  proposed_content:
  reason:
  review_status: 待审核
```

## 质量门槛

如果以下任意信息缺失，Agent 必须继续追问：

1. 图片类型。
2. 好案例或失败案例。
3. 至少一个可学习点或失败点。
4. 适用 skill。

如果设计师无法判断，Agent 可以先标记为 `待负责人审核`。
