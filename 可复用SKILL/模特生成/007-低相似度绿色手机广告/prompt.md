# 低相似度绿色手机时尚广告生成记录

## 任务分类

```yaml
image_type: 混合参考图 / 手机产品广告 / 时尚模特图
task_intent: 参考图再生成
selected_skill: reference-image-regeneration
similarity_level: 低相似
face_proportion_mode: 真实商业模特比例
model: gpt-image-2
status: 可复用案例候选
```

## 低相似度策略

保留：

- 绿色手机产品广告方向
- 橄榄绿 / 鼠尾草绿主色
- 年轻女性时尚模特
- 干净极简棚拍海报感
- 大圆形摄像头模组
- 真实商业模特比例

允许变化：

- 不复制原图标题区
- 不复制原图伸手横向递手机姿态
- 不复制原图圆角背景块版式
- 可重新设计站姿、手机摆放方式、背景图形和构图
- 可从手机海报转为更完整的绿色科技时尚大片

## 正向提示词

```text
Use case: ads-marketing
Asset type: low-similarity smartphone fashion advertisement reinterpretation
Primary request: Generate one vertical smartphone fashion advertisement with LOW similarity to the reference. Keep only the broad visual DNA: sage-green smartphone, olive fashion styling, young female model, clean minimalist fashion-tech campaign, pale green/grey palette. Reimagine the pose, framing, and graphic layout.

Scene/backdrop: minimalist pale grey studio with abstract sage-green rectangular shapes or a soft translucent green panel, modern high-end product campaign. No readable text, no real brand names, no logos, no watermark.

Subject: young adult female fashion model, realistic commercial model proportions, sleek black hair in a sculptural bun, confident fresh expression, natural makeup, real skin texture, elegant fashion attitude.

Wardrobe: olive green ribbed knit sleeveless turtleneck or structured knit top, matching modern skirt or trousers, clean monochrome styling.

Product: matte sage-green smartphone with rounded corners and large circular black camera module, displayed prominently either on a slim pedestal in the foreground or held at arm's length in a new pose. No readable brand text. Product should be sharp and realistic.

Composition/framing: vertical 2:3 editorial poster. Reimagined setup: model standing in a three-quarter full/half-body pose, one hand on hip, the other presenting the phone near shoulder level or placing it on a floating green platform; stronger graphic negative space than the reference, not the same leaning side pose.

Lighting/mood: soft bright studio lighting, crisp modern product highlights, calm premium tech-fashion mood.

Color palette: pale sage, olive green, light grey-white, black hair, natural warm skin.

Materials/textures: ribbed knit fabric, matte phone finish, glass camera lenses, realistic skin texture, natural hair flyaways.

Face proportion mode: realistic commercial model proportions, not idol close-up beauty.

Constraints: low similarity: do not copy the exact poster layout, title area, arm extension, or horizontal phone pose. Preserve only green fashion-tech smartphone advertising direction and clean commercial style.
```

## 负面提示词

```text
readable text, REDMI, Xiaomi, real logos, watermark, malformed hands, extra fingers, distorted phone, warped camera circle, plastic skin, waxy skin, over-smoothed skin, uncanny face, overly large eyes, doll-like proportions, messy background, harsh shadows, low resolution
```

## 推荐参数

```yaml
aspect_ratio: 2:3
style_strength: 中高
detail_strength: 中高
variation_strength: 高
image_reference_weight: 低
background: 极简浅灰 / 鼠尾草绿图形背景
product_color: matte sage green
negative_focus:
  - 品牌文字
  - 手机结构变形
  - 手部错误
  - 过度美颜
  - 偶像大眼比例
```

## 可复用标签

```text
低相似度再创作, 绿色手机广告, 鼠尾草绿科技感, 橄榄绿时尚造型, 极简棚拍海报, 真实商业模特比例, 圆形摄像头模组, 手机产品大片, 清爽高级科技广告, 无品牌文字
```

## 复用建议

这个模板适合把强品牌参考图转成“同方向但不复刻”的新广告概念。  
如果后续要继续生成同系列，可以只替换 `product_color`、`wardrobe` 和 `background`，保留低相似度策略与负面提示词。
