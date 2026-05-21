# 25 · AI Native Teams — 3 Real-World Organizational Patterns

> Season 1 · *AI PM Workflow Reconstruction* · Article 25 · Part 7: Organization
> Target length: ~5000 Chinese chars / ~2500 English words

---

The 24th "dismissive blind spot" —

**90% of bosses want to use AI to "replace employees".**

It's not that bosses are greedy. Most just **assume "AI Native = AI replaces humans = layoffs save money"** — then they follow Klarna's path: hiring freeze + natural attrition, then publicly admit in 2025 that "AI lacks empathy" and re-hire — **and the valuation takes a hit**.

After this article you'll see — **AI Native isn't "AI replaces humans," it's "Human × AI = 5-10x productivity" as a new organizational form**. There are 3 mainstream industry patterns, each fits different scenarios.

**This article is the core of the B2B funnel** — your company's boss will reach out to you after reading.

---

## Part 1: Workflow

### 3 Mainstream AI Native Organizational Patterns

#### Pattern 1: Anthropic / OpenAI "Research-Heavy" Structure

**Traits**:
- ~35% of company is Research staff
- ~65% is Engineering + Product
- Almost no traditional BD / Sales / Ops roles (extremely high per-capita ARR)

**Anthropic public signals (2025)**:
- Company size growing fast (thousands of people, official numbers vary)
- CEO Dario mentioned in public interviews that Research team is >1/3
- The rest is Engineering + Product + GTM
- Per-capita ARR extremely high (industry top)

**Applies to**: Model companies / frontier AI research

**Doesn't apply to**: 99% of application-layer companies

#### Pattern 2: Notion / Cursor "Elite Eng-Heavy" Structure

**Traits**:
- Engineers >50% of company
- Lean PM team (1 PM per 10-20 engineers)
- Independent Eval team (new role!)
- Marketing / Growth team small but PLG (Product-Led Growth)

**Notion public signals**: Core AI team is small (within a ~100-engineer team, only a subset focuses on AI). Independent Eval Team (one of the earliest in the industry). PLG-driven. dual-track eval (regression + frontier) lets specific workflows speed up nearly 10x (from Notion × Braintrust case study).

**Cursor public signals (2025-Q3 snapshot)**: ~100-person engineering team, $1B-scale ARR (still expanding), per-capita ARR far above traditional SaaS.

**Applies to**: AI application SaaS / developer tools
**Core playbook**: PLG + high product quality + engineering excellence

#### Pattern 3: Lovable "Founder-led + AI" Tiny Team Structure

**Traits**:
- 5-20 person total team
- Founder + top engineers + 1-2 PMs
- Heavy reliance on AI tools (Claude Code / Cursor) for development
- User ops via community + KOL

**Lovable public signals (2025-Q3 snapshot)**: ~18-person company, ~$17M ARR, per-capita ARR approaching $1M (rivals early Anthropic). Founder Anton Osika publicly said "we have 0 PMs, engineers do PM work." Note: Lovable grows fast, team and ARR may double within months.

**Microsoft public signals**: Internal engineers all on Copilot. Satya Nadella said at Q1 2025 earnings call "as much as 30% of our code is now written by AI."

**Applies to**: Early-stage startups / solo developers / small AI products
**Core playbook**: Extreme few-people + extreme AI leverage

---

## What the Boss Should Really Ask

Not "how many to lay off" — but "**what kind of people should I build**."

### 4 Roles to Transition

#### Role 1: Junior PM → AI PM
- Old work: writing PRDs / user research / driving projects
- New work: writing specs + eval cases / reading traces / running prompt experiments

#### Role 2: Traditional Software Engineer → AI Engineer
- Old work: coding / fixing bugs
- New work: coding + using AI to code + writing evals + prompt engineering

#### Role 3: QA / Test → Evaluator
- Old work: manual testing / automated testing
- New work: designing eval sets / aligning LLM judges / labeling bad cases

#### Role 4: Customer Service / Operations → AI Trainer
- Old work: answering users / flagging issues
- New work: labeling bad cases / maintaining RAG knowledge base / tuning prompts

### The 1 Role to Actually Cut

Only 1 — **pure repetitive labor roles**.

Examples: data entry (now OCR + LLM), simple classification (now LLM), template-based generation (now LLM).

But this category **isn't large** — typically 5-10% of headcount.

### 3 New Roles to Add

#### New Role 1: Eval Engineer / Evaluator
- Responsibilities: design eval sets / maintain LLM judges / track bad case distribution
- **Notion has set up an independent team** — the industry's most consensus new role

#### New Role 2: Prompt Engineer / AI Engineer
- Responsibilities: write system prompts / design few-shot examples / optimize RAG / tool use
- Ratio: 1 per 3-5 engineers

#### New Role 3: AI Ops / LLMOps
- Responsibilities: monitor dashboards / configure hard caps / handle bad case emergencies
- Ratio: 1 per 50 engineers

---

## Part 2: Engineering Reality

### The Real Meaning of the Klarna Lesson

**2024-02**: Klarna CEO Siemiatkowski announced "AI replaced the equivalent of 700 customer service agents." (Note: Klarna used hiring freeze + natural attrition, not one-time layoffs)

**2025**: CEO publicly admits "AI lacks empathy, can't handle complex issues," **re-opens hiring, transitions to hybrid model**.

The real meaning isn't "AI doesn't work" — it's "**AI Native ≠ headcount reduction**".

Klarna's AI Native transformation could have been done this way:
- Don't freeze hiring
- Let each CS agent use AI tools, **3-5x productivity boost**
- Same headcount serves 3-5x demand volume
- When business expands, **faster than competitors**

**Actual approach (questionable)**: Hiring freeze + attrition → customer experience drops → re-hire → IPO PR pressure
**Better approach**: Keep CS agents → arm them with AI tools → 3-5x productivity → advantage during expansion

### "AI Replaces Humans" vs "AI Arms Humans" — Fundamental Difference

| Dimension | AI Replaces | AI Arms |
|-----------|-------------|---------|
| Team size | Cut 50%+ | No cut or minor |
| Short-term cost | Drops significantly | Flat or slightly up |
| Long-term productivity | Drops significantly (30-50%) | Increases significantly (3-5x) |
| Customer experience | Risky (Klarna / DPD) | Improves |
| Legal risk | High (Air Canada) | Low |
| PR risk | High | Low |
| Business expansion speed | Slow (needs to re-hire) | Fast (5x with existing people) |

**Counter-consensus truth**: **AI Native's core playbook is using AI to make team productivity explode** — not saving people, but **letting 100 people do the work of 500**.

### Cat Wu's Anthropic Product Note Core View

Cat Wu (Head of Product, Claude Code) wrote in the 2025 Product Note:
> "**Prototypes over PRDs**" / "**Spec-first**" / "**Daily user sentiment loop**"

Translation —
- Don't write PRDs, build prototypes directly (with Claude Code)
- Don't write requirements docs, write specs (input / output / eval criteria)
- Look at user sentiment daily (don't wait for data)

**This is how AI Native PMs work** — completely different from traditional PMs.

---

## The Boss's Transformation Roadmap

Help the boss understand "how should our company change" — give an executable roadmap:

### Stage 1 (1-3 months): Pilot
- Pick 1 team (e.g., CS) to arm with AI
- No layoffs, let the team use AI tools
- Observe productivity changes + customer satisfaction

### Stage 2 (3-6 months): Expansion
- Push pilot lessons to 2-3 teams
- Hire 1 Eval Engineer
- Hire 1 Prompt Engineer
- Get PMs and engineers using Claude Code / Cursor

### Stage 3 (6-12 months): Org Reshaping
- Hire AI Ops for monitoring
- Transition QA team into Evaluators
- When business expands, **prioritize AI-powered productivity, not new hires**

### Stage 4 (12-18 months): Maturity
- Whole company runs on "Human × AI = 5-10x productivity"
- Per-capita ARR significantly above competitors
- Business expansion faster than industry

**Key**: This roadmap has **no "layoff" step** — that's the core insight PMs help bosses see.

---

### Next-Generation AI Native Team — Agent Ops, Not Human Ops

The 3 patterns + 4-stage roadmap above are the **current** AI Native — Human × AI = 5-10x productivity. But to be honest with readers — **12-24 months from now, a 4th pattern emerges: PMs no longer manage humans, PMs manage a fleet of Agents**.

Industry signals already running in 2026 —

**AgentOps becoming a standard enterprise function**. IBM, Red Hat, UiPath, Salesforce all wrote AgentOps into their official 2025-2026 documentation — "DevOps made software reliable, MLOps made models production-ready, AgentOps makes agentic AI trustworthy."

**Salesforce Agentforce Operations** launched in 2026 — directly handing back-office workflows to "specialized agent fleets," tagline being "without ripping and replacing existing systems" — meaning big companies are no longer debating "should we restructure," but **layering an agent fleet on top of existing org**.

**"Humans move up the stack"** is now the industry consensus framing. People remain in orchestration / strategy / exception handling three layers — **execution layer is 100% by agents**.

**This isn't layoffs — it's PM's management surface expanding from 6 humans to 6 agents + 6 humans** — same headcount, each person's leverage grows. This is consistent with the 5 data points above (AI arming, not replacing): just upgraded from "same role + AI tools" to "same people + Agent fleet."

This means the 4th pattern: **The PM's reports aren't 4 engineers + 2 designers, but 6 specialist agents + 1 lead agent + 1 grader**. 1-on-1 becomes trace review, OKR becomes agent rubric.

For now, see this article's 3 patterns + 4 stages clearly. But readers should keep one thing in mind — **what bosses will really ask in 18 months isn't "AI arming humans," it's "when do we start hiring an AgentOps Lead"**. PMs who can answer this question = the default answer for B2B inbound consulting.

---

## 5 Industry Data Points (Proving AI Native = Arming Humans)

### Data Point 1: Microsoft Engineers All on Copilot
Satya Nadella publicly said "as much as 30% of our code is now written by AI" — but Microsoft **didn't lay off**.

### Data Point 2: Notion AI Team Sped Up ~10x
Small core AI team + dual-track eval, specific workflow accelerated ~10x (from Notion × Braintrust case) — **core playbook is productivity explosion, not headcount army**.

### Data Point 3: Lovable's 18-person Team Built $17M ARR (2025-Q3)
Not because "AI replaced humans" — because "AI made each person 10x productive". **A small team can do what used to need hundreds**.

### Data Point 4: Klarna Counter-Example
Hiring freeze + attrition → customer experience drop → re-hire — proves "headcount reduction model" isn't sustainable in production.

### Data Point 5: Cursor's 100-Person Team at $1B ARR
Per-capita ARR far above traditional SaaS — **Cursor isn't "using AI to replace humans," it's "using AI to let 100 people do the work of thousands."**

---

## QE Lens: AI Native Teams = System-Level Productivity Upgrade

**8 years of Quality Engineering perspective** —

The essence of any industrial revolution is "**productivity upgrade**," not "**layoffs**."

- Steam engine era: weavers went from 100 cloth/hour → 1 cloth/hour — but textile industry total headcount **grew** (demand exploded)
- Computer era: accountants went from manual ledgers → Excel — but finance roles **grew** (business complexity exploded)
- AI era: PM / engineer / ops from manual → AI-powered — **business complexity will explode again**, headcount **will also grow**

What's wrong with the "AI replaces humans" logic? — **It assumes business volume is fixed**.

But AI-era business volume will explode —
- Users expect more (AI personalization, real-time response)
- Competition fiercer (everyone uses AI)
- New opportunities more (new business scenarios AI creates)

**AI Native = AI Arming Humans + Business Volume Explosive Expansion** — that's the truth.

PMs must help bosses see this — **the boss who lays off = the boss's company gets cut**.

---

## Your Action Checklist

#### Action 1: Identify your company's AI Native pattern
- Are you Anthropic / Notion / Lovable mode?
- Don't copy blindly

#### Action 2: Build the "4-stage transformation roadmap" for your boss
- Pilot / Expansion / Reshaping / Maturity
- Emphasize "no layoff step"

#### Action 3: Identify 4 roles to transition in your company
- Junior PM / Engineer / QA / Ops
- With matching training plans

#### Action 4: Identify 3 new roles to hire
- Eval Engineer / Prompt Engineer / AI Ops
- Write JDs for the boss

#### Action 5: Protect those tagged for layoff
- Only "pure repetitive labor" should be cut
- Everyone else should transition, not be cut

---

## Counter-Consensus Quotes

- **"AI Native isn't AI replacing humans — it's AI letting one person do the work of ten."**
- **"Boss lays off = boss's company gets cut — Klarna is the textbook counter-example."**
- **"Lovable did $17M ARR with 18 people — not because AI replaced hundreds, but because 18 people + AI = the productivity of hundreds."**

---

## Closing Thoughts

This article is the org section's core — the B2B funnel engine.

After reading this, the boss will think — "how does our company transform?" — and that's when your consulting inbound starts.

The next article is **the whole season's finale** —

Article 26 talks about — **AI-era PM growth path**.

---

> **Companion Resources**: AI Native 3-Pattern Self-Check + Boss 4-Stage Roadmap + New Role JD Templates (paid readers)
> **Next Up**: 26 · Finale — Personal Native vs Company Native, Two Independent Tracks
> **Feedback / Reader Community**: WeChat Official Account 「蔡逸雯」

---

> **Reading the Chinese original?** See [25-ai-native-team.md](./25-ai-native-team.md)
> **Part of**: Season 1 · AI PM Workflow Reconstruction · 26 essays
> **Author**: Cai Yiwen (蔡逸雯) · 8 years in QE → AI PM
