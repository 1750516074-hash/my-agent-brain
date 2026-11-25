# memory/projects/ — 项目级记忆

一个项目一个目录，目录名用仓库名或公认简称。只在任务涉及该项目时才读——不要一开始就全读一遍，那会把无关上下文塞进判断里。

## 单个项目的目录

```
memory/projects/<项目名>/
├── context.md      这个项目是什么、现在到哪一步、谁在用
├── decisions.md    做过的技术 / 产品决策，以及放弃的备选
└── gotchas.md      踩过的坑，写清楚「下次别再这样」
```

## context.md 模板

```markdown
---
title: <项目名> 上下文
updated: 2026-11-25
confidence: high
status: active
scope: project:<项目名>
source: 项目沉淀
---

# <项目名>

## 是什么

一句话。

## 当前状态

做到哪一步，下一步要做什么。

## 技术栈 / 约束

只写从代码里看不出来的：为什么用这个，不用那个。

## 关键人物

（角色，不写真实姓名——见 do-not/never.md N1）
```

## decisions.md 写法

一条一个决策，必须包含**放弃的备选**。只写「用了 A」没有价值，价值在「为什么不用 B」。

## gotchas.md 写法

一条一个坑，写三段：现象 / 原因 / 下次怎么做。只写现象等于没写。
