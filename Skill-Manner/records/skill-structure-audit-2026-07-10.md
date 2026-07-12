# Skill 结构审计记录

日期：2026-07-10

## 审计范围

`outputs/workbuddy-image-skill/skills` 下的所有可执行 Skill 及风格 Skill。

## 已修正

- 为 `conversation-context-to-skill`、`model-image-generation`、`reference-image-regeneration`、`reference-image-to-prompt` 补齐标准 YAML frontmatter。
- 确认 `project-workflow-orchestrator`、`style-skill-integration` 和 `unny-korean-minimal-beauty` 已符合 `name` 与目录名一致的要求。
- 确认 `style-generation` 是风格 Skill 容器，不作为可执行 Skill 登记。
- 新增统一规范：`framework/SKILL_NAMING_AND_STRUCTURE.md`。

## 当前标准 Skill

```text
conversation-context-to-skill
model-image-generation
project-workflow-orchestrator
reference-image-regeneration
reference-image-to-prompt
style-skill-integration
```

## 当前风格 Skill

```text
unny-korean-minimal-beauty
```

状态：`candidate`，需要审核后才能改为 `active`。
