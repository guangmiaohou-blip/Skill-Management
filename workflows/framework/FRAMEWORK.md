# 通用图片处理 Skill 框架

## 目标

建立一套面向网页自动化 Agent 的通用图片处理 Skill 体系，用于公司内部图片生成、参考图逆向提示词、参考图再生成和知识库沉淀。

框架保持平台无关，不绑定具体图像生成网站或模型。Agent 在执行时根据任务、图片类型、平台能力和用户要求选择合适工具。

## 核心原则

1. 先识别图片类型，再选择 skill。
2. 先结构化分析，再生成提示词。
3. 每次执行都输出可复用记录。
4. 成功案例沉淀为模板，失败案例沉淀为避坑规则。
5. 提示词默认中文维护，可按平台需要转换为英文。
6. 参考图再生成必须先确认相似度，支持高相似、中相似、低相似三档。

## 第一阶段 Skill

| Skill | 用途 |
| --- | --- |
| model-image-generation | 生成模特图，支持服装模特、电商模特、真人写真、虚拟人、局部模特、穿戴展示、生活方式场景 |
| reference-image-to-prompt | 根据上传参考图逆向分析并生成结构化提示词 |
| reference-image-regeneration | 根据参考图重新生成相似图，支持三档相似度 |
| conversation-context-to-skill | 读取设计师与 Agent 的对话上下文，提炼训练规则、知识库候选，并创建或更新 Skill 草案 |
| style-skill-integration | 将已训练出来的小型风格生成 Skill 接入大框架，负责格式校验、注册表登记、路由更新和待审核管理 |
| project-workflow-orchestrator | 管理一次图片项目的输入、建目录、背景材料、执行、临时输出、成功案例选择、审核、知识库入库和共享发布 |

## 标准执行链路

1. 接收用户输入图片和需求。
2. `project-workflow-orchestrator` 创建项目目录和 `project-manifest.yaml`。
3. 判断图片类型和任务意图，挂载调研 MD、风格 Skill 和其他背景。
4. 选择对应 Skill，并读取必要的风格注册信息。
5. 按维度分析图片，生成提示词和推荐参数。
6. 将每轮图片写入项目的临时输出目录。
7. 设计师选择成功图片并打标签，Agent 自动绑定完整生成上下文。
8. 生成知识库候选和 Skill 更新候选，进入审核队列。
9. 审核通过后更新总 Skill、知识库和共享发布目录。

## 对话上下文训练链路

当训练材料来自设计师和 Agent 的对话时，按以下流程执行：

1. 读取当前上下文或用户提供的历史对话。
2. 提取设计师明确判断、Agent 推断规则和待确认信息。
3. 判断应更新已有 Skill，还是创建新的 Skill 草案。
4. 生成训练记录、提示词候选、负面提示词候选和标签。
5. 生成知识库候选，默认进入待审核。
6. 如果创建新 Skill，只输出草案，不直接视为正式 Skill。

## 风格 Skill 并入链路

当用户已经训练出多个小型风格生成 Skill，并希望并入大框架统一执行时，按以下流程执行：

1. 读取 `skills/style-skill-integration/SKILL.md`。
2. 检查小 Skill 的目录、`SKILL.md`、frontmatter 和必填章节。
3. 判断小 Skill 支持 `model-image-generation`、`reference-image-regeneration` 或其他任务。
4. 检查它是否覆盖大框架强制规则。
5. 将合格小 Skill 放入 `skills/style-generation/{skill_id}/`。
6. 写入 `knowledge/style-registry.yaml`，默认状态为 `candidate`。
7. 更新或引用 `framework/STYLE_ROUTING.md` 作为后续调用依据。
8. 输出并入报告、冲突项、缺失字段和下一步审核动作。

## 目录说明

所有 Skill 的统一命名、目录和 `SKILL.md` 格式以 `framework/SKILL_NAMING_AND_STRUCTURE.md` 为结构规范。新增或并入 Skill 前必须先完成该规范的审计。

| 目录 | 说明 |
| --- | --- |
| framework | 总体规范、路由规则、命名和版本规范 |
| skills | 每个可复用 skill 的执行说明，包括核心图片 Skill、风格并入 Skill 和已接入的风格子 Skill |
| workflows | 面向 Agent 的端到端自动化流程 |
| knowledge | 知识库、标签体系、提示词维度、失败案例和风格 Skill 注册表 |
| records | 每次执行后的结构化记录模板 |
| schemas | 可选的数据结构约束 |

## Agent 使用要求

Agent 必须读取本文件和 `framework/ROUTING.md` 后再执行自动化图片任务。执行具体任务时，只读取相关 skill、workflow 和必要知识库文件。
