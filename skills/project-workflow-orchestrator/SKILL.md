---
name: project-workflow-orchestrator
description: 自动管理图片生成项目的完整生命周期。用于接收设计师任务，识别任务类型，创建标准项目文件，挂载调研 Markdown、风格 Skill 和其他背景材料，执行图片任务，管理临时图片，接收成功案例标签，生成结构化归档包，提交审核并在审核通过后更新总 Skill 与共享版本。
---

# 图片项目全流程总控 Skill

本 Skill 是项目级总控层，不替代具体的图片生成 Skill。它负责让 Agent 按统一状态机推动一个项目从输入到共享发布完成。

## 核心原则

1. 设计师只做四类动作：提交任务、选择或上传背景材料、标记成功图片、确认审核结果。
2. Agent 自动完成识别、建项目目录、选择 Skill、整理材料、生成记录、分类、提交审核和发布同步。
3. 每个项目必须有唯一 `project_id` 和 `project-manifest.yaml`。
4. 所有临时图片与正式案例分离。未被标记为成功的图片只能留在临时目录，不能进入知识库。
5. 成功案例必须与使用过的 Skill、调研 MD、提示词、参数、标签和审核记录绑定。
6. 审核通过前只能写入候选知识库，不能覆盖 active Skill。
7. 参考图中的文字、Logo、图形和产品默认去除；如人物与产品有互动，保留人物动作、手部位置、身体姿态和互动关系。
8. 参考图再生成的相似度必须询问，且相似度优先作用于样貌、脸部比例、五官关系、气质、发型和妆容，不默认作用于动作。

## 自动执行顺序

### 1. 接收任务

读取设计师上传的任务说明、图片、文件和对话上下文，创建 `project_id`。任务说明不完整时，先建立项目并把缺失项写入 `intake.yaml`，只询问必要问题。

### 2. 识别与初始化

自动识别图片类型、任务意图、是否需要参考图、是否涉及模特图或产品图、是否需要风格 Skill，并选择总框架中的核心 Skill。然后创建标准项目目录：

```text
{project_id}/
├── 00_input/                 原始任务、原图、设计师上传材料
├── 01_background/            调研 MD、风格 Skill、历史案例、品牌规范
├── 02_analysis/              图片识别、任务分类、相似度与保留/去除清单
├── 03_prompts/               正向提示词、负面提示词、版本提示词
├── 04_temp_outputs/          执行过程中产生的全部图片
├── 05_selected/              设计师标记成功的图片及标签
├── 06_records/               执行记录、参数、失败原因和迭代日志
├── 07_knowledge_candidate/   待审核案例、知识库候选和 Skill 更新候选
├── 08_review/                审核意见、修改记录和审核状态
└── 09_shared_release/        审核通过后可共享的发布包
```

每个新建目录必须放置简短 `README.txt`，说明该目录用途、允许放入的内容和禁止放入的内容。

可直接复制 `workflows/project-template/` 作为项目初始目录，再写入 `project-manifest.yaml`。

### 3. 挂载背景材料

设计师可以一次上传或选择调研 `.md`、风格 Skill、参考图、历史案例、品牌规范和平台参数。Agent 自动复制或建立来源引用，生成 `01_background/background-manifest.yaml`，并为每份材料标记：

```yaml
material_id: bg-0001
type: research-md | style-skill | reference-image | historical-case | brand-rule | platform-note
source: 原始路径或上传标识
used: true | false
reason: 本材料对当前任务的用途
```

材料只作为当前项目上下文使用，不能因为被上传就自动成为正式知识。任何准备并入 Skill、知识库或共享发布包的 `.md` 文档，都必须先按 `framework/MD_REWRITE_STANDARD.md` 完成统一重写；原始文档保留为来源，重写稿进入候选审核。

### 4. 执行任务

根据 `02_analysis/task-classification.yaml` 路由到具体 Skill。若匹配到 `active` 风格 Skill，则叠加其风格规则；`candidate` 风格 Skill 只能在设计师明确同意试用时使用。执行时所有生成图写入 `04_temp_outputs/`，每轮都生成 `generation-record-{n}.yaml`。

每轮记录至少包括：模型、平台、推荐参数、正向提示词、负面提示词、输入参考图、风格 Skill、相似度选择、保留项、去除项和输出文件。

### 5. 成功案例选择

Agent 自动展示临时输出的编号和简短差异说明。设计师只需勾选成功图片并添加或确认标签。Agent 将被选图片复制到 `05_selected/`，生成 `selection.yaml`，并自动关联对应的生成记录，不允许只保存图片而丢失上下文。

### 6. 自动整理候选

对每张成功图片生成：

- 图片类型和自动分类结果
- 可复用正向提示词
- 负面提示词
- 使用的平台和模型
- 推荐参数
- 风格与视觉标签
- 操作人、日期、项目版本
- 成功原因和适用边界
- 失败尝试与避坑规则

最终写入 `07_knowledge_candidate/knowledge-candidate.yaml` 和 `07_knowledge_candidate/case.md`。如对话中出现稳定的新方法，额外生成 Skill 更新候选，不直接覆盖正式 Skill。

### 7. 审核与发布

审核状态只能按以下顺序流转：

```text
intake -> running -> awaiting-selection -> candidate-review -> approved -> shared
                                      \-> rejected -> revision -> candidate-review
```

审核人检查真实性、稳定性、版权/品牌风险、提示词可复用性、材料来源和全局规则冲突。只有 `approved` 才能进入 `09_shared_release/`，并更新总知识库、风格注册表或 Skill 版本。发布后写入 `release-manifest.yaml`，记录版本、变更摘要和回滚来源。

## 必须询问的内容

只有这些信息缺失时才向设计师提问：任务目标、输出数量或尺寸、相似度档位、是否保留动作、是否保留参考图中的产品/文字/图形、可使用的平台/模型、成功图片选择和审核确认。问题一次最多 3 个。

## 失败处理

任何阶段失败都不得丢失项目文件。将错误写入 `06_records/errors.yaml`，状态改为 `blocked` 或 `revision`，保留已生成的中间材料，并给设计师一个可执行的下一步选择。

## 相关文件

- `workflows/PROJECT_LIFECYCLE.md`：完整生命周期和状态转移
- `schemas/project-manifest.yaml`：项目主清单
- `schemas/selection.yaml`：成功案例选择记录
- `schemas/knowledge-submission.yaml`：知识库候选提交记录
- `framework/ROUTING.md`：任务到具体 Skill 的路由
- `framework/STYLE_ROUTING.md`：风格 Skill 的调用和审核规则
