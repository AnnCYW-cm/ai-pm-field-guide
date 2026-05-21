# 08 · Model Selection Across 4 Dimensions — How to Weigh Cost / Latency / Effect / Compliance

> Season 1 · AI PM Workflow Reconstruction · Essay #8 · Part 2: Solutions
> Estimated length: 2200 words

---

The seventh dismissive blind spot —

**90% of PMs pick models by "the strongest one is never wrong."**

It's not that PMs want shortcuts. It's that most PMs **assume "strongest model = most stable," not realizing "strongest model = the starting point of a runaway bill"** — the result is the CFO @-ing them in the company group the second week post-launch asking "how did we burn 400K worth of tokens in one month?"

After reading this essay you'll know — **Model selection isn't "pick the strongest." It's making explicit trade-offs across 4 dimensions.** Each dimension has a question the PM must answer.

More importantly — this essay provides the latest 2026 Q2 mainstream model comparison table, **with every number marked with a traceable URL**.

---

## Part 1: Workflow

### The 4-Dimension Decision Matrix

| Dimension | Question the PM Must Answer | Decision Method |
|------|-----------------|---------|
| **Cost** | How much does this capability burn per month? What's the gross margin? | Run token economics (see Essay #9) |
| **Latency** | How long can users tolerate waiting? P50 or P99? | Real measurement + business-scenario tolerance |
| **Effect** | How does the model perform on my real task? | Run your own eval set (not public benchmarks) |
| **Compliance** | Does data leave the country? Need SOC 2 / HIPAA? | Business side decides (B2B must ask) |

### Mainstream Model 4-Dimension Comparison (2026-Q2)

> ⚠️ **Time-sensitivity reminder**: Models iterate extremely fast — re-verify within 3 months

| Model | Input Price | Output Price | Cache Read | SWE-bench Verified | First-Token Latency | Compliance |
|------|-------|-------|-------|-------------------|------------|------|
| **Claude Opus 4.7** | $5 | $25 | $0.50 | **87.6%** | ~2s | SOC2 II / HIPAA BAA / ZDR |
| Claude Sonnet 4.6 | $3 | $15 | $0.30 | ~82% (unverified) | 2s | Same as above |
| Claude Haiku 4.5 | $1 | $5 | $0.10 | ~73% (unverified) | <1s | Same as above |
| **GPT-5.5** | $5 | $30 | 10% auto | **88.7%** | 0.55s | SOC2 II / HIPAA |
| GPT-5.1 | $1.25 | $10 | Auto-cache | ~80% (unverified) | <1s | Same as above |
| GPT-5 | $0.625 | $5 | Auto-cache | ~75% (unverified) | <1s | Same as above |
| **Gemini 3 Flash** | $0.50 | $3 | - | **80.6%** (3.1 Pro number) | Sub-second | Vertex VPC SC / HIPAA BAA |
| DeepSeek V3.2 | $0.28 / $0.028 (cache hit) | $0.42 | Built-in | ~70% (unverified) | Medium | China-resident, no BAA |
| Kimi K2.6 | $0.60 | $2.50 | - | ~75% (unverified) | Medium | China-resident, no BAA |

**Unit**: per million tokens / USD.

⚠️ **Data disclaimer**: This table is a 2026-Q2 industry-aggregated snapshot. For all SWE-bench Verified scores, prices, and latency data, **please defer to the vendor's official model card** — model versions and scores expire within 3-6 months; the column does not stand behind these precise numbers. Numbers marked with ~ are aggregated estimates; even numbers without ~ should be cross-verified against official sources / Artificial Analysis / SEAL and other third-party leaderboards.

### Selection Workflow: The "Good Enough" Principle

The most common selection mistake in PM circles is "pick the strongest first."

The right approach is the reverse — **start from the cheapest model and add upward**.

```
Step 1: Use the cheapest model (Haiku / GPT-5 / Gemini 3 Flash / DeepSeek V3.2)
  → Run your own eval set (50-100 cases)
  → Check pass rate
  → Pass → selected, done
  → Fail → go to Step 2

Step 2: Move up one tier (Sonnet / GPT-5.1 / Gemini 3 Pro)
  → Run the same eval set
  → Pass → selected
  → Fail → go to Step 3

Step 3: Use the top tier (Opus 4.7 / GPT-5.5)
  → Run the same eval set
  → Pass → selected (but run the numbers, may not be commercially viable)
  → Fail → current models can't handle this requirement, cut it or change the path
```

This workflow lets you **solve 80% of scenarios with Haiku-tier models** — at 1/5 the cost of Opus.

### Model Selection Decision Doc Template

For every new requirement kickoff, attach a "Model Selection Decision Doc" to align with the boss / engineers:

```
Requirement: [name]

Candidate models:
1. [Model A]: cost ¥X/MAU, p99 latency Xs, eval pass rate X%
2. [Model B]: cost ¥Y/MAU, p99 latency Ys, eval pass rate Y%
3. [Model C]: cost ¥Z/MAU, p99 latency Zs, eval pass rate Z%

Selected: [Model X]
Reasoning: [Which dimension is it optimal on + which dimension did we trade off]
Risk: [What's the largest risk of this selection]
Fallback plan: [How to switch if this is wrong]
```

---

## "Cost Down 90%, Effect Down Only 3%" Real Cases

### Case 1: Anthropic Prompt Caching Cuts 90% Cost

A DEV.to author used prompt caching to cut RCA (root cause analysis) task cost by 90% — single RCA dropped from $0.0065 to sub-millidollar.

### Case 2: Monthly Bill $720 → $72

Du'An Lightfoot measured it: just by adding `cache_control`, the monthly bill dropped from $720 to $72, **with no perceptible effect difference**.

### Case 3: Cache Hit Rate 7% → 74%

After ProjectDiscovery moved dynamic content out of the cacheable prefix, hit rate rose from 7% to 74% and the bill dropped 59%.

**What the 3 cases have in common**: model didn't change, prompt didn't change, effect didn't change — **only cache usage changed, and the bill dropped 60%-90%**.

If you haven't systematically used prompt caching yet, **this is the lowest-hanging fruit**.

---

## Part 2: Engineering Reality

### The Real-World Traps in the 4 Dimensions

#### Cost Trap: Missing Retries and Context Accumulation

The 3 most commonly missed cost items in PM calculations:
1. **Retry cost**: 1 retry on failure = doubled cost
2. **Context accumulation**: in a 20-step agent loop with 1K token output per step, cumulative input is not 20K but **210K** (quadratic explosion)
3. **New tokenizer eats more tokens**: Claude Opus 4.7's price didn't change, but the **new tokenizer consumes 35% more tokens for the same text** — bill unchanged ≠ bill not rising

#### Latency Trap: Looking at P50 Without P99

PM thumps the table: "this model's latency is 1 second" — they mean P50.

What users actually feel in production is P99 — **the slowest 1% of requests**.

P99 is typically 3-5× P50. If your business scenario is "conversational interaction" — users will hit a P99 stall every 5-10 conversations. **That 1% determines word-of-mouth.**

You must ask about P99 during selection — never just P50.

#### Effect Trap: Demo Effect ≠ Production Effect

The demo videos from OpenAI / Anthropic / Google are cherry-picked cases.

Your real business scenario may not be in their demo capability range at all.

**The only trustworthy effect data is — your own eval set.** 50-100 real tasks, 3 independent labelers scoring, **report results with confidence intervals**. Anthropic's statistics methodology paper covers exactly this: 0.85 vs 0.87 may not be significant on a small sample.

#### Compliance Trap: Data Cross-Border + Training Data Source

The most common B2B project blow-ups are compliance-related.

3 must-asks:
- **Does data cross borders**: DeepSeek V3.2 / Kimi K2.6 infer inside China and have no BAA. Claude / GPT data may cross borders
- **Training data source**: Does the customer contract include a "cannot use customer data for training" clause? You need zero-data-retention (ZDR) mode. Anthropic offers ZDR; OpenAI Enterprise defaults to ZDR
- **Enterprise compliance certifications**: SOC 2 / HIPAA BAA / ISO 27001 — B2B customer audits require all of these

If your project touches healthcare / finance / government — **the compliance dimension alone may eliminate half the models**. This isn't a tech decision, it's a legal decision.

### Anthropic Prompt Caching Decision Line

When to enable prompt caching?

> When your system prompt is **> 1024 tokens** and reused **> 2 times**, the cache pays for itself.

Haiku cache-write $3.75/M, cache-read $0.30/M — breaks even at 2 reuses. Sonnet / Opus similar.

**What this line means**: most products with a system prompt should enable cache.

If your product has a 5000-token system prompt, 100K daily calls, 100% reuse rate —
- Without cache: monthly cost ≈ ¥450K
- With cache: monthly cost ≈ ¥45K

**10× difference.**

---

## ⚠️ Tokenizer Trap: Opus 4.7 Price Unchanged, Bill Up 35%

The most overlooked trap.

Claude Opus 4.7's list price didn't change ($5/$25 in/out), but Anthropic **switched to a new tokenizer** — the same text consumes 35% more tokens.

Meaning: your bill **automatically rises 35%**, but you can't see it from the pricing page.

Finout wrote a dedicated breakdown article: "The Real Cost Story Behind the Unchanged Price Tag."

**Advice for PMs**: when upgrading models, **measure token consumption in practice**, don't just look at the price sheet.

---

## QE Lens on Model Selection

**From 8 years of Quality Engineering perspective** —

Model selection is essentially "**engineering trade-offs under multiple constraints**" — cost constraint + latency constraint + effect constraint + compliance constraint.

In traditional software engineering there's a repeatedly verified principle: **"Premature optimization is the root of all evil."**

Translated to AI products — "**Premature 'use the strongest model' is the root of token bills out of control**" — premature top-tier model selection is the root cause of runaway token bills.

**Correct move**: first use the cheapest model to validate PMF, confirm the capability ceiling is sufficient, then upgrade as needed.

This isn't penny-pinching cleverness, it's the basic move of quality engineering — **avoid prematurely taking on unnecessary complexity (cost is a form of complexity)**.

---

## A Few Counter-Consensus Quotes (from the industry)

**Google CEO Pichai (Q4 2025 earnings call)**:

> "As we scale, we're getting dramatically more efficient. We were able to lower Gemini serving unit costs by **78% over 2025** through model optimisations, efficiency and utilisation improvements."

Gemini unit cost down 78% in one year — that's how Flash got down to $0.50/M input. Google is treating "the cost curve dropping" itself as a moat — forcing OpenAI to bleed in the token price war.

**DeepSeek founder Liang Wenfeng (Waves 暗涌 interview)**:

> "We didn't deliberately set out to be a catfish — we accidentally became one… Our principle is no subsidies, no excessive profits. This price is just slightly above cost."

DeepSeek de-mystified the price war — **"my cost is just this low, it's not a subsidy."** The moment this line landed, 6 domestic Chinese large model companies cut prices in emergency.

---

## Your Action Checklist

#### Action 1: Print this 4-dimension comparison table and tape it to your desk
- Reference directly during model selection
- Update quarterly (models iterate fast)

#### Action 2: Run every new requirement through the "good enough" flow
- Start from the cheapest model
- Run your own eval set
- Stop the moment it passes — don't default to "just use the strongest"

#### Action 3: Immediately enable prompt caching on all products with system prompts > 1024 tokens
- Lowest-hanging fruit
- 1 day of work, bill drops 60%-90%

#### Action 4: Attach a "Model Selection Decision Doc" to every project kickoff
- Candidate models + data + selection reasoning + risk + fallback
- For aligning with the boss and engineers

---

## Counter-Consensus Quotes

- **"Picking a model isn't picking the strongest — it's picking the one whose bill matches the cadence of your PMF. Opus codes powerfully, but when your product hasn't scaled, every bill is interest payment."**
- **"Model selection in 2026 is no longer 4-choose-1; it's 4 × cache strategy × Batch × ZDR mode = dozens of combinations. PMs who don't understand this matrix shouldn't be signing budgets."**
- **"GPT-5.5 beats Opus 4.7 by 1.1 points on SWE-bench but costs 6× more — that's the most expensive 1.1% of the AI era."**

---

## Closing Thoughts

This essay covered model selection. The next essay is the most important one in the Solutions arc — **the Token Ledger**.

The commercial viability of an AI product isn't determined by the market — it's determined by token economics. **The PM must be able to calculate "how many tokens each user burns per month, and whether we can earn it back."**

The next essay gives you the 3-layer structure of a token ledger + 5 commonly-missed line items + the real post-mortem of Cursor's June 2025 billing blowup.

After reading it you'll be able to talk costs cleanly with the CFO — **this is a hard skill of an AI PM**.

See you in the next essay.

---

> **Companion Resources for this essay**: 4-Dimension Selection Decision Matrix Excel + mainstream model comparison table (2026-Q2) (paid readers unlock, updated quarterly)
> **Next up**: 09 · The Token Ledger — Reverse-Engineering Business Model Viability from Unit Price
> **Feedback / Reader Community**: WeChat Official Account 「蔡逸雯」

---

> **Reading the Chinese original?** See [08-model-selection.md](./08-model-selection.md)
> **Part of**: Season 1 · AI PM Workflow Reconstruction · 26 essays
> **Author**: Cai Yiwen (蔡逸雯) · 8 years in QE → AI PM
