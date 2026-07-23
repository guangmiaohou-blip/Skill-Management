# 参数经验

## 平台无关字段

```yaml
platform: 待定
model: 待定
aspect_ratio: 根据任务选择
similarity_level: 待确认
style_strength: 中
detail_strength: 中高
variation_strength: 中
image_reference_weight: 中
```

## 相似度建议

| 相似度 | 参考图权重 | 风格强度 | 变化强度 |
| --- | --- | --- | --- |
| 高相似 | 高 | 中 | 低 |
| 中相似 | 中 | 中 | 中 |
| 低相似 | 低 | 中高 | 高 |

## 模特图建议

```yaml
aspect_ratio:
  full_body: 2:3
  half_body: 3:4
  ecommerce: 1:1
detail_strength: 中高
negative_focus:
  - 手部
  - 四肢
  - 五官
  - 服装结构
```
