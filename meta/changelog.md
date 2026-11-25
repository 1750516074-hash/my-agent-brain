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

## v0.2 — 2026-11-25

**做了什么**

- `AGENTS.md`：新增 `status: unknown` 规则（禁止推断填充）、衰减规则（3 个月 / 12 个月两档）、读取顺序加入 `NOW`
- `meta/schema.md`：`status` 扩为四态（`active` / `draft` / `unknown` / `superseded`），明确 `unknown` 与 `draft` 的区别
- 新增 `NOW.example.md`：当前状态一页纸模板（真实内容留私有库）
- 新增 `meta/plan-lifetime.md`：三层三副本落地方案（本地 / 私有云 / 异地冷备）
- 新增 `meta/steward.md`：维护者与继任规则，**核心问题留 `unknown`**

**为什么**

- 上一版只写了「不要推测」，强度不够：模型越强越擅长合理推断，会把空槽填得头头是道
- 「终身」的真正风险不是现在写错，是五年后没人维护却仍被当作现状
- 记忆分层后，不同层的写入权限和衰减速度不同，需要显式规则

**影响哪些行为**

- Agent 遇到 `unknown` 必须停下提问，不能填
- 超过 12 个月未确认的 `active` 条目，使用前必须先问本人
- 每个会话开头增加一次 `NOW` 读取（30 天以上过期先问）
- `steward.md` 的四个问题未答前，任何 Agent 不得擅自修改 L0 / L2 内容

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
