# 参考图再生成流程

## 流程

1. 调用参考图逆向提示词流程。
2. 如果用户未指定相似度，先询问高相似、中相似或低相似。
3. 确定相似度档位。
4. 对人物图，优先提取样貌、脸部比例、五官关系、气质、发型妆容作为相似度保留项。
5. 将动作、手势、姿势、构图和机位标记为可变化项，除非用户明确要求保留。
6. 将参考图中的文字、logo、图形符号、水印、UI 和无关标识放入必须避免项。
7. 将参考图中的产品放入必须去除项；如果人物正在手持或展示产品，保留人物动作、手部位置和互动关系。
8. 生成再生成提示词。
9. 给出平台无关参数建议。
10. 如已知平台，则补充平台专用参数。
11. 写入生成记录。

## 输出骨架

```yaml
similarity_level: 待确认
preserve:
  appearance:
  face_proportion:
  facial_features:
  temperament:
  hair_and_makeup:
change_allowed:
  pose:
  gesture:
  composition:
  camera_angle:
avoid:
  text_and_logo:
  graphic_symbols:
  watermark:
  products:
preserve_action_when_removing_product:
  hand_position:
  body_pose:
  gaze_direction:
  interaction_relation:
positive_prompt:
negative_prompt:
recommended_parameters:
reusable_tags:
```
