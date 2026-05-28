# 第一性原理工作流 / First Principles Workflow

> AI 编程助手通用协作技能：强制 **想清楚再动手**、**只做该做的**、**验到位才说完成**。
>
> A universal AI coding assistant skill that enforces: **think before you build**, **build only what's needed**, **prove it works before you call it done**.

---

## 这个技能解决了什么问题？ / What Problems Does This Solve?

| 痛点 Problem | 具体表现 What Happens |
|---|---|
| **上来就写代码** | 还没搞懂你要什么，就开始写了。你要的是一个按钮，它给你重写了整个页面 |
| **Jump to solutions** | Writes code before understanding your actual need |
| **复制粘贴思维** | 到处套同样的方案，不管适不适合。上个项目的登录系统直接搬来，但这个项目根本不需要登录 |
| **Copy-paste thinking** | Same patterns everywhere without questioning if they fit |
| **过度设计** | "以防万一"做一堆你根本用不上的功能。一个个人项目，它帮你搭了微服务架构 |
| **Over-engineering** | Builds features "just in case" that you'll never use |
| **假装完成** | 代码写完就说"好了"，根本没测过。你一跑就报错 |
| **Fake completion** | Says "done" without testing — you run it and it crashes |
| **理解偏差** | 误解你的需求，浪费几小时走错方向 |
| **Requirement drift** | Misunderstands intent, wastes hours going the wrong way |

---

## 适用于什么工作内容？ / What Kind of Work?

| 场景 | 不用的后果 | 用之后的效果 |
|---|---|---|
| 创建新功能 | 做一堆你不想要的东西 | 先问清需求，再做最小实现 |
| 修复 Bug | 贴补丁，治标不治本 | 找到根因，从源头解决 |
| 重构代码 | 改 A 坏了 B | 先确认边界，改完逐项验证 |
| 新建项目 | 复制旧项目配置，端口冲突、密钥泄露 | 从零配置，只加该项目必需的 |
| UI/设计改动 | 改完布局错乱，多问题一起改全搞砸 | 一个一个来，每个先出预览图 |
| 准备上线/发布 | 没做合规检查，可能违规 | 12 维度法律评估先过一遍 |

---

## 适用于哪些人？ / Who Is This For?

- **非程序员**——用 AI 编程工具但受够了拿到的代码跑不起来
- **独立开发者**——不想让 AI 过度设计，只想快速交付
- **团队协作者**——希望 AI 助手的输出稳定、可预期
- **所有人**——只要说过类似"这不是我要的""你怎么没测就交"之类的话

---

## 怎么用？ / How to Use

### Claude Code

```bash
git clone https://github.com/liq22191-cyber/first-principles-workflow.git \
  ~/.claude/skills/first-principles-workflow
```

### 其他 AI 编程工具（Cursor / Windsurf / Copilot 等）

将 `SKILL.md`（英文）或 `SKILL_CN.md`（中文）的内容复制到你的项目规则文件（如 `.cursorrules`、`.windsurfrules`、`CLAUDE.md`），或直接设为全局规则。

**中文用户**把 `SKILL_CN.md` 重命名为 `SKILL.md` 覆盖原文件即可切换。

每项任务必须经过五道硬性门禁，没有例外。
Every task goes through five hard gates. No exceptions.

```
搞清需求 → 第一性原理 → MVP → 自测 → 汇报
Clarify Intent → First Principles → MVP → Self-Test → Report
   (ask first)    (think deep)   (build lean)  (verify hard)  (deliver clean)
```

### Stage 1: Clarify Intent
Ask questions **one at a time**. Present 2-3 approaches with trade-offs. Get explicit approval before writing a single line of code. Even "simple" tasks go through this — unexamined assumptions cause the most waste.

### Stage 2: First Principles Thinking
Strip to fundamentals. Question every requirement. Is it truly necessary, or just inertia? Rebuild from scratch.

| Without This Skill | With This Skill |
|---|---|
| "Add login" → searches "how to add login" | Asks: does this project even need accounts? |
| Error → copy-pastes a patch from StackOverflow | Finds and fixes the root cause |
| New project → copies old project config | Asks: what does THIS project actually need? |

### Stage 3: MVP — Build Only What's Needed
No unused functions. No future-proofing. Delete dead code on sight. Get the core flow working first.

### Stage 4: Self-Test — 8 Dimensions × 3 Rounds
Visual, interaction, function, code, runtime, network, backend config, cross-platform. **Minimum 3 rounds** across every applicable dimension. One failure = restart from round 1.

### Stage 5: Report
Say what changed, what didn't, and why. List tools used and known limitations.

## Plus 9 Supplementary Rules

| Rule | One-Liner |
|---|---|
| Cross-Project Isolation | Never copy `.env`, assign fresh ports |
| Save Progress Proactively | Don't wait for "save this" |
| UI Preview First | 3-5 preview images before any visual change |
| Legal Compliance | 12-dimension check before start AND before launch |
| Explain Technical Terms | Plain-language explanations for every term |
| Skill Discovery | Check for relevant skills, even at 1% chance |
| UI Inspection | Screenshots + vision model, never code-reading |
| Idea Capture | Structure new ideas immediately |
| Work Log | Auto-generate logs at session end |

## Installation

```bash
# Clone into your Claude Code skills directory
git clone https://github.com/liq22191-cyber/first-principles-workflow.git \
  ~/.claude/skills/first-principles-workflow
```

Or copy the `first-principles-workflow/` folder directly into `~/.claude/skills/`.

The skill triggers when you ask your AI assistant to create, build, fix, refactor, or design anything.

## What's Inside

```
first-principles-workflow/
├── SKILL.md              # English skill (main file)
├── SKILL_CN.md           # 中文版（重命名为 SKILL.md 即可用）
├── references/
│   └── compliance-checklist.md  # 12-dimension legal compliance checklist
├── README.md             # This file (bilingual)
└── README_CN.md          # 中文版说明
```

## Why "First Principles" / 为什么叫"第一性原理"？

Because most problems come from **not questioning assumptions**. "Add authentication" is not a requirement — "users need to access their own data" is. This skill forces the AI to find the real requirement behind every request, then build the simplest thing that satisfies it.

因为大多数问题都源于**没有质疑假设**。"加个登录"不是需求——"用户需要访问自己的数据"才是。这个技能强制 AI 助手找到每个请求背后的真正需求，然后只做最简单有效的实现。

---

**License:** MIT
