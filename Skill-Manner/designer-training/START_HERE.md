# 设计师被动训练入口

## 你需要做什么

你不需要学习代码，也不需要理解 Skill 框架。你只需要跟着 Agent 的问题回答，上传图片、选择选项、确认总结。

一句话理解：

```text
设计师负责判断好不好；Agent 负责追问、整理、写入和沉淀。
```

## 最简单的训练流程

每张图只做 4 步：

1. 上传图片。
2. 选择它是好案例还是失败案例。
3. 选择它哪里好或哪里失败。
4. 确认 Agent 的总结。

如果你使用的是被动训练流程，请让 Agent 读取：

```text
designer-training/passive-mode/PASSIVE_TRAINING_PROTOCOL.md
designer-training/passive-mode/AGENT_INTERVIEW_SCRIPT.md
```

## 你会训练到哪些能力

| Skill | 设计师要提供什么 |
| --- | --- |
| reference-image-to-prompt | 判断参考图哪里值得学习 |
| reference-image-regeneration | 判断相似度、保留项和避坑项 |
| model-image-generation | 判断模特图是否适合商业使用 |

## 设计师不需要做什么

1. 不需要写代码。
2. 不需要配置模型。
3. 不需要理解 JSON Schema。
4. 不需要一次性写完整知识库。
5. 不需要追求专业术语，先用准确的中文描述。

## Agent 应读取哪些文件

被动训练时，Agent 读取：

1. `passive-mode/AGENT_INTERVIEW_SCRIPT.md`
2. `passive-mode/AGENT_OUTPUT_CONTRACT.md`
3. `passive-mode/REVIEW_QUEUE.md`

如果训练材料来自设计师和 Agent 的历史对话，Agent 继续读取：

1. `conversation-context/CONVERSATION_CONTEXT_TRAINING.md`
2. `conversation-context/CONVERSATION_INTERVIEW_SCRIPT.md`

设计师不需要打开这些文件。
