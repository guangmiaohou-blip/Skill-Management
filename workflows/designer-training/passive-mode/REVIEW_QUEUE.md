# 待审核队列规范

## 为什么需要待审核

设计师被动训练会产生大量候选知识。为了避免低质量内容直接污染正式 skill，所有训练结果先进入待审核队列。

## 队列状态

| 状态 | 说明 |
| --- | --- |
| 待审核 | Agent 已整理，负责人未确认 |
| 已通过 | 可以写入正式知识库 |
| 需修改 | 需要补充或调整 |
| 已拒绝 | 不进入知识库 |

## 审核人只需要判断

1. 这条经验是否可复用。
2. 提示词是否准确。
3. 负面提示词是否必要。
4. 标签是否合理。
5. 是否应该合并到已有模板。

## 待审核记录模板

```yaml
review_id:
status: 待审核
date:
designer:
reviewer:
skill:
case_type:
image_type:
task_intent:
summary:
positive_prompt:
negative_prompt:
reusable_tags:
proposed_knowledge_target:
review_notes:
```
