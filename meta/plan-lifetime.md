---
title: 终身记忆系统落地方案
updated: 2026-11-25
confidence: high
status: active
scope: global
source: 本人陈述
---

# 终身记忆系统落地方案

> 本方案只装**不变量**（协议、原则、方法）。真实内容放私有库，两者不互相引用。

## 结论

**三层三副本：本地是唯一真相，私有云端只管同步，异地冷备专防账号风险。**
公开仓库只放不变量，不参与存证。

## 一、四层结构

| 层 | 载体 | 频率 | 加密 | 作用 |
|----|------|------|------|------|
| A 本地工作副本 | 纯 Markdown 目录 + 本地 git | 实时 | 无 | **唯一真相**，随时能带走 |
| B 私有云端 | GitHub private | 每天 push | 敏感目录 git-crypt | 同步 + 历史 + 多设备 |
| C 异地冷备 | restic → 移动硬盘 + 对象存储 | 每周 | restic 内置 | 防账号 / 平台风险 |
| D 公开名片 | 本仓库 | 手动 | 无 | 不变量，零事实 |

## 二、为什么必须三层

`A + B` 是「同步」，不是「备份」。两者都依赖同一个账号，失效模式高度相关：
账号被风控、误删仓库、平台改政策，任何一件发生，A 和 B 会同时失效。

**3-2-1 自查**：3 份副本、2 种介质、1 份异地。
只有 A + B 时是 2 份、1 种介质、0 份异地——不合格。

## 三、加密：路径级，不是全库

全库加密会毁掉可用性：手机读不了、Agent 读不了、diff 看不了。
全库明文则私有不等于安全：平台可见，账号被盗即全泄露。

正解是 **git-crypt 路径级加密**：本地操作完全透明，推上去是密文，没有 key 的人 clone 下来只见乱码。

```bash
choco install git-crypt
cd <私有库>
git-crypt init
printf '%s\n' \
  '10-life/finance/** filter=git-crypt diff=git-crypt' \
  '10-life/health/**  filter=git-crypt diff=git-crypt' \
  '20-career/clients/** filter=git-crypt diff=git-crypt' \
  >> .gitattributes
git-crypt export-key <离线路径>/lifeos.key
```

**key 的保管规则**：离线两处（U 盘 + 纸质恢复码），不进任何仓库、不进云盘。
丢失即永久不可恢复——远端只有密文，GitHub 无法帮你还原。

## 四、冷备：restic，不用裸 tar

```bash
winget install restic
restic init --repo <冷备路径>/restic-lifeos
restic backup <私有库> --exclude .git
restic forget --keep-daily 30 --keep-weekly 104 --keep-monthly 60
```

增量、去重、加密、可校验。保留策略：日备 30 天、周备 2 年、月备 5 年。

## 五、层级映射

| 目录 | 层级 |
|------|------|
| `00-system/` | L1 协议（AGENTS.md、PERMISSIONS、steward） |
| `10-life/` `20-career/` | L2 事实 + L3 项目 |
| `30-inbox/` | L4 流水入口 |
| `90-archive/` | 过期层，只读 |

## 六、自动化

| 周期 | 动作 | 失败后果 |
|------|------|----------|
| 每天 22:00 | `git add -A && git commit && git push` | 丢一天 |
| 每周日 02:00 | `restic backup` | 冷备停滞 |
| 每月 1 日 | 扫超期记忆，出待确认清单 | 记忆悄悄过期 |

Windows 用 `schtasks /create` 三条即可，无需额外软件。

## 七、硬指标：恢复演练

**没演练过的备份等于没有备份。** 每季一次：把 restic 快照恢复到临时目录，随机打开三个文件确认可读。
十分钟，但它是唯一能证明「真的存下来了」的动作。

## 八、落地顺序

| 何时 | 做什么 | 耗时 |
|------|--------|------|
| 第一晚 | git-crypt + 首次 restic 备份 | 30 min |
| 第一周 | 三个计划任务 + 一次真实恢复演练 | 1 h |
| 第一月 | `NOW.md`、`steward.md`、过期检查 | 2 h |

## 九、成本

GitHub 免费，对象存储 10 GB 内近乎免费，restic 免费。**
真正的成本是每年四次演练的 40 分钟**——省掉它，整套系统就只是心理安慰。

## 十、常见死法

| 死法 | 症状 | 预防 |
|------|------|------|
| 只增不减 | 文件上千，找不到东西 | 过期检查 + `90-archive/` |
| 只写不读 | 库很完整，但从没影响过决策 | 每会话强制加载 `NOW.md` |
| 只同步不备份 | 账号一没全没 | C 层冷备 |
| 加密丢 key | 文件在但永远打不开 | key 离线两处 |
| 第三周放弃 | 成本太高，懒得维护 | 一切自动化，人工只做周复盘 |
