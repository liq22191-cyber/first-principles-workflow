---
name: first-principles-workflow
description: This skill should be used when the user asks to "create a feature", "build a component", "fix a bug", "refactor", "design a solution", "add functionality", "modify behavior", "start a new project", or begins any creative or implementation task. Use when the user mentions "first principles", "think from scratch", "rethink this", "question assumptions", or expresses frustration with copy-paste solutions that don't work, wasted time on misunderstood requirements, untested code being reported as "done", or projects that keep accumulating unnecessary complexity. NOT for simple informational queries, reading files, or questions about existing code without changes.
---

# First Principles Workflow

A disciplined collaboration workflow for Claude Code, Codex, and other AI coding assistants. Ensures every task is done right the first time: clarify intent, think from first principles, build only what's needed, self-test thoroughly, then report.

## The Chain

```
Clarify Intent → First Principles → MVP → Self-Test → Report
    (brainstorming)    (think deep)   (build lean)  (verify)   (deliver)
```

Each stage is a hard gate — do not skip.

---

## Stage 1: Clarify Intent

Before writing any code or proposing any solution, understand what the user actually needs.

**Hard gate:** Do NOT invoke any implementation skill, write any code, or scaffold any project until the user has approved a design.

- Ask questions one at a time — never bombard
- Understand: purpose, constraints, success criteria, expected outcome
- Propose 2-3 approaches with trade-offs and a recommendation
- Present the design and get user approval before proceeding
- Even "simple" tasks go through this — a short design is fine, no design is not

**Anti-pattern:** "This is too simple to need a design." Every task, no matter how small, benefits from clarified intent. The simplest tasks are where unexamined assumptions cause the most wasted work.

---

## Stage 2: First Principles Thinking

Before implementing the approved design, strip it down to fundamentals.

**Process:**
1. **Deconstruct**: What are the irreducible facts? Remove all assumptions, "industry standards", and "that's how it's usually done"
2. **Question**: Is each requirement truly necessary, or just inertia?
3. **Rebuild**: Derive the simplest effective solution from first principles

**Examples:**

| Without First Principles | With First Principles |
|---|---|
| User says "add login" → immediately search "how to add login" | Ask: does this project actually need user accounts? If not, skip it |
| Error appears → search error message and paste a patch | Understand the root cause, fix at the source |
| New project → copy old project's config and dependencies | Ask: what does THIS project actually need? Add only that |
| User says "add a settings page" → start designing settings UI | Ask: what settings would actually be changed? Maybe it's just one config value |

---

## Stage 3: MVP — Build Only What's Needed

Code as little as possible. Solve today's problem, not tomorrow's hypothetical one.

**Four rules:**
1. **Minimum code**: No unused functions, no uncalled dependencies, no dead code
2. **No future-proofing**: Solve the current problem only — don't build for "we might need this later"
3. **Delete > Add**: When you spot dead code, duplicates, or useless files, delete them immediately
4. **Make it work first**: Get the core flow running before adding polish

**Relationship with First Principles:** First principles tells you WHAT is truly needed; MVP ensures you build ONLY that.

---

## Stage 4: Self-Test Before Reporting

Never claim something is "done" until you have verified it yourself. **Minimum 3 rounds** of testing across ALL applicable dimensions before reporting.

**Test dimensions:**

| # | Dimension | Check |
|---|-----------|-------|
| 1 | **Visual** | Screenshots + visual analysis — layout, colors, spacing, fonts, dark theme, no overflow/truncation/blank areas |
| 2 | **Interaction** | Click, input, scroll, modal, toggle — all responsive, no lag or broken behavior |
| 3 | **Function** | Core flow works end-to-end (e.g., search → play → skip → chat reply) |
| 4 | **Code** | No syntax errors, no dead references, no unused imports, changes match the intended scope |
| 5 | **Runtime** | Server returns HTTP 200, browser console has zero JS errors, APIs return correct data |
| 6 | **Network** | HTTP status codes correct, API responses normal, WebSocket connections stable |
| 7 | **Backend Config** | If applicable: reverse proxy (Nginx/Caddy), process manager (PM2), SSL certs, environment variables — no errors |
| 8 | **Cross-Platform** | If the app runs on multiple platforms (web + desktop, or web + mobile) — compare both, differences must be intentional and documented |

**Hard rules:**
- **3 rounds minimum** across every applicable dimension before reporting
- If any test fails in any round, fix it and restart testing from round 1
- Never report "done" after just writing the code without running it
- Never submit an unfixed issue repeatedly — if stuck after 3 attempts, explain why to the user and ask for guidance
- For UI changes: screenshot + vision model analysis is mandatory, NOT optional
- Changed but untested = not done. Tested once = not done. Skipping a dimension = not done.

---

## Stage 5: Report What Was Done

After all tests pass, report clearly:

- What was changed and why
- What was NOT changed and why
- Any known limitations
- Tools and methods used

---

## Supplementary Rules

### Cross-Project Isolation

When creating a new project:
- Create `.env` (environment config) from scratch — NEVER copy from another project
- Assign a fresh port number; verify the old project's port still works after starting the new one
- Include only the config variables this project actually needs

### Save Progress Proactively

- Save conversation progress and key decisions to persistent memory after milestones
- Don't wait for the user to say "save this"
- Update project status files immediately after significant changes

### UI Changes: Preview First

- Before any visual/design change, generate 3-5 preview images
- User selects the preferred version → then write code
- Process one issue at a time, never batch multiple UI problems

### Legal Compliance Awareness

For any project, before starting AND before launching:
- Check content compliance (no illegal material)
- Check IP (licenses for all code, fonts, images, data)
- Check privacy (is user data collected? Is consent needed?)
- Check qualifications (does this project type require special licenses?)
- For the full 12-dimension checklist, see `references/compliance-checklist.md`
- **Red flag = stop and consult a real lawyer**

### Explain Technical Terms

When mentioning any technical term or abbreviation for the first time, add a plain-language explanation in parentheses. If a non-programmer wouldn't understand it, explain it.

### Discover Available Skills

At the start of every exchange, check whether any relevant skills or workflows apply to the task. Even a 1% chance a skill might help means invoking it.

### UI Inspection: Screenshots, Not Code-Reading

When checking or debugging frontend UI/layout, **never** diagnose issues by reading code line by line. Use screenshots + vision model analysis:

1. Open the page in a browser, take a full-page screenshot
2. Scroll to different positions, take 2-3 more screenshots covering all content
3. Analyze each screenshot with a vision model: check alignment, spacing, overflow, whitespace, truncation, blank areas
4. Compile findings into a complete issue list before touching any code

**Why:** Reading code shows what SHOULD render. Screenshots show what ACTUALLY renders. These are often different.

### Idea Capture: Structure Before You Forget

When the user expresses a new project idea or product concept, capture it immediately with structured analysis rather than letting it get lost in the conversation:

1. Save it to a persistent knowledge base (notes app, wiki, project folder)
2. Document at minimum: product overview, target users, core features, technical approach, monetization model, risks
3. Update an index file so the idea remains discoverable later

**Why:** Good ideas emerge mid-conversation and are easily forgotten. Structured capture turns fleeting thoughts into actionable projects.

### Work Log: Auto-Generate at Session End

When the user signals the work session is ending ("done for today", "wrap up", "save progress"), automatically generate a work log:

1. Review all changes made during the session (files edited, commands run, decisions made)
2. Create a dated log entry covering: completed items, confirmed items, unresolved issues, next steps
3. Update project-level logs cumulatively (new entries appended, not overwriting old ones)
4. Tell the user the log has been saved

**Why:** Manual logging is easily forgotten. Auto-generated logs ensure every session has a record for future reference.

---

## Quick Reference

| Stage | One-line rule |
|---|---|
| Clarify Intent | Ask questions, present design, get approval |
| First Principles | Strip to fundamentals, question every assumption |
| MVP | Build only what's needed today |
| Self-Test | 3 rounds, 8 dimensions, verify everything before saying "done" |
| Report | Say what changed, what didn't, and why |

| Supplementary Rule | One-line rule |
|---|---|
| Cross-Project Isolation | Never copy .env, assign fresh ports |
| Save Progress | Don't wait for "save this" — do it automatically |
| UI Preview | 3-5 preview images first, one issue at a time |
| Legal Compliance | 12-dimension check before start and before launch |
| Explain Terms | Tech terms get plain-language explanations |
| Discover Skills | Check for relevant skills, even at 1% chance |
| UI Inspection | Screenshots + vision model, not code-reading |
| Idea Capture | Structure new ideas immediately, don't lose them |
| Work Log | Auto-generate logs at session end |
