# 17 · The PM's New Leverage — Run Validation Without Engineers, Using Claude Code ⭐

> Season 1 · *AI PM Workflow Reconstruction* · Article 17 · Part 4: Delivery
> Target length: ~6000 Chinese chars / ~3500 English words (killer essay, one of the longest)

---

The 16th "dismissive blind spot" — **and the most important article in this book** —

**90% of PMs still "wait for engineers to validate requirements."**

It's not that PMs don't want to validate themselves. Most just **assume "code is engineers' work, PMs shouldn't touch it"** — so a requirement that could be validated in 3 hours **takes 2-4 weeks via "review → kickoff → schedule → build"** — and in those 2-4 weeks, others have validated 10 requirements with Claude Code.

After this article you'll see — **PM × Claude Code isn't about replacing engineers, it's about installing a validation lever for yourself**. But there's nuance — **half-knowing is more dangerous than not knowing**.

---

## Part 1: Workflow

### The Minimal Path for PM × Claude Code

**You don't need to write code — you need to validate end-to-end.**

The path:

```
Step 1: Install Claude Code (5 min)
  → npm install -g @anthropic-ai/claude-code
  → run `claude` in terminal
  → configure API key

Step 2: Open a new project directory (isolated environment)
  → mkdir prototype-xxx
  → cd prototype-xxx
  → DON'T play in production repo

Step 3: Write a markdown spec (10 min)
  → create prd.md
  → spell out: goal / inputs/outputs / API contract examples

Step 4: Let Claude Code run it (30 min - 3 hrs)
  → "Read prd.md. Build the smallest working prototype."
  → see it run → tweak prompt → run again

Step 5: Decide (10 min)
  → it runs → decide whether to kick off the project
  → it doesn't → kill the requirement
```

**Whole flow < 4 hours** — 1-2 months faster than traditional "review → kickoff → schedule → build."

### Applies to (5 scenarios)

PM × Claude Code is good for:
1. **Rapid capability validation**: can the model do this task
2. **Prompt debugging**: which prompt works best
3. **MVP prototypes**: for boss / customer demos
4. **Bad case reproduction**: run a production case locally
5. **Cross-system data pulls**: Linear / Slack / GitHub → weekly report

### Doesn't apply to (5 scenarios)

PM × Claude Code is NOT for:
1. **Production code**: your code can't ship, engineers must rewrite
2. **Performance-sensitive paths**: high concurrency / low latency / high QPS
3. **Complex frontend**: long-lived UI / complex state management
4. **Cross-system integration**: webhooks / callbacks / message queues going to production
5. **Critical business logic**: orders / billing / risk control

**One-sentence boundary**: **What you can throw away, PM writes; what you can't, engineers do.**

### The PM's 5-Step Claude Code Loop

```
Step 1: New project (isolated env)
   ↓
Step 2: Spell out the need (PRD/markdown)
   ↓
Step 3: See it run (actually execute)
   ↓
Step 4: Tweak the prompt, not the code (shift cost left)
   ↓
Step 5: Converge (declare demo-quality, decide next)
```

**Key counter-consensus**: **Tweak prompts, not code.**

PMs should never fall into "code-fixing" — that's engineers' job. PMs should tweak markdown / prompt — and let Claude Code run again.

**This is the core of PM leverage.**

---

## 7 Real Claude Code Prompts (Copy-Paste Ready)

### Scenario 1: Validate an AI requirement in 30 minutes

```
Read PRD.md in this folder. Build the smallest possible working
prototype that validates the core hypothesis: "User can upload a
WeChat chat history snippet, AI auto-summarizes the other party's
personality."
Use Anthropic's claude-sonnet API. UI: simplest HTML page.
No tests, no error handling, no deployment. After it runs, tell
me how to start it locally.
```

- **Expected output**: a runnable script + a local port
- **What it validates**: whether core AI capability can deliver the desired output quality
- **Pitfall**: don't let it build "complete version" — explicitly say "smallest possible"

### Scenario 2: Reproduce a production bad case

```
This is a user-reported bad case: [paste full input] → our AI
answered: [paste output]. User expected: [paste expectation].
Please: 1) find the prompt template path in my codebase that
handled this case 2) reproduce locally with the same input
3) rank 3 possible root causes.
Don't modify any code.
```

- **What it validates**: bad case is prompt issue, model issue, or data issue
- **Pitfall**: without "don't modify code," it'll start fixing and overwrite root cause

### Scenario 3: Debug a prompt

```
I have a prompt at ./prompts/summarizer.md.
Run 10 test cases (in ./test_cases.jsonl), tell me:
- which cases failed
- failure mode classification (hallucination/format/missing info/verbose)
- give 3 prompt rewrites ranked by expected improvement
```

- **What it validates**: prompt boundaries and failure modes
- **Pitfall**: give real test cases — don't let it make up samples (it picks easy ones)

### Scenario 4: MVP prototype for boss demo

```
Read prd.md. Build a pure-frontend clickable demo, all data mocked.
Requirements: 1) no backend needed
              2) looks like real product (use Tailwind)
              3) user walks through 3 core flow steps
              4) `npm run dev` to view
```

- **Note**: For this scenario, v0 / Lovable is more efficient than Claude Code unless you need Claude Code's codebase context

### Scenario 5: Test a RAG flow's feasibility

```
I want to validate: after chunk + embed of our 200 knowledge base
docs, can we correctly answer the 50 questions in
./eval_questions.txt?
Please: 1) run a minimal LangChain + Chroma pipeline
        2) output each question's retrieve top-3 chunks +
           generated answer + whether it hits ground truth
        3) give overall accuracy
Don't add reranker or hybrid search — show me the baseline.
```

- **What it validates**: RAG baseline accuracy, decide whether to kick off
- **Pitfall**: don't let it add reranker / fine-tune up front — you'll lose true baseline

### Scenario 6: Estimate engineering complexity for a new feature

```
Read the entire src/ directory. I want to add this feature:
[describe]. Please tell me: 1) which existing files are involved
2) what new files needed 3) where it conflicts with existing logic
4) how many days an experienced engineer needs.
No code — only assessment.
```

- **What it validates**: pre-conversation complexity prediction before talking to engineers
- **Pitfall**: it overestimates its own judgment — always sanity check with engineers

### Scenario 7: Cross-system data pull for weekly report

```
Via MCP, pull:
1) Linear tickets with status=done in past 7 days
2) Slack messages with high reactions in #checkout-project (same period)
3) Related PRs merged to main on GitHub
Synthesize a weekly report for the CEO, highlighting "user-visible
changes" and "blockers."
```

- **What it validates**: cross-system info integration — **this is Claude Code's real advantage over v0 / Lovable**

---

### The Next-Generation PM Tools After Claude Code

Lifting the view one layer — **Claude Code is the 2025-2026 H1 lever, not the terminal form**.

Starting H2 2026, the industry's PM tool stack is shifting in 4 directions:

**From Claude Code → Agent SDK**. Anthropic 2026-06 spun off Agent SDK / `claude -p` to independent monthly credit — meaning PM's unit of work upgrades from "I type a prompt" to "I dispatch a fleet of agents on a task." PM no longer sits at terminal waiting — **goes to a meeting, comes back to read the sub-agent fleet's outcome report**.

**From hand-written prompts → personal Skills library**. Skills are filesystem-based "domain expert packages" — customer interview synthesis / eval batch run / bad case classification, each a reusable skill package. Sachin Rekhi now teaches PMs to shift from "7 prompts" to "13+ skills" — **PM assets upgrade from "prompt notes" to "personal skill library"**.

**From single agent → sub-agent fleet**. One lead agent dispatches N specialist sub-agents in parallel (each with own model / prompt / tools), final Outcomes grader judges convergence — **PM designs aren't prompts, but fleet topology**.

**From chat UI → Generative UI**. Vercel AI SDK 3 + json-render + Google A2UI let LLMs generate React components directly — **product "UI" goes from designer deliverables to runtime LLM output**, PM's mockup thinking needs complete rewrite.

7 prompt templates you can use tonight — also watch these 4 shifts coming up. 6 months from now — **the PM who only types prompts but doesn't orchestrate skills + sub-agents will realize they're only using H1 2026 tooling**.

---

## Tool Comparison: 6 Vibe Coding Tools, PM's View

| Tool | PM Learning Curve | Best PM Scenario | Not For |
|------|-------------------|------------------|---------|
| **Claude Code** | Medium (terminal required) | Cross-file changes, reading codebases, reproducing bad cases, running agent/RAG, connecting Linear/Jira/Slack via MCP | Pure UI mockups |
| **Cursor** | Medium-high (IDE form) | PMs reading engineer-written logic in existing codebases | PMs who've never touched an IDE |
| **v0** | Low | UI mockups, design-to-code | Backend logic, agent flows |
| **Lovable** | Lowest (browser-based) | Non-technical PMs end-to-end deployable tools | Complex customization, performance-sensitive |
| **Bolt.new** | Lowest | Clickable demo in 30 min | Code requiring maintenance |
| **Replit Agent** | Medium | Full-stack small tools | Pure mockups |

**Anna Arteeva's summary is most cited**:
> "Lovable wins non-technical PMs, Bolt wins speed, v0 wins UI, Replit wins full-stack, Cursor / Claude Code wins engineering depth."

### How a PM Should Choose

| PM Scenario | Recommended Tool |
|-------------|------------------|
| First time playing | **v0 / Lovable** (no terminal needed) |
| Validating AI Agent / RAG flow | **Claude Code** (only one with direct API + SDK) |
| Demo to boss | **v0** |
| Validating deployable small tool | **Lovable / Replit** |
| Reproducing engineer's bad case | **Claude Code** (must read real codebase) |

---

## Part 2: Engineering Reality

### Real Industry Cases of PMs Using AI Coding

#### Dennis Yang (Chime PM) — Benchmark Case
- markdown PRD → open terminal `claude` → **clickable prototype in 20 minutes** → Slack screen-recording
- This is the earliest spread of "PRD as executable spec"

#### Lenny Rachitsky's Core View (2026-02 article)
> "Everyone should be using Claude Code more"

He publicly collected **50 non-technical user Claude Code cases**. Core view:
> "**Forget that it's called Claude Code — treat it as Claude Local / Claude Agent**."

#### Sachin Rekhi (ex-LinkedIn / Reforge instructor) — Most Systematic
- **1500 PMs at his webinar** showcased **13 self-built skills** (source: Sachin's public webinar recording + sachinrekhi.com course page)
- Covers: customer interview synthesis / NPS autonomy / no-SQL EDA / product strategy critique / release notes automation
- Same period produced **"AI Prototyping Mastery Ladder"** — **15 specific skills** graded into Apprentice / Journeyman / Master (source: sachinrekhi.com course page)

#### Boris Cherny (Head of Claude Code at Anthropic)
- On Lenny's podcast: **since 2025-11, 100% of his code is written by Claude Code**, he no longer types by hand
- Anthropic internal workflow: **prototype first, then dogfood — not write PRD first then develop**

#### Cat Wu (Head of Product, Claude Code at Anthropic)
- On Lenny show: Anthropic product team "why we're faster than anyone"
- **PM/Designer/Eng all use Claude Code to produce working prototypes for review** — not Figma + docs

### 4 Common Pitfalls

#### Pitfall 1: Getting addicted to coding, PM becoming less PM
**Case**: Industry KOLs repeatedly warn:
> "PM spending hours/days vibe-coding prototypes is hours/days NOT spent on user research, cross-team influence, strategic planning."

**Signal**: in a week, you open Claude Code more than user interview notes.
**Avoidance**: set a hard cap — max 2 hours per hypothesis validation; beyond that, stop and ask "**why am I writing this instead of having an engineer assess?**"

#### Pitfall 2: Treating demo as product (validation-grade ≠ production-grade)
**Critical warning**: Retool research: **vibe-coded apps connected to real DB face SQL injection as "data leaks waiting to happen."**

**Signal**: you start thinking "should we let real users try this."
**Avoidance**:
- Name it `prototype-xxx` from the start, not `feature-xxx`
- Explicitly: demo never connects to production DB / never stores real user data

#### Pitfall 3: Committing without reading the code
**Industry case**: a team's critical-path trap — agent stuffed achievement system logic into the game main loop, inflating hottest code 2x.

**Signal**: you can't explain "which files did it change" during review.
**Avoidance**:
- Always plan before execute
- Before committing, you must be able to explain each change in one sentence
- For critical path (login, payment, core loop) — always involve engineers

#### Pitfall 4: Using Claude Code to replace communication
**Industry quote**:
> "If a feature is important enough for you to rush-vibe-code it, it's important enough that the team should prioritize it."

**Core tension**: PM running it locally ≠ team can ship it.
**Avoidance**: first action after running it is screen-record + tag "validation only, not production", proactively pull engineer for 5-min review, ask not "can we ship this" but "**is my hypothesis right**."

### Validation-Grade vs Production-Grade Boundary

#### PM Can Do (Validation-Grade, 7 categories):
1. **AI capability probe**: call model API, try prompts, see output quality
2. **Local mock-data demo**: pure frontend + fake data
3. **Bad case reproduction script**: reproduce once, then discard
4. **Data exploration / EDA**: CSV → charts → insights
5. **Cross-system info synthesis**: Linear+Slack+GitHub → weekly report
6. **Small internal tool**: yourself, max team use, no production data
7. **Prompt evaluation harness**: run test set across multiple prompt versions

#### PM Should NOT Do (Production-Grade, 7 categories):
1. **Connecting to production database** (write access especially dangerous)
2. **Auth / authorization / payment** code
3. **Critical business logic** (orders, billing, risk control)
4. **Performance-sensitive modules** (high concurrency, low latency, high QPS)
5. **Cross-system integration to production** (webhooks, callbacks, queues)
6. **Complex frontend state management / long-lived UI**
7. **Any change affecting other engineers' codebase** (critical path / shared components)

### One-Sentence Boundary

> **What you can throw away, PM writes; what you can't, engineers do.**

---

## QE Lens: PM × Claude Code Leverage

**8 years of Quality Engineering perspective** —

Any engineering domain's evolution follows one rule: **push validation cost down from "high-barrier specialist role" to "business role"**.

- 30 years ago: testing needed hardware labs + specialized instruments
- 20 years ago: testing needed automation frameworks + QA engineers
- 10 years ago: testing needed CI/CD pipeline + engineers
- Now: **testing needs markdown PRD + Claude Code + PM themselves**

Claude Code isn't a new tool for PMs — **it's pushing "validation" from engineers down to PMs**.

This means PM's work fundamentally changes — **from "waiting for validation result" to "running validation themselves"**. Those who wait will be left behind at 10x speed. Those who run it become the new generation of PMs.

---

## Your Action Checklist

#### Action 1: Install Claude Code TODAY
- `npm install -g @anthropic-ai/claude-code`
- Configure API key
- Run a minimal validation with the 5-step loop

#### Action 2: Bookmark the 7 prompts
- 7 real scenario prompts already given
- Copy-paste-tweak for your scenario

#### Action 3: Run validation 3 hours before your next requirements review
- Run it through with Claude Code before review
- Drop the demo in the meeting for everyone
- Review efficiency: 5x

#### Action 4: Pin the 4 pitfalls at your desk
- Code addiction / demo-as-product / not-reading-code / replacing communication
- Ask yourself each time you open Claude Code

---

## Counter-Consensus Quotes

- **"PM's new leverage isn't writing code — it's compressing the cost of 'should we kick this off' from 2 weeks to 2 hours."**
- **"Lenny is right: forget it's called Claude Code — it's your Local Agent."**
- **"PRD doesn't die, but PRD's next reader is AI — a PRD that AI can run end-to-end is a good PRD."**
- **"AI turns PMs from 'schedule chasers' into 'hypothesis validators before scheduling' — that's leverage."**

---

## Closing Thoughts

This is the column's killer article.

After reading, you should take 3 actions:
1. Install Claude Code
2. Try the 7 prompts
3. Run validation before your next requirements review

The next article covers AI products' gradual rollout strategy — **fundamentally different from traditional feature gradual rollout**.

Prompt version, model version, parameter version multi-axis switching. How multi-axis rollout is designed, shadow traffic industry best practices, Notion's 70 engineers surviving via dual-track eval real case.

See you next article.

---

> **Companion Resources**: PM-specific Claude Code scaffold (with prompt templates, directory structure) + 5-step loop checklist (paid readers) ⭐ Premium
> **Next Up**: 18 · AI Product Gradual Rollout Strategy — After Traditional A/B Fails
> **Feedback / Reader Community**: WeChat Official Account 「蔡逸雯」

---

> **Reading the Chinese original?** See [17-pm-claude-code.md](./17-pm-claude-code.md)
> **Part of**: Season 1 · AI PM Workflow Reconstruction · 26 essays
> **Author**: Cai Yiwen (蔡逸雯) · 8 years in QE → AI PM
