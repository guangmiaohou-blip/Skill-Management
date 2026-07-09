# 给负责人的使用说明

## 目标

把设计师的审美判断和图片经验，转化成 Agent 能稳定复用的 skill 知识库。

默认采用被动训练模式：设计师不读框架，不写结构化文档，只通过上传图片、选择、打分和确认来训练。

## 角色分工

| 角色 | 负责内容 |
| --- | --- |
| 设计师 | 选图、判断好坏、填写训练表、标注失败原因 |
| Skill 负责人 | 整理训练表、合并同类规则、更新 skill 和 knowledge |
| Agent | 读取 skill、执行分析、生成提示词、沉淀记录 |

被动模式下的分工：

| 角色 | 负责内容 |
| --- | --- |
| 设计师 | 上传图、选择选项、口头补充、确认总结 |
| Agent | 访谈、归纳、生成记录、生成知识库候选 |
| Skill 负责人 | 审核候选内容，决定是否合并 |

## 推荐训练节奏

第一周只做三件事：

1. 每个核心 skill 通过 Agent 访谈收集 5 个好案例。
2. 每个核心 skill 通过 Agent 访谈收集 3 个失败案例。
3. 每个核心 skill 由负责人审核沉淀 1 份稳定提示词模板。

如果设计师没有 skill 训练经验，第一周不要让设计师填写模板。请由 Agent 按 `passive-mode/AGENT_INTERVIEW_SCRIPT.md` 访谈收集。

## 验收标准

一条被动训练记录合格，需要满足：

1. 有明确适用 skill。
2. 有图片类型和任务类型。
3. 有好图标准。
4. 有必须保留、可以变化、必须避免。
5. 有正向提示词和负面提示词。
6. 有可复用标签。

## 如何合并进框架

| Agent 生成内容 | 合并位置 |
| --- | --- |
| 好案例候选 | knowledge/prompt-patterns 或 records/templates/reusable-case.md |
| 失败案例候选 | knowledge/failure-cases.md |
| 标签 | knowledge/taxonomy/reusable-tags.yaml |
| 提示词模板 | knowledge/prompt-patterns |
| 执行检查项 | 对应 skill 的 SKILL.md 或 designer-training/quality-checklists |
