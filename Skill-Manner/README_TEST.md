# 外部代码工具测试入口

## 项目用途

这是一个面向网页自动化 Agent 的通用图片处理 Skill 框架，当前重点测试“设计师被动训练”流程。

设计师不需要学习 Skill，也不需要填写复杂文档。测试时应让 Agent 主动提问，设计师只负责上传图片、选择选项、补充一句话、确认总结。

## 推荐测试顺序

1. 先读取 `framework/FRAMEWORK.md`
2. 再读取 `framework/ROUTING.md`
3. 测试设计师被动训练时，读取：
   - `designer-training/passive-mode/PASSIVE_TRAINING_PROTOCOL.md`
   - `designer-training/passive-mode/AGENT_INTERVIEW_SCRIPT.md`
   - `designer-training/passive-mode/AGENT_OUTPUT_CONTRACT.md`
   - `designer-training/passive-mode/REVIEW_QUEUE.md`
4. 根据测试任务再读取对应 skill：
   - `skills/model-image-generation/SKILL.md`
   - `skills/reference-image-to-prompt/SKILL.md`
   - `skills/reference-image-regeneration/SKILL.md`

## 测试目标

测试 Agent 是否能做到：

1. 不让设计师阅读框架。
2. 每轮最多问 3 个问题。
3. 优先使用选择题。
4. 把设计师的口语判断转成结构化训练记录。
5. 自动生成正向提示词、负面提示词和可复用标签。
6. 生成待审核知识库候选，而不是直接污染正式知识库。

## 通过标准

一次测试通过，需要输出：

1. 给设计师看的自然语言总结。
2. 给负责人的训练摘要。
3. 一条 records 格式的训练记录。
4. 一条 knowledge candidate。
5. 待审核状态。

## 不通过标准

以下情况视为失败：

1. 要求设计师阅读大量文档。
2. 要求设计师手动写 YAML、JSON 或提示词模板。
3. 一次问太多问题。
4. 没有生成结构化记录。
5. 没有区分正式知识库和待审核候选。
