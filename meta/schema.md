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
| `updated` | `YYYY-MM-DD` | **最后一次被本人确认的日期**。每次改都必须更新；只读不确认不算更新 |
| `confidence` | `high` / `medium` / `low` | 这条内容的可信程度 |
| `status` | `active` / `draft` / `unknown` / `superseded` | 是否已确认、是否未知、是否已作废 |
| `scope` | `global` / `project:<name>` | 适用范围 |
| `source` | `本人陈述` / `行为推断` / `项目沉淀` | 这条内容从哪来 |
| `supersedes` | 文件路径（可选） | 本文件取代了哪一份 |

## 确信度的判定

- **high** —— 本人明确说过，或至少三次独立体现
- **medium** —— 从一两次行为推断出来，方向清楚但样本不足
- **low** —— 纯推测，或只出现过一次。默认不要写 `low`；如果非要写，说明为什么值得记

## status 的四态

| 值 | 含义 | Agent 该怎么做 |
|----|------|----------------|
| `active` | 本人已确认 | 照做，但仍受衰减规则约束 |
| `draft` | 有内容，未经确认 | 当假设，交付时说明 |
| `unknown` | **明确不知道** | **禁止推断填充**，需要就问 |
| `superseded` | 已作废 | 只作历史参考 |

`unknown` 和 `draft` 的区别很关键：`draft` 是「我写了个初稿，你确认一下」，`unknown` 是「这里空着，因为我不知道，别替我填」。

## 正文写法

- 用二级标题划分主题，一个主题一个文件
- 条目用有序列表，编号**固定不复用**（`P1` 作废了就空着，不要重排）
- 每条：一句话结论 + 最多两句说明
- 不写「用户觉得」「我认为」这类主体，直接写事实

## 文件名

- 全小写，短横线分隔：`how-to-talk-to-me.md`
- 项目记忆放 `memory/projects/<项目名>/`，项目名与仓库名或简称一致
- 日期文件放 `memory/log/YYYY-MM-DD.md`
