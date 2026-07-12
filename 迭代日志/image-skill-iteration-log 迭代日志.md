# Image Skill Training Framework 迭代日志

## 基本信息

```yaml
project: image-skill-training-framework
date: 2026-07-06
current_version:
  framework_package: v1.6-md-rewrite-standard
  workbuddy_package: v1.6-md-rewrite-standard
status: 可继续测试
```

## 项目目标

本项目用于构建一套面向网页自动化 Agent 和通用 Agent 的图片处理 Skill 框架。

核心目标：

1. 支持参考图逆向提示词。
2. 支持参考图再生成。
3. 支持模特图生成。
4. 支持设计师被动训练。
5. 支持读取设计师与 Agent 的对话上下文并创建或更新 Skill。
6. 支持将使用后的 Markdown 文档整理成待审核知识库候选。
7. 支持通过测试结果持续纠偏并沉淀规则。

## 当前目录与交付包

当前主要目录：

```text
outputs/kuangjia
outputs/workbuddy-image-skill
```

当前保留的主要压缩包：

```text
kuangjia-framework-v1.0-face-proportion-modes.zip
workbuddy-image-skill-v0.7-face-proportion-modes.zip
```

WorkBuddy 导入包要求 zip 根目录必须包含：

```text
SKILL.md
```

该要求已满足并验证。

## 主要版本演进

### v0.1：基础图片 Skill 框架

建立了第一版通用图片处理框架，包含：

1. framework 总规范。
2. skills 三个核心能力。
3. workflows 自动执行流程。
4. knowledge 知识库。
5. records 记录模板。
6. schemas 结构约束。

第一批核心 Skill：

```text
model-image-generation
reference-image-to-prompt
reference-image-regeneration
```

### v0.2：设计师训练包

新增设计师训练材料，但初版仍然需要设计师阅读文档和填写模板。

后来判断该形式学习成本仍然偏高，因此被后续版本替代。

### v0.3-v0.4：设计师被动训练

将设计师角色从“主动学习 Skill 并填写文档”调整为“被动判断和确认”。

设计师只需要：

```text
上传图片
选择好案例或失败案例
选择哪里好或哪里失败
确认 Agent 总结
```

Agent 负责：

```text
主动访谈
整理判断
生成提示词
生成训练记录
生成知识库候选
提交负责人审核
```

新增核心文件：

```text
designer-training/passive-mode/PASSIVE_TRAINING_PROTOCOL.md
designer-training/passive-mode/AGENT_INTERVIEW_SCRIPT.md
designer-training/passive-mode/AGENT_OUTPUT_CONTRACT.md
designer-training/passive-mode/REVIEW_QUEUE.md
```

### v0.5：外部工具测试包

新增外部代码工具测试入口：

```text
README_TEST.md
TEST_PROMPTS.md
PACKAGE_INFO.md
```

用于把框架放到其他 Agent 或代码工具中测试。

### WorkBuddy 兼容版本

WorkBuddy 导入时报错：

```text
SKILL.md not found in zip archive
```

原因：WorkBuddy 要求 zip 根目录直接包含 `SKILL.md`。

修正：

1. 创建 `outputs/workbuddy-image-skill`。
2. 在根目录增加 `SKILL.md`。
3. 打包时压缩目录内容，而不是外层文件夹。
4. 验证 zip 根目录存在 `SKILL.md`。

### v0.6：对话上下文训练

新增能力：

```text
conversation-context-to-skill
```

用途：

1. 读取设计师与 Agent 的历史对话或当前上下文。
2. 提炼设计师明确判断。
3. 区分 Agent 推断和待确认信息。
4. 生成训练记录。
5. 生成知识库候选。
6. 在出现稳定新任务类型时创建待审核 Skill 草案。

新增文件：

```text
skills/conversation-context-to-skill/SKILL.md
workflows/conversation-context-training.md
records/templates/conversation-training-record.yaml
designer-training/conversation-context/
```

### v0.7：发型与饰品能力

用户提出模特生成 Skill 需要加入：

```text
饰品
发型
```

更新内容：

1. model-image-generation 增加发型展示。
2. 增加饰品展示。
3. 增加发色、刘海、卷度、发丝质感。
4. 增加耳饰、项链、戒指、手链、发饰、眼镜、手表等配饰控制。
5. 增加饰品材质、位置、比例、遮挡检查。
6. 更新提示词模板、标签体系、记录模板和质量检查表。

### v0.8：相似度必须询问

原规则中参考图再生成默认使用：

```text
中相似
```

用户要求取消默认值。

修正后规则：

```text
如果用户明确说高相似 / 中相似 / 低相似，可以直接使用。
如果用户没有说明，相似度必须先询问。
不能默认填中相似。
未确认时记录为：待确认。
```

已更新：

```text
framework/ROUTING.md
skills/reference-image-regeneration/SKILL.md
workflows/reference-image-regeneration.md
records/templates/*
knowledge/parameter-recipes.md
designer-training/passive-mode/AGENT_INTERVIEW_SCRIPT.md
```

### v0.9：模特美感、年轻感、真实感纠偏

测试 ELLE 风格大片后发现问题：

1. 亚洲人感过重。
2. 模特美感不足。
3. 年轻感不足。
4. 人物真实感不足。

错误归因：

```text
70% 来自提示词审美方向错误
20% 来自平台输出质感或水印限制
10% 来自 Skill 缺少美感和真实感审核
```

主要问题词：

```text
East Asian woman
phoenix eyes
sharp jawline
striking
intense gaze
flawless
porcelain skin
8K
ultra realistic
single hard key light
no fill light
```

修正规则：

1. 不在用户未要求时默认锁定亚洲女性或特定族裔。
2. 区分冷艳成熟感与年轻真实模特感。
3. 减少 flawless、porcelain skin、8K 等容易产生 AI 味的词。
4. 增加真实相机摄影、自然皮肤纹理、轻微面部不对称。
5. 增加模特美感、年龄感、真实感质检。

新增正向方向：

```text
young fashion model
balanced facial proportions
fresh youthful presence
natural confident expression
modern international editorial beauty
real camera photograph
natural skin texture
visible pores
subtle facial asymmetry
realistic fabric texture
```

新增负面方向：

```text
AI generated look
plastic skin
waxy skin
over-smoothed skin
uncanny face
overly sharp facial features
mature severe look
```

### v1.0：脸部比例模式

第二次测试发现眼睛占脸部比例问题。

最初判断为：

```text
眼睛过大
中庭偏短
幼态大眼
美颜滤镜脸
```

随后用户提供目标参考图，确认这类比例在某些场景中不是错误，而是目标效果。

因此新增两个脸部比例模式：

#### 真实商业模特比例

适合：

```text
电商
服装
真实摄影
成熟时尚模特
产品展示
```

要求：

```text
真实成年人面部比例
自然眼睛大小
正常眼距
协调三庭五眼
真实眼部结构
中庭不过短
脸部不过度幼态
```

#### 偶像近景美妆比例

适合：

```text
近景脸部特写
偶像感
清透美妆
发夹
美甲
手部靠近脸部
水润唇妆
清透眼妆
```

允许并强化：

```text
眼睛占比略大但自然
短中庭
清透圆润眼型
饱满卧蚕
柔和小脸轮廓
轻微无辜感
K-pop idol beauty close-up
glossy beauty editorial
```

仍需避免：

```text
眼睛畸形
眼距过近
瞳孔过大
眼白过多
五官错位
过度漫画化
假人感
```

### v1.1：样貌相似优先与参考图清理

用户提出：参考图再生成中的相似度不应主要体现在模特动作上，而应主要体现在样貌上。

修正规则：

```text
人物图相似度优先体现在样貌、脸部比例、五官关系、气质、发型妆容和整体美感方向上。
动作、手势、姿势、构图和机位只在用户明确要求时保留。
参考图中的文字、logo、图形符号、水印、UI、排版文字和无关标识默认全部去除。
```

### v1.2：参考图产品默认去除但保留人物动作

用户进一步提出：参考图中的产品默认不保留，但需要保留人物原本动作关系。

修正规则：

```text
参考图中的产品默认全部去除。
如果人物正在手持、佩戴、展示或靠近产品，应保留人物动作、手部位置、身体姿态、视线方向和互动关系，但移除产品本体。
产品相关的品牌、logo、文字、屏幕内容、包装图形和商业标识也默认全部去除。
只有用户明确要求保留产品时，才把产品加入保留项。
```

新增测试：

```text
测试 10：参考图产品去除但保留人物动作
```

新增输出目录管理：

```text
outputs/LOW：保存最近三个旧版本
outputs/NEW：始终保存当前最新版
```

## 当前关键原则

### 1. 不直接污染正式知识库

所有训练结果、对话总结和使用后的 Markdown 文档，都应先进入候选层。

推荐流程：

```text
原始 md 文档
→ Agent 读取整理
→ 生成 knowledge candidate
→ 负责人审核
→ 合并到正式知识库
```

### 2. 区分来源类型

知识候选必须标记来源：

```yaml
source_type:
  - designer_explicit
  - agent_inferred
  - result_observed
  - user_confirmed
  - needs_confirmation
```

### 3. 不把一次测试结果变成强规则

测试结果需要沉淀为：

```text
待审核候选
适用场景
触发条件
避免事项
```

而不是直接变成全局默认。

### 4. 模特审美必须先判断模式

生成模特图前必须判断：

```text
真实商业模特比例
偶像近景美妆比例
成熟冷艳大片
年轻国际化时尚模特
亚洲感明确
不锁定族裔
```

不能把一种比例强行套到所有场景。

## 当前已知问题与后续建议

### 已知问题

1. 部分平台会强制添加水印，Skill 无法完全通过提示词解决。
2. 不同平台对 `真实感`、`美感`、`年轻感` 的解释差异较大。
3. 仅靠文字提示词仍然可能无法稳定控制脸部比例。
4. 后续可能需要加入参考图权重、面部比例模板或局部重绘策略。

### 后续建议

1. 新增 `md-to-knowledge-candidate` Skill，用于将使用后的 `.md` 文档整理成待审核知识库候选。
2. 增加“平台差异记录”，记录不同图像模型对同一提示词的表现。
3. 建立“脸部比例样本库”，把真实商业模特比例与偶像近景美妆比例分开存放。
4. 建立“失败图 → 纠偏提示词 → 再测试结果”的闭环记录。
5. 对发型、饰品、眼睛比例、手部、美甲等高风险区域建立单独检查项。

## 当前上下文压缩摘要

当前项目已经从基础图片 Skill 框架演进为一个可在 WorkBuddy 中导入的图片处理与训练 Skill 包。它支持参考图逆向、参考图再生成、模特图生成、设计师被动训练、对话上下文训练、发型饰品控制、相似度询问、模特真实感纠偏和脸部比例模式选择。

历史记录中的旧版本为：

```text
kuangjia-framework-v1.2-remove-reference-products-keep-action.zip
workbuddy-image-skill-v0.9-remove-reference-products-keep-action.zip
```

如果后续继续工作，优先从以下文件读取：

```text
outputs/kuangjia/PACKAGE_INFO.md
outputs/kuangjia/skills/model-image-generation/SKILL.md
outputs/kuangjia/knowledge/prompt-patterns/model-image-template.md
outputs/kuangjia/knowledge/failure-cases.md
outputs/kuangjia/TEST_PROMPTS.md
outputs/workbuddy-image-skill/SKILL.md
```

历史阶段后续重点：

```text
新增 md-to-knowledge-candidate
完善知识库候选审核流程
继续测试脸部比例模式
把真实测试结果沉淀为待审核候选
```

## v1.3：风格 Skill 并入管理

新增 `style-skill-integration`，用于将设计师训练出的风格 Skill 接入总框架。

主要变化：

1. 新增 `skills/style-generation/{skill_id}/` 风格 Skill 容器。
2. 新增 `knowledge/style-registry.yaml` 风格注册表。
3. 风格 Skill 接入后默认状态为 `candidate`。
4. 只有负责人明确审核后，才允许改为 `active`。
5. 小 Skill 不得覆盖相似度询问、样貌相似优先、参考图文字图形去除和产品默认去除等全局规则。
6. 已完成 `unny-korean-minimal-beauty` 测试并入。

## v1.4：项目全生命周期自动化

新增 `project-workflow-orchestrator`，把一次图片任务统一管理为完整项目。

标准流程：

```text
任务提交
→ 自动识别
→ 创建 project_id 和项目目录
→ 挂载调研 MD、风格 Skill 和背景材料
→ 执行生成并保存临时图片
→ 设计师选择成功图片并打标签
→ 自动生成案例与知识库候选
→ 审核
→ 更新总 Skill
→ 共享发布
```

标准项目目录：

```text
00_input
01_background
02_analysis
03_prompts
04_temp_outputs
05_selected
06_records
07_knowledge_candidate
08_review
09_shared_release
```

设计师只负责提交任务、选择材料、选择成功图片、确认标签和审核结果，其余步骤由 Agent 自动维护。

## v1.5：Skill 命名与目录统一规范

新增 `framework/SKILL_NAMING_AND_STRUCTURE.md`，统一所有 Skill 的结构。

强制规则：

1. Skill 目录名与 `SKILL.md` 的 `name` 必须完全一致。
2. 只允许小写英文、数字和连字符。
3. 每个可执行 Skill 必须包含 `SKILL.md` 和 `README.txt`。
4. `SKILL.md` 必须包含标准 YAML frontmatter。
5. `style-generation` 只作为容器，不能作为独立执行 Skill。
6. 主包和 `kuangjia` 同步包必须保持一致。
7. 已补齐核心 Skill 的 frontmatter，并将 `_template` 规范为 `style-skill-template`。

## v1.6：并入 Markdown 统一重写

新增 `framework/MD_REWRITE_STANDARD.md`，规定所有并入的 `.md` 文档必须重新编写。

新的处理方式：

```text
原始 MD
→ 来源留档
→ 按统一字段重写
→ candidate
→ 审核
→ 进入 Skill / 知识库 / 共享发布
```

重写稿必须包含：

```text
文档类型
文档 ID
版本
状态
来源
重写日期
重写人
关联 Skill
目的
适用范围
执行规则
正向规则
负面规则
参数与示例
质量检查
限制与待确认项
变更记录
```

本轮已将 UNNY 测试来源记录按新规范重写，并同步到主包和 `kuangjia` 包。原始文档只能作为来源材料保留，不能直接覆盖正式 Skill 或知识库。

## 当前版本摘要

```yaml
version: v1.6-md-rewrite-standard
status: 可继续测试，新增内容默认 candidate
main_package: outputs/workbuddy-image-skill
sync_package: outputs/kuangjia
core_skills:
  - conversation-context-to-skill
  - model-image-generation
  - project-workflow-orchestrator
  - reference-image-regeneration
  - reference-image-to-prompt
  - style-skill-integration
style_skills:
  - unny-korean-minimal-beauty
required_md_rule: all-imported-markdown-must-be-rewritten
required_similarity_rule: ask-before-reference-regeneration
required_reference_cleanup: remove-text-graphics-and-products-by-default
```

## 下一步

1. 将 v1.6 重新打包为 WorkBuddy 可导入包，并验证 zip 根目录包含 `SKILL.md`。
2. 为更多已训练风格 Skill 执行“原始 MD 留档 + 规范重写 + candidate 审核”流程。
3. 完善知识库候选审核和共享发布后的版本回滚机制。
4. 继续测试模特脸部比例、眼睛占比、真实感、发型和饰品稳定性。
