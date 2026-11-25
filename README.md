# my-agent-brain

> 我的外置大脑。给所有 AI Agent 的公开记忆库。

每次新开一个会话，模型都要从零猜我的偏好：猜错了返工，猜对了也只是运气。
这个仓库把「我是谁、我怎么判断好坏、我做事的路数」写成版本化文件，任何 Agent 读一遍就能直接进入状态，不用重新试探。

## Agent 从这里开始

严格按顺序读，不要跳：

| # | 文件 | 你会拿到什么 |
|---|------|--------------|
| 1 | [`AGENTS.md`](AGENTS.md) | 读写协议。**必读**，不读就不要动这个仓库 |
| 2 | [`do-not/never.md`](do-not/never.md) | 硬约束，读完立刻生效，优先级高于一切偏好 |
| 3 | [`identity/who-i-am.md`](identity/who-i-am.md) | 我是谁、在做什么、在什么环境里 |
| 4 | [`identity/how-to-talk-to-me.md`](identity/how-to-talk-to-me.md) | 语言、长度、格式、语气 |
| 5 | [`working-style/`](working-style/) | 判断标准、做事流程、交付自检 |
| 6 | [`memory/MEMORY.md`](memory/MEMORY.md) | 跨项目的历史结论 |
| 7 | `memory/projects/<项目>/` | 只在任务涉及该项目时读 |

只读前两个文件就开始干活，大概率会因为格式或判断标准返工。

## 仓库结构

```
my-agent-brain/
├── AGENTS.md                    读写协议（核心）
├── identity/                    我是谁
│   ├── who-i-am.md
│   └── how-to-talk-to-me.md
├── working-style/               我怎么判断、怎么推进
│   ├── principles.md            决策原则，编号固定
│   ├── workflow.md              接到任务怎么推
│   └── delivery-checklist.md    交付前自检
├── do-not/
│   └── never.md                 硬约束
├── memory/
│   ├── MEMORY.md                长期记忆（人工策展）
│   ├── log/                     按日记录
│   └── projects/                项目级记忆
└── meta/
    ├── schema.md                文件格式规范
    ├── changelog.md             变更记录
    └── open-questions.md        待本人回答的问题
```

## 状态字段

每个文件头部有 `status`：

- **`active`** —— 已确认，可以照着做
- **`draft`** —— 结构就位，内容待本人确认。**按它行动前必须先问**
- **`superseded`** —— 已被取代，只作历史参考

当前 `AGENTS.md`、`meta/schema.md`、`do-not/never.md` 是 `active`；
`identity/` 和 `working-style/` 下多数是 `draft`，空槽待填。

## 怎么让它变准

[`meta/open-questions.md`](meta/open-questions.md) 里是我还没回答的问题。
回答一次，这份记忆就准一分——比 Agent 自己推测一百次都管用。

## 边界

这是公开仓库，里面的内容可能被任何人读到、索引、缓存，撤回也无法真正删除。

**永远不写**：密码、密钥、令牌、身份证件、住址、真实客户全名、未公开的商业数据。
这条写在 [`AGENTS.md`](AGENTS.md) 里，是硬约束，不因任务紧急而放宽。
