# AI PM Field Guide

> **An AI PM's job isn't to write specs. It's to define boundaries and engineer degradation.**

A 26-essay industrial field guide for AI Product Managers, written from 8 years of Quality Engineering perspective.

> Season 1 · 26 essays · 9 toolkits · 95 references
> Author: [Cai Yiwen (蔡逸雯)](https://github.com/AnnCYW-cm) · WeChat Official Account 「蔡逸雯」
> 中文版 README: [README.md](./README.md)

---

## ⭐ The Signature Thesis

> **An AI PM's job isn't to write specs. It's to define boundaries and engineer degradation.**

The existing positions in our industry are each taken:
- **Hamel Husain**: *Eval-driven development*
- **Aparna Chennapragada**: *Prompt sets are the new PRDs*
- **Cat Wu**: *Prototypes over PRDs*
- **Marty Cagan**: *Discovery over delivery*

The position this book claims: **"Boundaries + Degradation"** — because AI is a probabilistic system, not deterministic. Models will fail, launches will hit surprises, business will surface needs beyond AI capability. The PM's two core actions are:

- **Define boundaries** — what AI can / can't do, when to escalate to humans
- **Engineer degradation** — what happens when it fails, fall back to rules, human handoff, postmortem

These are precisely the core actions of FMEA in 60 years of Quality Engineering tradition.

---

## Who This Is For

- **Working AI PMs** — already shipping AI products but workflow not systematized
- **PMs transitioning into AI** — have PM experience, don't know what to relearn
- **AI product team leads** — need to walk team through AI-Native workflow upgrade

**Not for**:
- AI engineers / ML researchers (this is PM-perspective)
- Zero-experience PMs (read a traditional PM primer first)
- Pure academics (this is industrial practice, not theory)

---

## 📖 26-Essay Table of Contents

**Preface** · [00 · About This Book](./00-preface.en.md)

### Part 1 · Needs Identification (Articles 1-6)
1. [6 Collapse Points · Why AI PM Workflow Must Be Reconstructed](./01-six-collapse-points.en.md) ⭐ *Opening*
2. [From Features to Capabilities](./02-from-features-to-capabilities.en.md)
3. [AI Product Needs No Longer Come from User Interviews](./03-not-from-user-interviews.en.md)
4. [Should-AI vs Should-Not-AI Decision Framework](./04-pseudo-ai-needs.en.md)
5. [4 Hard Boundaries of Agent Capability](./05-agent-capability-boundaries.en.md)
6. [Requirements Review SOP · 5-Signal Scorecard](./06-five-signals.en.md)

### Part 2 · Solution + PRD Framework (Articles 7-12)
7. [From Feature Flow to Capability Flow](./07-capability-flow.en.md)
8. [Model Selection · 4 Dimensions](./08-model-selection.en.md)
9. [Token Economics](./09-token-economics.en.md)
10. [Technical Path Decision Tree](./10-tech-path-decision-tree.en.md)
11. [PRD: 4 Adds, 2 Cuts](./11-prd-skeleton.en.md) ⭐ *Synthesis Original*
12. [Eval Section · 5 Elements Template](./12-eval-design.en.md)

### Part 3 · PRD Essentials (Articles 13-15)
13. [EDD · Eval-Driven Development](./13-eval-driven-development.en.md)
14. [Bad Case 4-Tier Grading](./14-bad-case-grading.en.md)
15. [Cost · Explaining to the CFO](./15-cost-budget-cfo.en.md)

### Part 4 · Delivery (Articles 16-19)
16. [72h MVP Methodology](./16-72h-mvp.en.md)
17. [PM × Claude Code · Battle Tested](./17-pm-claude-code.en.md) ⭐ *The Killer App*
18. [Multi-Axis Gradual Rollout Strategy](./18-gradient-strategy.en.md)
19. [Pre-launch Eval · 5 Categories](./19-pre-launch-eval.en.md)

### Part 5 · Operations (Articles 20-22)
20. [4 AI-Specific Monitoring Metrics](./20-monitoring-metrics.en.md)
21. [Bad Case Management · 5 Steps](./21-bad-case-management.en.md)
22. [The Courage to Downgrade · A PM's Checklist](./22-courage-to-downgrade.en.md)

### Part 6 · Collaboration (Articles 23-24)
23. [The New Collaboration Language with Engineers](./23-pm-engineer-language.en.md)
24. [The New Alignment Framework with Your CEO](./24-aligning-with-ceo.en.md)

### Part 7 · Organization + Finale (Articles 25-26)
25. [AI Native Teams · 3 Patterns](./25-ai-native-team.en.md) ⭐ *B2B Funnel Engine*
26. [Finale · Personal Native vs Company Native · Two Independent Tracks](./26-pm-growth-path.en.md)

📚 **References Index** · [27 · v1.1 References](./27-references.en.md) (95 citations · 9 highest-frequency URLs verified)

---

## 🛠️ 9 Copy-Paste-Ready Toolkits

| # | Toolkit | Article |
|---|---------|---------|
| 1 | 5-Signal Requirements Review Scorecard + 5 Rebuttal Templates | 06 |
| 2 | PRD: 4 Adds, 2 Cuts Skeleton | 11 |
| 3 | Eval Section · 5 Elements Template | 12 |
| 4 | Bad Case 4-Tier + Microsoft RAI Matrix | 14 |
| 5 | CFO Cost Card Template | 15 |
| 6 | 7 Battle-Tested Claude Code Prompts | 17 |
| 7 | Pre-launch Eval · 5-Category Checklist | 19 |
| 8 | 4 Downgrade Scenarios + 3 Communication Scripts | 22 |
| 9 | 4 Collaboration Playbook + Trace 5-Field Cheatsheet | 23 |

---

## 💡 4 Categories of Original Insight

1. **Synthesis Original**: PRD 4 Adds, 2 Cuts (the "2 Cuts" is counter-consensus — industry only talks about what to add)
2. **Local Insight**: Personal Native vs Company Native, two independent tracks (a global blindspot)
3. **Lens Original**: 8-year Quality Engineering perspective (FMEA / probabilistic thinking / knowing when to stop)
4. **Methodology Original**: 5-Signal Scorecard / 4-Scenario Playbook / Trace Minimum Set / CFO Cost Card

---

## 👤 Author Anchor

**8 years in Quality Engineering** (QA → Test Architect → PM). Three unique framings:

- **FMEA lens on PRDs** — 60-year QE tradition meets AI product design
- **Observability for probabilistic systems** — distribution-thinking, not mean-thinking, is QE instinct
- **"Knowing when to stop"** — the hardest judgment for a Quality Engineer, now the courage to downgrade

---

## 🤖 AI Collaboration Disclosure

Parts of this book were produced with **Claude Opus 4.7 (1M context)**:
- **AI-assisted**: case verification + citation organization + prose polishing
- **Author's original**: core thesis + framework + QE perspective + local insights
- **Responsibility**: all business judgments + final content rest with the author

**Why proactively disclosed**: This book teaches PMs to reconstruct workflow using Claude Code (Article 17) — the author using Claude to co-write this book **is the best demonstration of that workflow**.

What readers get is the genuine product of "PM × AI collaboration," not the outdated mode of "pretending I didn't use AI."

---

## ⚖️ Disclaimer

All citations are from **public sources** — fair use for evaluative purposes. Company names (Anthropic / OpenAI / Notion / Cursor / Lovable / Microsoft / Klarna / Air Canada / DPD, etc.), product names, and trademarks belong to their respective rights holders. **This is not an endorsement or commercial partnership.**

**Model data**: 2026-Q2 industry snapshot (Claude Opus 4.7 / GPT-5.5 / Gemini 3.1 Pro / DeepSeek V3.2 / Kimi K2.6). Models iterate fast — **verify against vendor official model cards within 3-6 months**.

Complete URL list: see [27-references.en.md](./27-references.en.md).

---

## 📜 License

**[CC-BY-NC 4.0](./LICENSE)** · Creative Commons Attribution-NonCommercial 4.0 International

You can:
- ✅ Read / share / cite freely
- ✅ Copy toolkits into your company's PRD process
- ✅ Reference in PM training / internal sharing (with attribution)

You cannot:
- ❌ Package as paid courses / books for sale
- ❌ Use in commercial products without attribution
- ❌ Tamper with or remove author attribution

**For commercial partnerships / licensing**: contact via WeChat Official Account 「蔡逸雯」.

---

## 💬 Feedback / Community

- **WeChat Official Account**: 「蔡逸雯」(Cai Yiwen)
- **Paid Practitioner Community** (monthly live + author's consulting Q&A): message "实战社群" on the account
- **Season 2 preview**: Context Engineering / Memory / Multi-Agent / Agent OS — coming Q3 2026

---

## ⭐ Star This Repo

If this book helps you —

⭐ **Star this repo** — the best feedback you can give the author
🔄 **Fork it** — write your own version, this methodology needs more local practice
📢 **Share with an AI PM friend** — let the community level up together

---

> **Season 1 Complete · Season 2 — Q3 2026**
