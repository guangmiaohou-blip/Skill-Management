# 风格 Skill 路由规则

## 目标

本文件用于管理小风格 Skill 如何被大框架调用。大框架先判断任务类型，再判断是否需要加载风格 Skill。

## 路由顺序

1. 判断用户任务是否属于图片生成、参考图再生成或提示词生成。
2. 读取 `knowledge/style-registry.yaml`。
3. 根据用户关键词、图片类型、任务类型和设计师指定风格匹配候选风格 Skill。
4. 如果只匹配到一个 `active` 风格 Skill，加载该风格 Skill。
5. 如果匹配到多个风格 Skill，最多列出 3 个选项让用户选择。
6. 如果匹配到 `candidate` 风格 Skill，先提示它处于待审核状态，再询问是否临时使用。
7. 如果没有匹配项，使用通用 `model-image-generation` 或 `reference-image-regeneration`。

## 调用规则

风格 Skill 只能补充风格规则，不得覆盖以下大框架规则：

1. 参考图再生成前必须询问相似度。
2. 相似度优先体现在样貌、脸部比例、五官关系、气质、妆发和真实感上。
3. 参考图文字、logo、图形、水印、UI 和无关标识默认全部去除。
4. 参考图产品默认全部去除。
5. 去除产品时，默认保留人物动作、手部位置、身体姿态、视线方向和互动关系。
6. 每次执行都输出可复用记录和知识库候选。

## 多风格处理

当用户同时要求多个风格时：

1. 必须确定一个主风格。
2. 其他风格只能作为辅助元素。
3. 如果风格之间冲突，以主风格为准。
4. 如果无法判断主风格，向用户询问，最多提供 3 个选项。

## 匹配字段

路由时优先使用以下字段：

```yaml
skill_id: 唯一标识
display_name: 中文展示名
status: active | candidate | archived
supported_tasks: 支持任务
triggers: 触发词
image_types: 图片类型
similarity_policy: ask
mandatory_global_rules: 大框架继承规则
reusable_tags: 可复用标签
```

## 输出要求

每次调用风格 Skill 时，在执行记录里写明：

```yaml
style_skill:
  skill_id: ""
  display_name: ""
  version: ""
  status: ""
  match_reason: ""
  primary_or_secondary: primary
```
