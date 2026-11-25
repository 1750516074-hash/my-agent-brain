---
title: 变更记录
updated: 2026-11-25
confidence: high
status: active
scope: global
source: 项目沉淀
---

# meta/changelog.md — 变更记录

每次合并 PR 追加一条。格式：日期 · 改了什么 · 为什么 · 影响哪些行为。

## v0.1 — 2026-11-25

**做了什么**

- 建立仓库骨架：`AGENTS.md` 读写协议、`meta/schema.md` 格式规范、`do-not/never.md` 硬约束
- 建 `identity/`、`working-style/`、`memory/`、`meta/` 四个区
- `identity/` 与 `working-style/` 下的个人内容**留空槽**，标 `status: draft`

**为什么**

- 先让协议和结构跑通，任何 Agent 读进来都不会用错格式、不会乱写
- 个人偏好不做推测填充：空槽会让 Agent 来问，错误的推测会让它一直错下去

**影响**

- Agent 现在可以安全地读和改这个库
- 但 `draft` 文件的内容不可当作本人偏好使用
- `how-to-talk-to-me.md` 里有一份「缺省约定」临时生效，属通用默认，非本人确认
