# 保守重构报告

## 原则

- 只新增目录和文件。
- 从原目录复制，不移动、不删除原始内容。
- 不覆盖任何已有目标。
- Skill 与案例采用并行结构，通过 `catalog.yaml` 关联。

## 新入口

- `skills/`：正式 Skill 副本。
- `cases/`：生图与审核案例副本。
- `knowledge/`：跨 Skill 共享知识。
- `workflows/`：框架、训练与项目流程。
- `archive/`：为第二阶段归档预留。
- `catalog.yaml`：Skill 与案例的关系索引。

## 有意暂缓的修复

- 未修改原始目录。
- 未删除 README、目录说明、输出图片或 ZIP。
- 未自动改写 Skill 正文。
- 未纳入 `style-skill-integration`，因为其 `SKILL.md` 与 `project-workflow-orchestrator` 重复，需要人工确认真实用途。
- 电商工具 Skill 的非标准 frontmatter 保留在新副本中，等待第二阶段规范化。

## 下一阶段建议

1. 逐个校验 `skills/` 下的 frontmatter。
2. 为案例补充统一的 `case.md` 元数据。
3. 将 Obsidian Canvas 改为读取并行入口。
4. 验证后再决定是否归档旧目录及 ZIP。