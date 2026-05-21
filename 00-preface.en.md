# Preface · About This Book

> Season 1 · *AI PM Workflow Reconstruction* · Opening Note
> Author: Cai Yiwen (蔡逸雯) · WeChat Official Account 「蔡逸雯」

---

## The Core Thesis of This Book

> **An AI PM's job isn't to write specs. It's to define boundaries and engineer degradation.**

That's the signature of all 26 essays in Season 1.

The existing framings in our industry each claim their own position:
- **Hamel Husain**: "Eval-driven development is the defining skill for AI PMs"
- **Aparna Chennapragada**: "Prompt sets are the new PRDs"
- **Cat Wu**: "Prototypes over PRDs"
- **Marty Cagan**: "Discovery over delivery"

The position I claim — **"Boundaries + Degradation"**.

Why these two things? Because AI is a **probabilistic system**, not a deterministic one —
- Models will always fail (see Article 14 · Bad Case 4-Tier Grading)
- Production launches will always hit surprises (see Article 19 · Pre-launch Eval, 5 Categories)
- Business will always surface needs beyond AI boundaries (see Article 5 · Agent Boundaries + Article 22 · Courage to Downgrade)

So the PM's two core actions are:
- **Define boundaries** — what AI can do / can't do / when to escalate to humans in this scenario (Articles 2 / 5 / 7 / 11 / 23)
- **Engineer degradation** — what happens when it fails / fall back to rules / human handoff / postmortem (Articles 14 / 19 / 21 / 22)

**If an AI PM column can't make you internalize these two things, everything else is nice-to-have.**

And these two things — **are precisely the core actions of FMEA in 60 years of Quality Engineering tradition**. That's why the author's 8 years of QE background becomes the real moat of this book.

---

## Who This Book Is For

**Primary readers**:
- **Working AI PMs** — you're already shipping AI products but your workflow isn't systematized
- **Traditional PMs transitioning into AI** — you have PM experience but don't know what to relearn for the AI era
- **AI product team leads** — you need to walk your team through the "AI Native PM" workflow upgrade

**Not for**:
- AI engineers / ML algorithm engineers (this is a PM-perspective book, technical depth only goes as deep as PMs need)
- Beginner PMs with zero experience (read a traditional PM primer first)
- Pure academic researchers (this is industrial practice, not AI theory)

---

## What This Book Does NOT Cover

Honest disclosure —

1. **Doesn't teach you prompt syntax** — that's an engineer's job, PMs only need to understand boundaries (see Article 23)
2. **Doesn't teach fine-tuning / RAG / inference optimization implementation** — PMs don't need this
3. **Doesn't reproduce Hamel / Cat Wu / Aparna's original work** — the latest global frontier concepts (Context Engineering / Memory Architecture / Agent OS) are not covered in this season, saved for Season 2
4. **Doesn't predict stock prices or teach AI investing** — this is a PM column, not an investment newsletter

---

## What Makes This Book Different

Most Chinese AI PM content is **translation of Lenny / Marty Cagan / Sachin Rekhi**.

What's different here —

**Author anchor: 8 years in Quality Engineering** (QA → Test Architect → PM). This gives 3 unique framings:
- **FMEA lens on PRDs** — failure mode analysis is a 60-year QE tradition; introducing it to AI PRDs is a new combination
- **Observability for probabilistic systems** — looking at AI output as a *distribution* rather than a *mean* is instinctive to QE
- **"Knowing when to stop"** — courage to downgrade is the hardest judgment for a Quality Engineer

**Local insight**: Most Chinese PMs are stuck in the dilemma of "company hasn't started AI transformation + I personally have ambition." **Global content defaults to your company being OpenAI / Anthropic, an AI-Native shop — this book is specifically for the Chinese context.**

---

## Disclaimer

All industry cases, report data, KOL quotes, and model data cited in this book come from **public sources**, and use is evaluative (fair use).

Company names (Anthropic / OpenAI / Notion / Cursor / Lovable / Microsoft / Klarna / Air Canada / DPD, etc.), product names (Claude Code / ChatGPT / Cursor, etc.), and trademarks belong to their respective rights holders. **This book is not an endorsement or commercial partnership.**

KOL public views cited (Hamel Husain / Cat Wu / Sachin Rekhi / Mike Krieger / Aparna Chennapragada, etc.) — sources are public interviews / blogs / podcasts / conference talks / Twitter. Complete URL list in companion resource: *References Index*.

**Model versions and data**: This book uses a 2026-Q2 industry snapshot (Claude Opus 4.7 / GPT-5.5 / Gemini 3.1 Pro / DeepSeek V3.2 / Kimi K2.6, etc.). **Models iterate fast — verify against vendor official model cards / Artificial Analysis / SEAL leaderboards within 3-6 months.** This book does not vouch for these precise numbers.

**Incident case data**: All amounts, dates, and impact data come from public news reports. The author has done due diligence on cross-verification (Air Canada CAD 650.88 / Klarna 700 customer service FTEs / Cursor billing incident, etc.), but **industry facts may be clarified or updated over time** — readers should cross-reference latest reports.

---

## AI Collaboration Disclosure

Parts of this book were produced in collaboration with **Claude Opus 4.7 (1M context)** —
- **AI-assisted**: case verification + industry citation organization + prose polishing
- **Author's original**: core thesis + framework structure + 8-years-of-QE perspective + local insights
- **Responsibility**: all business judgments + final content + accountability rest with the author

**Why I'm proactively disclosing this**: This book teaches PMs to reconstruct their workflow using Claude Code (Article 17) — the author using Claude to co-write this book **is the best demonstration of that workflow**.

What readers get is the genuine product of "PM × AI collaboration," not the outdated mode of "pretending I didn't use AI."

---

## Companion Resources

Every article ends with a "Companion Resources" line — unlocked for paid readers. **All 9 toolkits can be copy-pasted directly into your company's PRD process**:

| # | Tool | Article |
|---|------|---------|
| 1 | 5-Signal Requirements Review Scorecard + 5 Rebuttal Templates | 06 |
| 2 | PRD: 4 Adds, 2 Cuts Skeleton Template | 11 |
| 3 | Eval Section: 5 Elements Template | 12 |
| 4 | Bad Case 4-Tier Grading + Microsoft RAI Matrix | 14 |
| 5 | CFO Cost Card Template | 15 |
| 6 | 7 Battle-Tested Claude Code Prompts | 17 |
| 7 | Pre-launch Eval 5-Category Checklist | 19 |
| 8 | 4 Downgrade Scenarios + 3 Communication Scripts | 22 |
| 9 | 4 Collaboration Scenarios Playbook + Trace 5-Field Cheatsheet | 23 |

Also: **References Index** — complete URL list of all citations across 26 articles (KOL sources / third-party reports / incident news links), so readers can dig into any citation they want to research further.

---

## Feedback / Unsubscribe / Reader Community

- **Reader Community**: leave a message on WeChat Official Account 「蔡逸雯」
- **Feedback**: same channel
- **Refund policy**: per platform policy within 7 days
- **Season 2 preview**: Context Engineering / Memory Architecture / Multi-Agent Orchestration / Agent OS — the global frontier topics. Season 1 subscribers get priority pricing.

---

## One-Sentence Value Proposition

> **Saves you 50 hours of organizing Hamel / Cat Wu / Anthropic / a16z primary sources,
> gives you 9 PM toolkits to copy directly into your company,
> plus 4 categories of original insight (synthesis / local / lens / methodology).**

Now begin with Article 1 — **6 Collapse Points**.

---

> **Reading the Chinese original?** See [00-preface.md](./00-preface.md)
> **Part of**: Season 1 · AI PM Workflow Reconstruction · 26 essays
> **Author**: Cai Yiwen (蔡逸雯) · 8 years in QE → AI PM
>
> First published: 2026-05-21
> Season 1 · Complete
