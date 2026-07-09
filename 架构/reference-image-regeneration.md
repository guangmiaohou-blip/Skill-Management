# 参考图再生成流程

## 流程

1. 调用参考图逆向提示词流程。
2. 确定相似度档位。
3. 把画面元素分为必须保留、允许变化、必须避免。
4. 生成再生成提示词。
5. 给出平台无关参数建议。
6. 如已知平台，则补充平台专用参数。
7. 写入生成记录。

## 输出骨架

```yaml
similarity_level: 中相似
preserve:
change_allowed:
avoid:
positive_prompt:
negative_prompt:
recommended_parameters:
reusable_tags:
```
