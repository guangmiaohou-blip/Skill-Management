# 可复用案例

```yaml
case_id: xiaomi-disney-100th
version: v0.1
date: 2026-07-06
operator: WorkBuddy
image_type: 产品联名海报（3张系列图）
task_intent: A1 三张分别逆向 + 按高/中/低相似度分档生成
platform: 待定
model: 待定
similarity_level: 高/中/低（三档各3张）
reusable_tags:
  - IP联名产品海报
  - 迪士尼联名
  - 米奇限定版
  - 红黑撞色配色
  - 日系少女风
  - 商业棚拍白底
  - 手绘涂鸦装饰
  - Z世代审美
```

## 输入

图片路径：
- 用户上传 3 张产品海报（文件名经系统过滤，画面由多模态模型读取）：
  - 图1：小米 CIVI 3 · 迪士尼 100 周年限定版（手机）
  - 图2：小米手环 8 · 迪士尼 100 周年限定版
  - 图3：小米真无线降噪耳机 3 · 迪士尼 100 周年限定版

用户需求：
- 对 3 张参考图分别走 13 维逆向分析（A1）
- 基于分析，按高 / 中 / 低相似度各生成 3 张变体（共 9 张）

## 分析摘要

**系列共享 DNA（三张一致）**

| 维度 | 内容 |
| --- | --- |
| 模特 | 同一人：黑齐刘海 bob 短发 + 超大哑光红圆耳环 |
| 配色 | 红黑白三角撞色，米奇红 `#D32F2F` 为主 |
| 背景 | 纯白无缝底 + 手绘涂鸦（每张符号不同） |
| 布光 | 商业棚拍柔光，软光无硬阴影 |
| 后期 | CG 级精修，磨皮保纹理，纯净数字感 |
| 风格 | 日系少女 × 波普漫画涂鸦 × IP 联名 |

**三张差异设计**

|      | 图1 CIVI3 | 图2 手环8  | 图3 耳机3        |
| ---- | -------- | ------- | ------------- |
| 服装   | 白+黑学院领   | 黑红撞色心形摆 | 黑主+白翻领+choker |
| 手势   | 双手持机     | 食指指点    | 掌托充电仓+佩戴      |
| 表情   | 俏皮惊讶     | 甜美微笑    | 温柔微笑          |
| 视角   | 3/4侧脸正对  | 正面偏侧    | 纯侧脸           |
| 涂鸦   | 红星×2     | 闪烁线+皇冠  | 闪烁线+心形        |
| 红色元素 | 2处       | 3处      | 4处（最密）        |
|      |          |         |               |

## 正向提示词

```text
【系列通用骨架】
年轻亚洲女性模特，黑色齐刘海 bob 短发及下巴、两侧微内扣，大圆眼自然粉妆、红唇，
超大号哑光红色圆形耳环；近景胸以上肖像，居中略偏左，大面积纯白背景留白约 50-60%，
平视微仰、3/4 侧脸；正面偏左顶柔光、软光无硬阴影、轻微轮廓光；纯白无缝背景纸 +
手绘涂鸦装饰；皮肤光滑细腻商业精修保留毛孔纹理，CG 级重度精修保持写实；
主色高饱和米奇红 #D32F2F + 黑 #1A1A1A + 白 #FAFAFA 三角撞色，中性偏暖 5500K-6000K；
商业广告产品摄影 × 日系少女清新 × 波普漫画涂鸦，活泼俏皮年轻潮流；
等效 50-85mm 人像焦段 f/4-f/5.6 中景深，静态摆拍。

【图2 手环8 差异补丁】黑红撞色针织上衣（红心形下摆），食指指点红色手环，甜美微笑，
涂鸦=闪烁线+皇冠，红色元素3处。
【图3 耳机3 差异补丁】黑主+白翻领+黑色 choker 颈链，右耳佩戴红耳机+左手掌托红充电仓
+左腕红手表，温柔微笑，纯侧脸，涂鸦=闪烁线+心形，红色元素4处。
```

## 负面提示词

```text
模糊失焦、手指变形多指或数量错误、五官不对称大小眼、肢体比例失调、表情僵硬死板、
产品变形扭曲、摄像头/表带比例失调、IP 米奇图案变形或颜色偏差、皮肤塑料蜡感失去纹理、
服装褶皱不自然、玻璃/塑料反光异常、耳环高光异常、画面噪点过多、光线不均硬影、
背景非纯白出现杂色、色彩偏色溢色、氛围阴郁沉闷、锐化过度轮廓发白、压缩伪影、
构图裁切不当主体偏离中心。
```

## 推荐参数

```yaml
aspect_ratio: 3:4          # 竖版半身
quality: high
background: opaque         # 纯白不透明
similarity_levels:
  high:
    similarity: 高
    style_strength: 中高   # 保留品牌+IP元素
    detail_strength: 高    # 产品细节需精确
  mid:
    similarity: 中
    style_strength: 中高
    detail_strength: 中高
  low:
    similarity: 低
    style_strength: 中高
    detail_strength: 中
```

## 分档生成记录

### 🔴 高相似（3张）— 还原构图/配色/手势/表情
- `generated-images/Commercial_product_advertiseme_2026-07-06T09-29-02.png`（图1 CIVI3）
- `generated-images/Commercial_product_advertiseme_2026-07-06T09-27-59.png`（图2 手环8）
- `generated-images/Commercial_product_advertiseme_2026-07-06T09-29-34.png`（图3 耳机3）

### 🟡 中相似（3张）— 保留 DNA，放宽产品细节/手势/涂鸦/表情
- `generated-images/sim_mid1/Commercial_product_advertiseme_2026-07-06T09-32-47.png`（phone）
- `generated-images/sim_mid2/Commercial_product_advertiseme_2026-07-06T09-33-48.png`（band）
- `generated-images/sim_mid3/Commercial_product_advertiseme_2026-07-06T09-33-19.png`（earbuds）

### 🟢 低相似（3张）— 仅留 DNA，姿态/服装/产品/表情自由发挥
- `generated-images/sim_low1/Stylish_product_ad_photo__youn_2026-07-06T09-40-10.png`（phone）
- `generated-images/sim_low2/Stylish_product_ad_photo__youn_2026-07-06T09-40-37.png`（band）
- `generated-images/sim_low3/Stylish_product_ad_photo__youn_2026-07-06T09-41-23.png`（earbuds）

## 结果评价

成功点：
- 系列 DNA（模特气质+红黑白撞色+白底涂鸦+商业柔光+CG精修）三档均高度一致复刻
- 高→中→低相似度递进清晰，满足"1:1复刻 / 系列变体 / 全新创作"三档需求

失败点：
- AI 无法精确复刻真实品牌 logo（MI）、米奇图案精确比例、摄像头模组结构
- 并行生成触发文件名时间戳冲突（图1/图3 覆盖），已改顺序调用解决

复用建议：
- 换 IP / 换产品 / 换模特均可套用本系列 DNA 骨架（见系列共享 DNA 表）
- 多张生成务必顺序调用 ImageGen，避免文件串目录覆盖
