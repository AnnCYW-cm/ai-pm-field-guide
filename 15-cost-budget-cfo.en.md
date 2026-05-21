# 15 · Cost Budget & Hard Caps — The AI Product PRD a CFO Can Actually Read

> Season 1 《Rebuilding the PM Workflow for the AI Era》· Chapter 15 · Part III: PRD (the column's hard currency)
> Estimated length: 5000 words

---

The fourteenth "dismissive blind spot" —

**90% of PMs don't know how to talk money to a CFO**.

It's not that PMs can't do arithmetic. It's that most PMs **assume "cost is the engineer's or finance's problem"** — and then the first time the CFO slams the invoice on the table and asks "how much is this thing burning every month?", the PM stammers something vague, and **in that moment they get classified as "unprofessional"**.

By the end of this chapter you will know — **every AI product PRD must contain a "Cost Section that finance can read."** This is the full pipeline for converting tokens into RMB and getting the CFO's signature.

---

## Part 1 · Workflow

### The 3-Layer Cost Section

#### Layer 1: Unit cost (per-request)

```
single-call cost =
  (input_tokens × input price) +
  (output_tokens × output price) +
  (cache_read_tokens × cache price) +
  (other add-ons: embedding / tool calls / 3rd-party APIs)
```

⚠️ **The point that slaps every CFO in the face the first time**: **output is 3–10x more expensive than input**.

A typical chatbot, real numbers:
- input: 1M tokens × $0.15 = $0.15
- output: 2M tokens × $0.60 = $1.20
- total: **$1.35/M tokens** — 9x more than the "$0.15" on the pricing page

### Layer 2: Scale cost (per-MAU / per-month)

**Don't show the CFO tokens. Show RMB per monthly active user.**

```
monthly LLM cost =
  single-call cost × calls/user/month × MAU × (1 + retry factor) × top-1% spike factor
```

Example. A customer-service chatbot:
- single-call cost ¥0.05
- 30 conversations per user per month
- MAU 100,000
- retry factor 1.3
- top-1% spike factor 1.5

monthly LLM cost = 0.05 × 30 × 100,000 × 1.3 × 1.5 = **¥292,500**

### Layer 3: Hard cap (circuit breaker)

Configure automatic breaker conditions:
- monthly cost > 80% of budget → automatic alert
- monthly cost > 100% of budget → automatic downgrade (switch to cheaper model)
- monthly cost > 120% of budget → automatic service pause (avoid unbounded burn)

**OpenAI / Azure both natively support monthly budget hard cap.** Configure it before launch — don't wait for the CFO to @ you in the group chat.

### The CFO Cost Card Template

A CFO cannot read "5K input + 1K output". A CFO reads this:

```
| Dimension | Value |
|-----------|-------|
| MAU | 100,000 |
| Calls per user per month | 30 |
| Total calls | 3,000,000 |
| Single-call cost (incl. retry) | ¥0.05 |
| Total monthly LLM cost | ¥150,000 |
| Monthly ARR (at ¥29.9 subscription) | ¥899,400 |
| LLM cost as % of ARR | 16.7% |
| Other costs (servers/bandwidth/support) | ¥200,000 |
| Monthly gross profit | ¥549,400 |
| Gross margin | 61% |
| ⚠️ Top-1% spike risk | +¥30,000-50,000 uncertain cost |
| ⚠️ Hard cap threshold | ¥300,000 (triggers auto-downgrade) |
```

**The CFO version must include**:
- Use RMB, not USD
- Use MAU/month, not tokens/second
- Explicitly mark the retry factor and top-1% spike risk
- Compare gross margin to traditional SaaS
- Hard cap threshold clearly labeled

---

## Industry Best Practice on Hard Caps

### OpenAI native support

- **Monthly Budget hard cap**: once the limit is hit, all API calls return an error
- **RPM / TPM / RPD / TPD multi-dimensional quota**: per-minute / per-day / request count / token count, all enforceable

### Azure OpenAI

- **Quota-per-deployment**: each deployment gets its own quota
- Enterprise pattern: **per-customer / per-tenant quota + budget alerts**

### Industry best practice (Vellum / Traceloop)

"**N-consecutive-error breaker + spike detection + per-user hard cap**" — the mandatory triple-set for large-customer scenarios.

Concrete config:
- 5 consecutive failures → break that endpoint for 1 minute
- current spend vs rolling 7-day baseline > 3x → trigger spike alert
- single user single day cost > ¥100 → auto rate-limit

---

## Part 2 · Engineering Reality

### 3 Classic Cost-Runaway Paths

#### Runaway 1: Context accumulation

A 20-step agent loop, 1K token output per step:
- intuition: cumulative input = 20K
- reality: cumulative input = **210K** (quadratic blow-up)

Why? Step N's input includes everything from steps 1 through N-1.

**Mitigation**: cap agent steps (≤ 10) or actively truncate the history context.

#### Runaway 2: Retry explosion

One team misconfigured a retry loop — **burned $72,000 of OpenAI credit overnight**.

Mechanism: model fails → retry → retry still fails → retry again → infinite loop.

**Mitigation**:
- Strict retry cap (max 3)
- Exponential backoff between retries
- Hard fail after retry exhaustion (do NOT continue)

#### Runaway 3: Adversarial users

Malicious users intentionally burning tokens:
- Upload extremely long documents (50K input each call)
- Trigger recursive calls
- Use prompt injection to force massive output

**Mitigation**:
- Per-user daily cap (e.g. ¥10)
- Per-request input/output cap
- Anomaly detection (abnormally long input / abnormally high frequency)

### Real Event: Cursor June 2025 Billing Blow-up

In June 2025, Cursor switched to credit-based billing without warning:
- Long-time users went from a "$20 mental model" to $200-$400 in overages
- Hacker News users posted "**$350 in a week**" — equivalent to monthly cost spiking to 10–20x
- On July 4 the CEO publicly apologized and issued refunds

**This is the cleanest public sample for telling a CFO "if we ever did this..."**

Lessons:
1. **Billing model changes must give existing users ample notice**
2. **The new model must have transparent cost ceilings**
3. **Accidental overruns must auto-break, not auto-charge**

---

## CFO Talk-Track Translations

A CFO does not ask about tokens. They ask about RMB.

### Translation templates

❌ Don't say: "We use GPT-5.1, input $1.25/M, output $10/M."
✅ Say: "**Our LLM cost is ¥3.2 per MAU, leaving ¥27 of gross margin headroom.**"

❌ Don't say: "Context window is 8K."
✅ Say: "**Single-conversation cap is 5,000 characters**; beyond that gets truncated."

❌ Don't say: "Prompt caching hit rate is 74%."
✅ Say: "**After enabling cache, the monthly bill dropped from ¥450K to ¥45K.**"

❌ Don't say: "3 retries quadruples cost."
✅ Say: "**A 1% failure rate adds ¥X to monthly cost.**"

**The CFO doesn't speak tokens — but they do speak ¥3.2, 5,000 characters, ¥45K.**

---

## High-ARR / Low-Margin: The Industry Reality

Baseline data every PM must internalize:

### Anthropic's inference cost once exceeded its revenue
Per The Information's reporting, Anthropic's inference compute spend once exceeded the same-period revenue — **burning faster than earning** (gross-margin figures vary by reporting methodology; use vendor-disclosed financials as the authoritative source).

### OpenAI 2025 revenue ~$13B, expected to post massive net losses (per The Information / Reuters)
Revenue rises, losses rise.

### The industry meme that's actually true
A certain AI coding startup: "**$100M ARR / $120M model bill**" — **negative gross margin**.

### ICONIQ 2025 survey
Average AI product gross margin 2024 = 41% / 2025 = 45% / 2026 = 52% — **still far below traditional SaaS at 70-80%**.

### Jevons paradox, live specimen
Token prices have fallen 99.7%, yet enterprise AI total spend has **risen to $37B**.

---

## The 5 Cost Questions a CFO Will Always Ask

Before PRD review, answer these 5 yourself:

| # | What the CFO asks | What the PM must be able to answer |
|---|-------------------|------------------------------------|
| 1 | How much does this burn per month? | ¥X / MAU; at scale X, monthly cost ¥X |
| 2 | How much do the top 1% users burn? | ¥X, needs hard cap |
| 3 | What happens when we blow the budget? | Auto-break to [fallback model / rules / pause] |
| 4 | LLM cost as % of ARR? | X% (healthy < 30%, warning > 30%, dead > 50%) |
| 5 | What are peers running for gross margin? | ICONIQ 41–52%, traditional SaaS 70–80% |

If you can't answer all 5 → **don't go to the CFO**.

---

## QE Lens: Cost Budget = the Resource Budget of the AI Era

**8 years of software quality engineering perspective** —

Any production-grade system design must have a **resource budget** — CPU, memory, bandwidth, disk IO. The core move of a resource budget is "**unit economic model + monitoring thresholds + automatic breakers**".

Applied to AI products, tokens are the new generation of "resource" —

- Unit economic model = cost per user per month
- Monitoring threshold = monthly LLM cost as % of ARR < 30%
- Automatic breaker = monthly budget hard cap

The traditional software PM asking "how many servers does this feature need" — that's the baseline move.
The AI-era PM must ask "how many tokens does this capability burn per month" — that's the new baseline move.

**Not knowing this answer = not a qualified AI PM.**

---

## Action Checklist

#### Action 1: Every AI product PRD must contain a Chapter 7 — Cost Budget
- 3-layer structure (unit / scale / hard cap)
- CFO-readable card format
- RMB, not USD

#### Action 2: Configure monthly budget hard cap before launch
- OpenAI / Azure / Anthropic all support it
- Don't wait until things go off the rails

#### Action 3: Answer the CFO 5-Question set before PRD review
- Can't answer all → PRD is not ready
- Answer all → then go to the CFO

#### Action 4: Monthly cost retrospective
- Actual vs budget delta
- Top-1% user consumption breakdown
- Re-tune the hard cap as needed

---

## Counter-Consensus Lines

- **"Your product isn't losing money on users — it's losing money on the 99% of tokens consumed by the top 1% of users."**
- **"The CFO can't read tokens, but they can read 'each active user burns ¥3.2'."**
- **"An AI product with no breaker is a Formula 1 car with no brakes."**

---

## Closing

This is the final chapter of the PRD section (Chapters 11–15).

By now you should have full AI-product PRD competency:
- Ch. 11 — PRD skeleton (4-add + 2-cut)
- Ch. 12 — How to write Eval (the 5 elements)
- Ch. 13 — EDD philosophy (eval before code)
- Ch. 14 — Bad Case grading (4 tiers + degradation strategy)
- Ch. 15 — Cost budget (CFO lens)

PRD section closes. We enter Part IV — **Delivery**.

Part IV will lead to the column's **trump card** — PMs using Claude Code to run validation without depending on engineers (Chapter 17).

But we placed it in Part IV rather than the opening because **consensus must be built first**. The first 15 chapters laid the foundation — without it, Claude Code is just another tool in your hands.

The next chapter covers the 72-hour MVP — **an AI product's MVP isn't a "smaller version of the product"; it's the "smallest unit that demonstrates a capability loop"**.

See you next chapter.

---

> **Companion Resources**: Cost card template (finance edition) + hard cap decision tree + CFO communication script comparison (unlocked for paid subscribers)
> **Next Up**: 16 · 72-Hour MVP Methodology — from PRD to demoable demo
> **Feedback / Reader Community: WeChat Official Account 「蔡逸雯」**

---

> **Bilingual notice**: This is the English translation of the original Chinese article. For the original Chinese version, please refer to the source file `15-cost-budget-cfo.md`. Some industry jargon (QE, FMEA, CFO, MAU, ARR, etc.) is kept in English by convention.
