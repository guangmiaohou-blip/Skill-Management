---
name: commercial-model-card
description: Commercial model-card system for locking a recurring product model while allowing controlled appearance changes. Use when the user calls C01 or another model card, needs consistent commercial product model imagery, asks to change makeup, skin tone, skin texture, hairstyle, wardrobe, pose, scene, or needs consumer-electronics e-commerce, social, poster, or product-demonstration images with a stable model identity.
---

# 商业模特卡

这是“模特卡系统”的主入口。先支持 `C01`。调用模特时，先锁定模特身份，再允许在可变外观层里调整妆容、肤色、肤质、发型、服装、表情、姿势和场景。

## 运行顺序

1. 识别用户调用的模特卡。当前只支持 `C01`；如果用户未指定但上下文指向当前女模特，默认使用 `C01`。
2. 读取 `references/00-运行总则.md`。
3. 读取 `references/01-模特调用流程.md`。
4. 调用 C01 时读取：
   - `references/models/c01/C01-身份锁定.md`
   - `references/models/c01/C01-参考图调用.md`
   - `references/models/c01/C01-可变外观层.md`
5. 若用户要生成肤色、肤质、妆容、发型、服装等参考图，读取 `references/models/c01/C01-预设参考图规则.md`。
6. 若用户指定或需要选择光源、棚拍、户外、柔箱、阴影、反光强弱，读取 `references/05-光源预设.md`。
7. 若涉及产品展示，读取 `references/02-产品展示规则.md`。
8. 组装提示词前读取 `references/03-提示词组装规则.md`。
9. 生成或编辑后读取 `references/04-结果校验与重试.md` 和 `references/models/c01/C01-校验规则.md`。

## 最高优先级

冲突时按以下顺序处理：

1. 模特身份与身体一致性。
2. 产品保真。
3. 人物与产品交互可信。
4. 用户指定的场景、姿势、视觉风格。
5. 商业构图和卖点强化。

外观层可以改变“呈现”，不能重写“这个人是谁”。

## 资产位置

C01 参考图资产位于 `assets/c01/`。使用前按 `C01-参考图调用.md` 选择最小必要组合，不要无差别加载所有图片。
