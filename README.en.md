# step-processing

> In one line: **break a big task into small steps, and in any new session just say "start from next-session.md" — it auto-continues.**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](./LICENSE)
[![Claude Code Skill](https://img.shields.io/badge/Claude%20Code-Skill-blueviolet)](./SKILL.md)
[![GitHub stars](https://img.shields.io/github/stars/wangxi83/step-processing)](https://github.com/wangxi83/step-processing/stargazers)

🌐 **[中文](./README.md) | [English](./README.en.md)**

---

## 🎉 What does it actually do?

If you've worked with Claude / Codex on anything more than a quick question, you've probably hit this:

> "This task is too big to finish in one session. I want Claude to break it into steps and do it over multiple sessions… but every new session forgets where we left off, and I have to re-explain the whole background. 😩"

**`step-processing` is built to solve exactly that.**

It does two things — and only two things:

1. ✂️ **Split the task**: turn a big goal into N independent, individually-completable small steps.
2. 🤖 **Auto-handoff**: after each step, status, evidence, and blockers are written to `task-status.md`. **In the next new session, just say "start from next-session.md" and it picks up — no re-briefing required.**

That moment of *"Oh! So Claude can just run step-by-step, hands-off, in fresh sessions — that's awesome!"* 😎

---

## 🚀 30-second Quick Start

### First session: split the task

In Claude Code, just say:

> "Use the step-processing skill to break 'migrating the order system from MySQL to PostgreSQL' into steps."

Claude will ask you three things:

1. **Which directory?** (e.g. `plans/order-migration/`)
2. **Is the goal clear?** (if not, it'll keep clarifying)
3. **How many steps?** (it'll suggest, you confirm)

Then it generates these files:

```
plans/order-migration/
├── next-session.md       ← the new session reads this
├── task-status.md        ← the global state table
├── step-01-analyze-orders.md
├── step-02-design-schema.md
├── step-03-migrate-data.md
└── step-04-verify-and-cutover.md
```

### Every next session: just keep going

Close the current session. Open a **new session**. Say:

> "Start from `plans/order-migration/next-session.md`."

Done. Claude will automatically:

- ✅ Read `task-status.md` to see what's done and what isn't;
- ✅ Read `next-session.md` to find the current step;
- ✅ Execute the step, then update both files and point at the next;
- ✅ When everything is done, explicitly say *"All step-processing tasks are finished."*

**That's it.** 🎯

---

## 📦 How to install it into your project?

Just drop `SKILL.md` into your skills directory:

```bash
# Global — usable in any project
mkdir -p ~/.claude/skills/step-processing
cp SKILL.md ~/.claude/skills/step-processing/

# Project-local — only for the current project
mkdir -p .claude/skills/step-processing
cp SKILL.md .claude/skills/step-processing/
```

Next time you launch Claude Code, the skill is available.

---

## 📂 What's in this repo?

```
step-processing/
├── SKILL.md      ← ⭐ Core. This is what Claude actually reads.
├── README.md     ← Chinese
├── README.en.md  ← English (this file)
├── LICENSE       ← MIT, do whatever you want
├── CHANGELOG.md  ← What changed
└── .gitignore
```

That's it. **No more, no less.** Simple, right? 😉

---

## 🛡️ The iron rules

For the "auto-handoff" to actually work, a few hard rules:

| When | Must do |
| --- | --- |
| **A new session starts** | **Must** read `task-status.md` first to see the global progress. |
| **All steps are done** | **Must** tell the user "All step-processing tasks are finished" — **never** hallucinate more work. |
| **Before splitting a task** | **Must** ask the user which directory to use. Don't write files until confirmed. |
| **Step file naming** | `step-01-xxx.md`, `step-02-xxx.md` — fixed two-digit numbering. |
| **After completing a step** | **Must** update both `next-session.md` and `task-status.md`. |
| **When blocked** | Must record: what's blocked, what was tried, the next minimal action. |

Why so strict? Because without these, the next session can't pick up the thread. 😅

---

## 🤔 When to use it?

**Good fit:**

- ✅ Big refactors (DB migrations, framework upgrades, monolith → microservices)
- ✅ Multi-day projects (can't finish today, will continue tomorrow)
- ✅ Work where you want every step visible and individually reviewable
- ✅ Multi-person / cross-session collaboration

**Bad fit:**

- ❌ Small one-shot tasks (just ask directly)
- ❌ Exploratory work that needs tight real-time feedback (splitting gets in the way)

---

## 📄 License

[MIT](./LICENSE) — use it, modify it, redistribute it, just keep the attribution.
© 2026 wangxi83
