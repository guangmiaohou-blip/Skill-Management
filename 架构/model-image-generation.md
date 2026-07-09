# 模特图生成流程

## 流程

1. 判断模特图类型。
2. 判断是否需要身份一致性。
3. 分析产品、服装、姿势、场景和风格要求。
4. 生成模特设定。
5. 生成正向提示词和负面提示词。
6. 给出推荐参数。
7. 检查人体、产品、服装和商业质感风险。
8. 写入生成记录。

## 输出骨架

```yaml
model_image_type:
identity_consistency:
scene_goal:
model_setting:
product_or_clothing:
pose:
composition:
lighting:
style:
positive_prompt:
negative_prompt:
recommended_parameters:
quality_check:
reusable_tags:
```
