---
title: 文件格式规范
updated: 2026-11-25
confidence: high
status: active
scope: global
source: 本人陈述
---

# meta/schema.md — 文件格式规范

所有记忆文件共用一套 frontmatter，保证任何 Agent 写入的格式一致、可解析、可排序。

## frontmatter 字段

```yaml
---
title: 文件标题
updated: 2026-11-25
confidence: high
status: active
scope: global
source: 本人陈述
---
```

| 字段 | 取值 | 含义 |
|------|------|------|
| `title` | 字符串 | 文件标题，与 H1 一致 |
| `updated` | `YYYY-MM-DD` | 最后修改日期。**每次改都必须更新** |
| `confidence` | `high` / `medium` / `low` | 这条内容的可信程度 |
| `status` | `active` / `draft` / `superseded` | 是否已确认、是否已作废 |
| `scope` | `global` / `project:<name>` | 适用范围 |
| `source` | `本人陈述` / `行为推断` / `项目沉淀` | 这条内容从哪来 |
| `supersedes` | 文件路径（可选） | 本文件取代了哪一份 |

## 确信度的判定

- **high** —— 本人明确说过，或至少三次独立体现
- **medium** —— 从一两次行为推断出来，方向清楚但样本不足
- **low** —— 纯推测，或只出现过一次。默认不要写 `low`；如果非要写，说明为什么值得记

## 正文写法

- 用二级标题划分主题，一个主题一个文件
- 条目用有序列表，编号**固定不复用**（`P1` 作废了就空着，不要重排）
- 每条：一句话结论 + 最多两句说明
- 不写「用户觉得」「我认为」这类主体，直接写事实

## 文件名

- 全小写，短横线分隔：`how-to-talk-to-me.md`
- 项目记忆放 `memory/projects/<项目名>/`，项目名与仓库名或简称一致
- 日期文件放 `memory/log/YYYY-MM-DD.md`
