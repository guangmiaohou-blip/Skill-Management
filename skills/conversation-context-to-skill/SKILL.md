---
name: conversation-context-to-skill
description: 读取设计师与 Agent 的对话上下文，提取明确判断、稳定方法、失败规则和待确认信息，生成训练记录、知识库候选以及新的 Skill 草案或现有 Skill 更新候选。用于对话训练、经验沉淀和 Skill 创建。
---

# conversation-context-to-skill

## 用途

当用户要求 Agent 阅读、整理设计师与 Agent 的历史对话，并根据对话内容训练 Skill、更新知识库或创建新的 Skill 草案时，使用本 Skill。

典型触发：

1. “根据刚才设计师和 Agent 的对话训练一下。”
2. “把这段上下文整理成 Skill。”
3. “从设计师反馈里提炼规则。”
4. “根据这轮训练创建一个新的 Skill。”
5. “整理历史对话，沉淀成知识库。”

## 输入

```yaml
conversation_context: 设计师与 Agent 的对话文本或当前上下文
related_images: 可选，相关图片路径或编号
target_skill: 可选，已有 Skill 名称
creation_mode: 更新已有 Skill | 创建新 Skill | 生成待审核候选
operator: 操作人
date: YYYY-MM-DD
```

## 输出

必须输出：

1. 对话摘要。
2. 设计师明确表达的判断。
3. Agent 推断出的规则。
4. 待确认信息。
5. 可训练内容。
6. 正向提示词候选。
7. 负面提示词候选。
8. 可复用标签。
9. 知识库候选。
10. Skill 创建或更新草案。
11. 审核状态。

## 执行流程

### 1. 整理对话

从对话中提取：

| 字段 | 说明 |
| --- | --- |
| task_goal | 这轮对话要解决什么图片任务 |
| image_type | 图片类型 |
| task_intent | 任务意图 |
| designer_judgement | 设计师对好坏、风格、问题的判断 |
| keep_rules | 生成时必须保留的元素 |
| change_rules | 允许变化的元素 |
| avoid_rules | 必须避免的问题 |
| quality_standard | 好图标准 |
| reusable_context | 适合复用的场景 |

### 2. 区分来源

所有规则必须标注来源：

```yaml
source_type: designer_explicit | agent_inferred | needs_confirmation
```

含义：

| 来源 | 说明 |
| --- | --- |
| designer_explicit | 设计师明确说过，可以优先沉淀 |
| agent_inferred | Agent 根据上下文推断，需要审核 |
| needs_confirmation | 信息不足，需要设计师或负责人确认 |

### 3. 判断是更新还是创建

如果对话内容属于已有三类能力，则更新已有 Skill 候选：

1. reference-image-to-prompt
2. reference-image-regeneration
3. model-image-generation

如果对话中出现新的稳定任务类型，则创建新 Skill 草案。

新 Skill 草案必须包含：

```yaml
skill_name:
skill_purpose:
trigger_scenarios:
inputs:
outputs:
workflow:
quality_checks:
knowledge_to_save:
review_status: 待审核
```

### 4. 生成训练记录

按 `records/templates/conversation-training-record.yaml` 输出结构化记录。

### 5. 生成知识库候选

知识库候选不能直接覆盖正式知识库，必须输出：

```yaml
knowledge_candidate:
  target_file:
  change_type: 新增 | 更新 | 合并
  proposed_content:
  source_evidence:
  source_type:
  review_status: 待审核
```

## 追问规则

如果对话信息不足，最多问 3 个问题。优先问：

1. 这段对话主要要训练哪个能力？
2. 这条经验是好案例、失败案例，还是通用规则？
3. 是否需要创建新 Skill，还是更新已有 Skill？

## 禁止事项

1. 不把 Agent 推断内容当成设计师明确结论。
2. 不直接写入正式知识库。
3. 不创建没有触发场景的新 Skill。
4. 不把一次偶然反馈沉淀成强规则。
5. 不暴露复杂结构给设计师确认，只给自然语言摘要。
