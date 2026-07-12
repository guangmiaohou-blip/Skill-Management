---
name: unny-korean-minimal-beauty
description: UNNY 韩系极简美妆风格生成 Skill。用于用户要求韩系极简美妆、纯白棚拍、大地色低饱和、清冷或松弛人像、无产品变体、模特美妆图、参考图再生成时。支持高/中/低相似度，但执行参考图再生成前必须询问相似度；参考图文字、图形、logo、水印和产品默认去除。
---

# 风格目标

生成韩系极简美妆人像：纯白棚拍背景、大地色低饱和色彩、柔和漫射光、干净商业修图、清冷或松弛的年轻美妆模特气质。

该风格来自 `0010-UNNY测试版` 测试记录，当前作为候选风格 Skill 并入大框架。

## 适用场景

1. 韩系极简美妆人像。
2. 美妆品牌氛围图。
3. 无产品变体模特图。
4. 纯白棚拍、低饱和大地色、柔和光线的人像生成。
5. 参考图再生成中的高/中/低相似度测试。
6. 需要保留妆容、发型、肤感、氛围，但移除产品和品牌元素的任务。

## 不适用场景

1. 强剧情场景、户外大片、复杂背景。
2. 高饱和潮流视觉、赛博、暗黑、夸张妆造。
3. 明确要求保留参考图产品、logo、包装文字的任务。
4. 明确要求欧美硬光商业大片、奢华珠宝大片或强产品广告主视觉的任务。
5. 需要强动态动作、多人复杂互动或大场景构图的任务。

## 核心视觉特征

1. 纯白无缝棚拍背景。
2. 大地色低饱和色彩，常用暖棕、米色、白色、黑色。
3. 前左侧柔和漫射光，光线均匀，无硬阴影。
4. 干净商业棚拍质感，画面留白充足。
5. 美妆编辑片气质，整体克制、清爽、轻商业。
6. 肤质可精修，但必须保留真实细节，避免塑料皮。

## 人物与样貌规则

1. 年轻亚洲女性模特方向，脸部真实自然。
2. 可使用大眼、上挑眼线、裸粉唇、清透肤感作为风格 DNA。
3. 高相似时优先保留样貌、脸部比例、五官关系、妆容、发型和气质。
4. 中相似时保留发型、妆容、肤色、配色、光线和背景，允许姿态表情变化。
5. 低相似时只保留韩系极简氛围、纯白棚拍、大地色和柔和光线。
6. 避免过度成熟、过度网红、过度 AI 磨皮、脸部比例失真。

## 妆发与饰品规则

1. 妆容以自然裸妆、裸粉唇、清晰眼线、干净眼妆为主。
2. 可使用黑色短发、齐刘海、麻花辫作为高相似标志元素。
3. 发丝应清晰自然，避免糊成块。
4. 饰品默认弱化，不作为主视觉。
5. 如果参考图中有发饰、耳饰或小配饰，只有用户明确要求时才保留。
6. 饰品不得遮挡关键五官，不得破坏极简干净感。

## 服装与产品处理规则

必须继承大框架规则：

1. 参考图中的文字、logo、图形、水印、UI 和无关标识默认全部去除。
2. 参考图中的产品默认全部去除。
3. 若人物正在手持、佩戴、展示或靠近产品，保留人物动作、手部位置、身体姿态和视线方向，但移除产品本体。
4. 服装建议使用深棕麂皮、米色针织、奶油色或低饱和大地色单品。
5. 不生成产品包装、品牌字样、屏幕内容或商业标识。

## 构图与光线规则

1. 竖版 3:4 优先。
2. 近景或半身胸以上人像优先。
3. 纯白无缝背景，可保留 40%-60% 留白。
4. 镜头建议 50mm-85mm，中等景深，焦点在眼睛。
5. 光线为前左侧柔和漫射光，整体均匀。
6. 避免强阴影、复杂道具和背景装饰。

## 正向提示词模块

高相似模块：

```text
Young Asian female model, black straight bangs short hair at ear-length, two thick braids, big round eyes with sharp upturned eyeliner, natural nude makeup, pale nude pink lips, dewy glass skin with fine texture, earth tone outfit, lazy cold aloof expression, close-up chest and above portrait, pure white seamless studio background, generous negative space, front-left soft diffused light, Korean minimalist beauty editorial, clean commercial studio shot, warm brown white black low saturation palette, 50-85mm lens, focus on eyes, 3:4 aspect ratio, ultra realistic
```

中相似模块：

```text
Young Asian female beauty model with Korean minimalist styling, black neat hair, clean upturned eyeliner, nude lips, soft dewy skin, warm beige or brown outfit, relaxed natural gesture, calm side gaze, close-up chest and above portrait, pure white seamless studio background, soft front-left diffused light, earth tone warm minimal palette, clean serene commercial beauty editorial, 50mm lens, 3:4 aspect ratio, ultra realistic
```

低相似模块：

```text
Minimalist Korean beauty editorial photograph, elegant young model with natural makeup, soft dewy skin, simple natural hairstyle, cream and beige earth-tone outfit, calm serene expression, half-body portrait, pure white studio background, soft diffused light from left, clean airy atmosphere, muted warm color palette, sophisticated effortless vibe, 3:4 aspect ratio, ultra realistic commercial photography
```

## 负面提示词模块

```text
product, packaging, logo, text, watermark, UI, brand name, props, busy background, harsh shadow, overexposed skin, plastic skin, waxy face, distorted eyes, oversized eyes beyond reference, crossed eyes, asymmetrical face, broken fingers, extra fingers, deformed hands, heavy makeup, saturated colors, dark cinematic lighting, cluttered accessories, low resolution, cartoon, anime, illustration
```

## 推荐参数

```yaml
recommended_models:
  - 按平台能力选择最新图像模型
recommended_parameters:
  aspect_ratio: "3:4"
  size: "1024x1365 或平台接近尺寸"
  quality: high
  background: opaque
  style_strength: 待平台确认
similarity_policy: ask
```

## 质量检查

1. 是否保持韩系极简美妆风格。
2. 是否为纯白或近纯白无缝棚拍背景。
3. 是否去除了产品、logo、文字、水印和图形标识。
4. 人物样貌是否真实，脸部比例是否自然。
5. 眼睛是否对称、大小是否合理、视线是否自然。
6. 肤感是否有真实纹理，避免塑料皮。
7. 发丝和辫子是否清晰，不糊成块。
8. 大地色低饱和配色是否稳定。
9. 高/中/低相似度是否按用户选择执行。
10. 手部、肩颈、服装边缘是否存在明显畸形。

## 可复用标签

```yaml
reusable_tags:
  - style-skill
  - unny
  - korean-minimal-beauty
  - beauty-editorial
  - white-studio
  - earth-tone
  - no-product-variant
  - model-image-generation
  - reference-image-regeneration
```
