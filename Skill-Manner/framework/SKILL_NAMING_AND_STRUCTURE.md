# Skill 命名与目录统一规范

## 1. Skill ID 命名

所有可执行 Skill 的目录名和 `SKILL.md` frontmatter 中的 `name` 必须完全一致，并且只允许：

```text
小写英文字母 + 数字 + 连字符
```

约束：

- 长度 3 至 63 个字符。
- 必须使用动词或明确任务名，优先采用 `动作-对象` 结构。
- 禁止中文、空格、下划线、括号、点号、斜杠和版本号。
- 禁止使用 `skill`、`new`、`test`、`final` 等无业务含义的单独名称。
- 同一 Skill ID 不得在不同目录重复出现。

推荐示例：`model-image-generation`、`reference-image-to-prompt`、`project-workflow-orchestrator`。

## 2. 标准目录结构

单个可执行 Skill 必须采用：

```text
{skill-id}/
├── SKILL.md              必须存在，包含唯一 frontmatter
├── README.txt            必须存在，说明目录用途和内容边界
├── agents/               可选，平台界面元数据
├── references/           可选，按需读取的知识资料
├── scripts/              可选，确定性执行脚本
├── assets/               可选，模板、样例和图片资源
└── examples/             可选，真实使用案例
```

`SKILL.md` 不得放在二级目录；一个 Skill 目录只能有一个 `SKILL.md`。`README.txt` 是本框架的目录说明文件，不替代 `SKILL.md`。

## 3. SKILL.md 必备格式

文件第一行必须是 `---`，frontmatter 只能包含 `name` 和 `description` 两个字段：

```yaml
---
name: example-task-skill
description: 说明 Skill 做什么、何时触发、处理什么输入和输出什么结果。
---
```

正文必须使用命令式或步骤式表达，建议控制在 500 行以内。详细知识应放到 `references/`，不要把大段案例和历史讨论全部塞进入口文件。

## 4. 风格 Skill 规范

风格 Skill 必须放在 `skills/style-generation/{skill-id}/`，仍然必须满足本规范，并在 `knowledge/style-registry.yaml` 登记。新接入状态固定为 `candidate`，审核后才能改为 `active`。

`skills/style-generation/` 本身是容器目录，不是可执行 Skill，不得单独写入注册表。

## 5. 同步与版本规范

主包 `outputs/workbuddy-image-skill` 和同步包 `outputs/kuangjia` 的 Skill 内容必须一致。每次新增或修改 Skill 后，必须同步：

1. Skill 目录。
2. 路由文件。
3. 注册表或索引。
4. 版本信息。
5. 对应目录的 `README.txt`。

## 6. 整理与审核规则

整理时先审计，再移动或改名。不得因改名删除原始内容；无法确认用途的目录进入 `needs-review`，不得自动并入 active Skill。审核记录至少写明原名称、标准名称、变更原因、来源、版本和审核状态。

## 7. Markdown 并入规则

所有并入的 `.md` 文档必须先按 `framework/MD_REWRITE_STANDARD.md` 重写。原始文档只能留档，重写稿必须包含文档类型、文档 ID、版本、来源、关联 Skill、执行规则、正向规则、负面规则、质量检查和待确认项。
