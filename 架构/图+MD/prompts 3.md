# OPPO Enco Clip2 × Watch X3 Mini 模特图生成 · 提示词包

- **生成日期**：2026-07-06
- **目标平台**：GLM-5.2（已规避真品牌字样）
- **风格类型**：商业广告人像 / 穿戴展示
- **风格锁定**：暖米色棚拍 × 香槟金缎面 × 同一虚拟模特 × 4 机位
- **关联训练记录**：RC-2026-07-06-001
- **关联知识库候选**：KC-2026-07-06-001

---

## 通用角色设定（4 张共用）

同一东亚女性，25-28 岁，鹅蛋脸，杏仁眼，暖铜色修容，裸粉雾面唇，皮肤自然光泽；低盘发 + 飞絮；香槟金缎面露背吊带礼服（液态金属高光）；金色细环耳饰；右耳金边银色耳夹式耳机；左腕金带珍珠白表盘腕表（花纹字）；暖米→浅咖径向渐变棚拍背景；柔光侧打 + 头发轮廓光；85mm / f2.0 浅景深。

## Shot 1 — 3/4 侧半身 + 手触耳夹

```
Editorial commercial product advertising photograph, three-quarter side view half-body portrait of the same young East Asian woman, 25-28 years old, refined oval face, soft almond eyes, subtle warm bronze contour makeup, nude-matte dusty-rose lips, luminous natural skin texture with healthy glow, hair in a low chignon bun with a few loose flyaway strands, wearing a champagne-gold silk satin backless slip dress with liquid-metal highlights, gold thin hoop earrings, a gold-rim silver clip-on earbud on her right ear, a thin gold-band wristwatch with pearl-white dial and floral numerals on her left wrist, her right hand gently touching the clip-on earbud, fingers relaxed, gaze softly lowered toward camera-left, warm beige to light taupe radial gradient studio backdrop, soft directional side lighting from camera-right with gentle fill, subtle rim light on hair, shot on 85mm lens, f/2.0 shallow depth of field, vertical advertising key visual composition, ultra realistic, fine skin pores, 8K detail, no text, no watermark, no logo
```

## Shot 2 — 正面半身 + 手抚发髻（腕表落在右 1/3 黄金位）

```
Editorial commercial product advertising photograph, frontal half-body portrait of the same young East Asian woman, 25-28 years old, refined oval face, soft almond eyes, subtle warm bronze contour makeup, nude-matte dusty-rose lips, luminous natural skin texture, hair in a low chignon bun with a few loose flyaway strands, wearing a champagne-gold silk satin backless slip dress with liquid-metal highlights, gold thin hoop earrings, a gold-rim silver clip-on earbud on her right ear, her right hand gracefully resting near her hair bun at the back of her head, the thin gold-band wristwatch with pearl-white dial and floral numerals on her left wrist clearly visible and placed at the right-third golden ratio of the frame, calm confident gaze looking directly into camera, warm beige to light taupe radial gradient studio backdrop, soft directional lighting from camera-right, gentle rim light on shoulders, shot on 85mm lens, f/2.0 shallow depth of field, vertical advertising key visual composition, ultra realistic, fine skin pores, 8K detail, no text, no watermark, no logo
```

## Shot 3 — 背身回眸 + 耳夹特写

```
Editorial commercial product advertising photograph, back view with head turned three-quarter over her shoulder, half-body portrait of the same young East Asian woman, 25-28 years old, refined oval face seen in profile, soft almond eyes, subtle warm bronze contour makeup, nude-matte dusty-rose lips, luminous natural skin texture, hair in a low chignon bun with a few loose flyaway strands exposing her neckline and the gold thin hoop earring plus a gold-rim silver clip-on earbud on her right ear shown in sharp focus as the visual hero, wearing a champagne-gold silk satin backless slip dress with liquid-metal highlights revealing her bare back, a thin gold-band wristwatch with pearl-white dial and floral numerals on her left wrist resting along her collarbone, soft gaze back toward camera, warm beige to light taupe radial gradient studio backdrop, soft directional lighting from camera-left emphasizing the earbud, gentle rim light along her back silhouette, shot on 85mm lens, f/2.0 shallow depth of field, vertical advertising key visual composition, ultra realistic, fine skin pores, 8K detail, no text, no watermark, no logo
```

## Shot 4 — 90° 侧颜 + 左 1/3 留白（给品牌文案）

```
Editorial commercial product advertising photograph, ninety-degree pure side profile portrait of the same young East Asian woman, 25-28 years old, refined oval face in sharp profile, soft almond eyes, subtle warm bronze contour makeup, nude-matte dusty-rose lips, luminous natural skin texture, hair in a low chignon bun with a few loose flyaway strands, long graceful neck and jawline as the visual hero, wearing a champagne-gold silk satin backless slip dress with liquid-metal highlights, gold thin hoop earrings, a thin gold-band wristwatch with pearl-white dial and floral numerals on her left wrist softly visible, body placed at the right two-thirds of the frame leaving the left third as clean empty negative space for brand copy, calm gaze directed forward, warm beige to light taupe radial gradient studio backdrop, soft directional lighting from camera-front, gentle rim light tracing her profile, shot on 85mm lens, f/2.0 shallow depth of field, vertical advertising key visual composition, ultra realistic, fine skin pores, 8K detail, no text, no watermark, no logo
```

## 通用负面提示词

```
text, watermark, logo, brand name, OPPO, Enco, Watch, X3, Mini, low quality, blurry, deformed fingers, extra fingers, missing fingers, deformed hands, plastic skin, waxy skin, over-smoothed skin, cartoon, anime, illustration, 3d render, busy background, harsh shadow, multiple people, cropped face, mutated limbs, deformed ears, wrong anatomy, distorted watch dial, distorted earbud, plain cotton fabric (anti-satin)
```

## 推荐参数

| 参数 | 值 | 说明 |
| --- | --- | --- |
| 尺寸 | 1024×1536 | 竖版广告主图 |
| 质量 | high | 商业级 |
| 步数 | ≥35 | 缎面需要足够步数承载液态金属高光 |
| 采样器 | Karras | 平滑肤色 + 金属反光 |
| CFG | 7–8 | 商业广告常用区间 |
| seed | 4 张保持一致 | 锁定同一虚拟模特身份 |

## 可复用标签

`#商业广告` `#穿戴展示` `#棚拍` `#暖米色背景` `#缎面材质` `#香槟金` `#东亚女性` `#低盘发` `#同一虚拟模特` `#4机位` `#侧颜留白` `#耳夹式耳机` `#珍珠表盘` `#轻奢` `#85mm人像` `#浅景深`

## 视觉一致性检查表

- [ ] 4 张为同一面部特征、同一发型、同一肤色
- [ ] 4 张服装材质均呈现缎面液态金属高光（非棉布）
- [ ] 4 张背景均为暖米→浅咖径向渐变
- [ ] 耳夹在每张中可识别为「clip-on earbud」而非普通耳环
- [ ] 腕表表盘为珍珠白 + 花纹字（非纯白）
- [ ] 无任何 OPPO / Enco / Watch / X3 / Mini 字样
- [ ] 手指数量正确，无畸形
- [ ] Shot 2 腕表位于画面右 1/3
- [ ] Shot 4 左 1/3 为干净留白

## 风险与避坑

1. **缎面塌成棉布**：弱模型下高光会消失，强制 ≥35 步 + Karras。
2. **耳夹误成耳环**：必须显式写 `gold-rim silver clip-on earbud`。
3. **腕表表盘花纹糊**：必须显式写 `pearl-white dial, floral numerals`。
4. **品牌字样**：Nano Banana 对真品牌字样会主动拒出，提示词末尾的 `no text, no watermark, no logo` + 负面提示词双保险。
5. **身份漂移**：4 张并行生成容易面部不一致，建议串行 + 同 seed；本批因并行触发时间戳撞秒，已补齐。
