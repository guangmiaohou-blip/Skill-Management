---
name: commercial-model-card
description: Commercial model-card system for locking recurring product models C01 and C02 while allowing controlled appearance changes. Use when the user calls C01, C02, or another model card, needs consistent commercial product model imagery, asks to change makeup, skin tone, skin texture, hairstyle, wardrobe, pose, scene, or needs consumer-electronics e-commerce, social, poster, or product-demonstration images with a stable model identity.
---

# 商业模特卡

这是“模特卡系统”的主入口。当前支持 `C01` 和 `C02`。调用模特时，先锁定对应模特身份，再允许在可变外观层里调整妆容、肤色、肤质、发型、服装、表情、姿势和场景。

## 运行顺序

1. 识别用户调用的模特卡。当前支持 `C01` 与 `C02`；如果用户未指定，沿用当前上下文已明确的模特卡，不能在 C01 与 C02 之间自行切换。
2. 读取 `references/00-运行总则.md`。
3. 读取 `references/01-模特调用流程.md`。
4. 调用 C01 时读取：
   - `references/models/c01/C01-身份锁定.md`
   - `references/models/c01/C01-比例控制.md`
   - `references/models/c01/C01-参考图调用.md`
   - `references/models/c01/C01-可变外观层.md`
5. 调用 C02 时读取：
   - `references/models/c02/C02-身份锁定.md`
   - `references/models/c02/C02-比例控制.md`
   - `references/models/c02/C02-参考图调用.md`
   - `references/models/c02/C02-可变外观层.md`
6. 若用户要求面部细节回填，读取当前模特卡对应的 `[C01 或 C02]-面部细节局部回填.md`。该模块只处理完整面部身份、面部几何和常规可见细节，不得加载或执行眼部微距模块。若同时涉及头部结构、侧脸/三分之二侧脸/回眸、头饰或耳机导致的头部比例变化、脸身肤色统一、耳位或下颌校正，继续读取：
   - `[C01 或 C02]-独立头部结构强检测.md`
   - `[C01 或 C02]-局部回填与头部结构校验.md`
7. 只有用户明确点名“眼部”或“双眼”，并要求眼部微距局部回填、眼部裁切放大精修或调用当前模特眼部精修模块时，才读取并执行 `眼部微距局部回填.md`。仅出现“面部回填”“面部细节回填”或“裁切—放大—回填—合成”等通用工艺描述，不得触发眼部模块。
8. 面部细节回填与眼部细节回填严格分离：不得在同一次生成调用、同一裁片、同一遮罩或同一校验步骤中合并执行。用户同时要求两者时，必须先完成并验收面部回填，再把其输出作为眼部模块的输入单独执行。
9. 若用户要生成肤色、肤质、妆容、发型、服装等参考图，读取当前模特对应的 `预设参考图规则.md`。
10. 若用户指定或需要选择光源、棚拍、户外、柔箱、阴影、反光强弱，读取 `references/05-光源预设.md`。
11. 若涉及产品展示，读取 `references/02-产品展示规则.md`。
12. 组装提示词前读取 `references/03-提示词组装规则.md`。
13. 生成或编辑后读取 `references/04-结果校验与重试.md` 和当前模特对应的 `校验规则.md`。

## 最高优先级

冲突时按以下顺序处理：

1. 模特身份与身体一致性。
2. 产品保真。
3. 人物与产品交互可信。
4. 用户指定的场景、姿势、视觉风格。
5. 商业构图和卖点强化。

外观层可以改变“呈现”，不能重写“这个人是谁”。

## 资产位置

C01 资产位于 `assets/c01/`，C02 资产位于 `assets/C02/`。使用前按当前模特的参考图调用规则选择最小必要组合。严禁跨模特混用身份、头骨、身体、表情或眼部母版。
