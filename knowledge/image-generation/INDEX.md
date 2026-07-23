# 知识库索引

## 用途

本目录用于沉淀图片自动化任务中的可复用知识，包括提示词模板、标签体系、失败案例、参数经验和案例记录。

## 文件说明

| 文件或目录 | 说明 |
| --- | --- |
| taxonomy/image-types.yaml | 图片类型和任务类型分类 |
| taxonomy/prompt-dimensions.yaml | 逆向提示词分析维度 |
| taxonomy/reusable-tags.yaml | 可复用标签体系 |
| prompt-patterns | 成功提示词模板 |
| failure-cases.md | 失败案例和避坑规则 |
| parameter-recipes.md | 平台无关参数经验 |

## 沉淀规则

1. 每次执行都先写 records。
2. 被重复使用或人工评分高的记录，整理进 prompt-patterns。
3. 失败原因整理进 failure-cases。
4. 标签必须优先使用 taxonomy 中已有标签；新增标签时同步更新 taxonomy。
