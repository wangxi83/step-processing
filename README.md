# step-processing

> 一句话：**把大事拆成小步，每完成一步，新 session 只要说一句"按 next-session.md 开始工作"，就自动接着干！**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](./LICENSE)
[![Claude Code Skill](https://img.shields.io/badge/Claude%20Code-Skill-blueviolet)](./SKILL.md)
[![GitHub stars](https://img.shields.io/github/stars/wangxi83/step-processing)](https://github.com/wangxi83/step-processing/stargazers)

---

## 🎉 它到底能干嘛？

你心里应该冒出过这个念头：

> "这事儿太大了，我想让 Claude 帮我拆成几步慢慢做……可是我每次开新 session，它就忘了上次干到哪了，又要重新解释一遍背景！😩"

**`step-processing` 就是来解决这个痛点的。**

它做两件事，而且就只做这两件事：

1. ✂️ **拆任务**：把一个大目标，拆成 N 个彼此独立、能各自干完的小步骤。
2. 🤖 **自动续命**：每干完一步，状态、证据、阻塞全都记到 `task-status.md` 里。**下一个新 session 只要说一句"按 next-session.md 开始工作"，它就自己接着干，完全不用你再解释一遍！**

是不是突然感觉：**"哦！原来 Claude 也能这样无脑自动执行啊，太爽了吧！"** 😎

---

## 🚀 30 秒上手

### 第一次：拆任务

在 Claude Code 里这么说就行：

> "帮我用 step-processing 技能，把'把订单系统从 MySQL 迁到 PostgreSQL'这件事拆成几步。"

Claude 会问你三件事：

1. **放在哪个目录？**（比如 `plans/order-migration/`）
2. **目标清不清楚？**（不清楚就继续问清楚）
3. **拆成几步？**（它会建议，你拍板）

然后它就生成这些文件：

```
plans/order-migration/
├── next-session.md       ← 下次新 session 读这个
├── task-status.md        ← 全局状态表，看一眼就知道干到哪了
├── step-01-分析现有订单.md
├── step-02-设计新表结构.md
├── step-03-数据迁移.md
└── step-04-验证与切换.md
```

### 后续 session：接着干

关掉当前对话，开个**新 session**，进来就说一句：

> "按 `plans/order-migration/next-session.md` 开始工作。"

完事。Claude 会自动：

- ✅ 读 `task-status.md`，知道哪些已做完、哪些没做；
- ✅ 读 `next-session.md`，知道自己现在该干哪一步；
- ✅ 干完一步，自动更新两个文件，把指针指向下一步；
- ✅ 全干完了，明确告诉你"分步骤任务已全部结束"。

**就这么简单。** 🎯

---

## 📦 怎么装到我的项目里？

把这个仓库的 `SKILL.md` 文件扔到你自己的 skills 目录就行：

```bash
# 全局生效（所有项目都能用）
mkdir -p ~/.claude/skills/step-processing
cp SKILL.md ~/.claude/skills/step-processing/

# 只对当前项目生效
mkdir -p .claude/skills/step-processing
cp SKILL.md .claude/skills/step-processing/
```

然后下次开 Claude Code，它就能用上这个技能了。

---

## 📂 仓库里都有啥？

```
step-processing/
├── SKILL.md      ← ⭐ 核心，Claude 实际读的就是它
├── README.md     ← 你正在看的
├── LICENSE       ← MIT，随便用
├── CHANGELOG.md  ← 改了什么
└── .gitignore
```

就这几个文件，**没了**。简单吧？😉

---

## 🛡️ 它的"铁律"

为了让"自动续命"真的能跑起来，定了几个死规矩：

| 什么时候 | 必须做什么 |
| --- | --- |
| **新 session 一进来** | **必须**先读 `task-status.md`，看看全局进度 |
| **所有步骤都做完了** | **必须**直接告诉你"分步骤任务已全部结束"，**绝不**瞎猜还有活儿 |
| **拆任务之前** | **必须**先问你目录放哪，你不说它就不动手 |
| **步骤文件命名** | `step-01-xxx.md`、`step-02-xxx.md` 这样，固定两位数编号 |
| **每完成一步** | **必须**同步更新 `next-session.md` + `task-status.md` |
| **遇到卡住** | 必须写清楚"卡在哪、试过啥、下次第一步该干嘛" |

为什么这么死板？因为不这样，下次新 session 就接不上茬了 😅

---

## 🤔 什么时候该用它？

**适合**：

- ✅ 大重构（数据库迁移、框架升级、单体拆微服务）
- ✅ 一次要做多天的项目（今天做不完，明天接着干）
- ✅ 你希望每一步都看得到、能单独验收的工作
- ✅ 多人协作 / 跨 session 接力

**不适合**：

- ❌ 一次能搞定的小活儿（直接问就完了）
- ❌ 需要实时反馈的探索性工作（拆了反而碍事）

---

## 📄 许可证

[MIT](./LICENSE) — 爱用用、爱改改、爱转转，标注原作者就行。
© 2026 wangxi83
