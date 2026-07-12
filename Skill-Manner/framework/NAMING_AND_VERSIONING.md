# 命名与版本规范

## 文件命名

使用小写英文、数字和连字符。

示例：

```text
model-image-generation
reference-image-to-prompt
image-analysis-record.yaml
```

## 记录版本

每条可复用记录必须包含：

```yaml
version: v0.1
date: YYYY-MM-DD
operator: 操作人
```

## Skill 版本

Skill 使用语义化版本：

```yaml
skill_version: 0.1.0
```

版本含义：

| 版本 | 含义 |
| --- | --- |
| 0.1.x | 初始框架、字段和流程仍可能调整 |
| 0.x.0 | 新增能力或知识库结构 |
| x.0.0 | 与旧版本不兼容的大调整 |

## 案例编号

推荐格式：

```text
YYYYMMDD-图片类型-任务类型-三位序号
```

示例：

```text
20260706-model-regeneration-001
```
