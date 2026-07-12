---
name: image-skill-training-framework
description: 通用图片处理与设计师被动训练 Skill。用于网页自动化 Agent 或通用 Agent 执行图片分析、参考图逆向提示词、参考图再生成、模特图生成、发型展示、饰品与配饰展示，以及通过被动访谈或读取设计师与 Agent 的对话上下文来收集判断、提炼训练数据、创建或更新 Skill，并沉淀为可复用知识库。触发场景包括：用户上传图片后需要分析图片、根据参考图生成提示词、根据参考图重新生成相似图、训练模特图生成能力、训练发型或饰品展示能力、收集好案例或失败案例、整理设计师和 Agent 的历史对话、把对话内容转化为新 Skill 草案、让设计师以选择和确认的方式训练 Skill。
---

# Image Skill Training Framework

## 使用目标

使用本 Skill 执行图片处理和设计师被动训练任务。设计师不需要阅读框架、不需要填写复杂文档、不需要写提示词。Agent 负责主动提问、整理答案、生成提示词、生成训练记录和待审核知识库候选。

## 入口文件

先读取：

1. `README_TEST.md`
2. `framework/FRAMEWORK.md`
3. `framework/ROUTING.md`
4. `framework/STYLE_ROUTING.md`

如果是设计师被动训练，继续读取：

1. `designer-training/passive-mode/PASSIVE_TRAINING_PROTOCOL.md`
2. `designer-training/passive-mode/AGENT_INTERVIEW_SCRIPT.md`
3. `designer-training/passive-mode/AGENT_OUTPUT_CONTRACT.md`
4. `designer-training/passive-mode/REVIEW_QUEUE.md`

根据任务读取对应 Skill：

1. `skills/reference-image-to-prompt/SKILL.md`
2. `skills/reference-image-regeneration/SKILL.md`
3. `skills/model-image-generation/SKILL.md`
4. `skills/conversation-context-to-skill/SKILL.md`
5. `skills/style-skill-integration/SKILL.md`

所有 Skill 在执行、并入或发布前，必须先符合 `framework/SKILL_NAMING_AND_STRUCTURE.md` 的命名、目录、frontmatter、README 和同步规范。
所有并入的 `.md` 文档必须先按照 `framework/MD_REWRITE_STANDARD.md` 重新编写，原始文档只能留档，不能直接进入 Skill 或知识库。

如果是完整图片项目，必须先按 `skills/project-workflow-orchestrator/SKILL.md` 创建项目目录和主清单，再进入具体图片 Skill。

## 完整项目自动化入口

收到设计师任务后，Agent 自动执行：识别任务 -> 创建标准项目目录 -> 挂载调研 MD、风格 Skill 和其他背景 -> 路由并执行 -> 保存临时图片 -> 接收成功图片选择和标签 -> 生成知识库候选 -> 管理审核 -> 更新总 Skill -> 生成共享发布包。

设计师只需要提交任务、选择背景材料、选择成功图片、补充标签并确认审核；项目目录、记录、分类和发布清单由 Agent 自动维护。

## Skill 统一规范

目录名必须与 `SKILL.md` 中的 `name` 完全一致，并且只能使用小写英文字母、数字和连字符。风格 Skill 只能放入 `skills/style-generation/{skill_id}/`，新增状态必须为 `candidate`。

## 默认行为

当用户上传图片但没有说明用途时：

1. 先判断图片类型。
2. 使用最多 3 个选择题询问用户意图。
3. 默认进入参考图逆向提示词流程。
4. 输出图片分析、正向提示词、负面提示词、推荐参数和可复用标签。
5. 询问是否继续执行参考图再生成或模特图生成。

## 设计师被动训练要求

Agent 必须：

1. 每轮最多问 3 个问题。
2. 优先使用选择题。
3. 不要求设计师阅读文档。
4. 不要求设计师写 YAML、JSON 或完整提示词。
5. 把设计师的口语判断转成结构化记录。
6. 输出待审核知识库候选，不直接污染正式知识库。

## 对话上下文训练要求

当用户要求根据设计师与 Agent 的对话来训练或创建 Skill 时，Agent 必须：

1. 先整理对话中的任务目标、图片类型、好坏判断、保留项、避坑项和最终结论。
2. 区分设计师明确表达、Agent 推断和待确认内容。
3. 把对话内容转成训练记录、提示词模板、负面提示词、可复用标签和 Skill 规则候选。
4. 如果对话中出现新的稳定任务类型，则创建新的 Skill 草案。
5. 新 Skill 草案必须进入待审核状态，不能直接视为正式 Skill。
6. 如果对话信息不足，最多提出 3 个补充问题。

## 风格 Skill 并入要求

当用户要求把已经训练出来的小风格 Skill 并入大框架，或让大框架可以执行某个新风格时，Agent 必须读取 `skills/style-skill-integration/SKILL.md`。

Agent 必须：

1. 校验小 Skill 是否包含独立 `SKILL.md`。
2. 检查小 Skill 的 frontmatter、必填章节、触发词、适用场景和负面提示词。
3. 将小 Skill 放入 `skills/style-generation/{skill_id}/`。
4. 写入或更新 `knowledge/style-registry.yaml`。
5. 使用 `framework/STYLE_ROUTING.md` 判断后续调用方式。
6. 新接入的小 Skill 默认进入 `candidate` 状态，不能自动视为正式启用。
7. 不允许小 Skill 覆盖大框架强制规则，包括相似度询问、样貌相似优先、参考图文字图形去除、参考图产品默认去除。

## 输出要求

每次训练结束后输出：

1. 给设计师看的自然语言总结。
2. 给负责人的训练摘要。
3. 一条 records 格式训练记录。
4. 一条 knowledge candidate。
5. 审核状态，默认 `待审核`。
