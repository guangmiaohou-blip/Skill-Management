# 参考图逆向提示词流程

## 流程

1. 识别图片类型。
2. 按主体、细节、姿势、构图、光线、背景、材质、色彩、风格、镜头和后期质感拆解。
3. 生成中文正向提示词。
4. 生成中文负面提示词。
5. 给出通用推荐参数。
6. 输出可复用标签。
7. 写入图片分析记录。

## 输出骨架

```yaml
image_type:
analysis:
  subject:
  details:
  pose:
  composition:
  lighting:
  background:
  material:
  color:
  style:
  camera_language:
  post_processing:
positive_prompt:
negative_prompt:
recommended_parameters:
reusable_tags:
```
