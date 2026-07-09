# reference-image-regeneration

## 用途

当用户上传参考图，并希望重新生成相似图、保留风格、复刻视觉方向或基于参考图再创作时，使用本 skill。

## 输入

```yaml
image: 用户上传参考图
user_request: 用户原始需求
similarity_level: 高相似 | 中相似 | 低相似
language: 中文
```

如果用户没有指定相似度，默认使用中相似。

## 输出

必须输出：

1. 图片类型。
2. 自动分类结果。
3. 相似度档位。
4. 正向提示词。
5. 负面提示词。
6. 推荐参数。
7. 可复用标签。
8. 生成执行建议。
9. 可写入 records 的结构化记录。

## 相似度控制

### 高相似

保留：

1. 主体身份或产品外观。
2. 构图和景别。
3. 视角和镜头感。
4. 光影关系。
5. 背景结构。
6. 材质和颜色。

### 中相似

保留：

1. 主体类型。
2. 核心风格。
3. 主要构图关系。
4. 光线氛围。
5. 关键材质或颜色。

允许变化：

1. 背景细节。
2. 姿势或动作。
3. 道具。
4. 次要颜色。

### 低相似

保留：

1. 风格方向。
2. 情绪。
3. 色彩倾向。
4. 商业用途。

允许重新创作主体、构图和场景。

## 执行步骤

1. 先使用 `reference-image-to-prompt` 的分析维度拆解参考图。
2. 根据相似度档位筛选需要保留和允许变化的元素。
3. 生成正向提示词和负面提示词。
4. 给出推荐参数。
5. 如平台支持参考图权重，给出参考图权重建议。
6. 输出可复用记录。

## 参数建议

```yaml
high_similarity:
  image_reference_weight: 高
  style_strength: 中
  variation_strength: 低
medium_similarity:
  image_reference_weight: 中
  style_strength: 中
  variation_strength: 中
low_similarity:
  image_reference_weight: 低
  style_strength: 中高
  variation_strength: 高
```

## 质量检查

生成前检查：

1. 是否明确保留主体。
2. 是否明确允许变化的部分。
3. 是否避免直接复制水印、商标、隐私信息。
4. 是否给出负面提示词。
5. 是否记录平台、模型、日期、操作人和版本。
