# 09 · Token Economics — Reverse-Engineering Business Viability from Unit Price

> Season 1 · AI PM Workflow Reconstruction · Essay 9 · Part 2: Solutions
> Estimated length: 2,200 words

---

The eighth dismissive blind spot —

**90% of PMs calculate token economics by "it shouldn't be that expensive, right?"**

It's not that PMs can't do math. It's that most PMs **assume "cost is engineering's problem, or finance's problem"** — and then two weeks after launch the CFO slams the bill on the table and asks "why did we just burn $60K?", and the PM has no answer.

After reading this essay you'll know — **the viability of an AI product's business model is not decided by the market, it's decided by token economics**.

---

## Part 1 · Workflow

### The 3-Layer Token Ledger

#### Layer 1: Per-Call Cost

The cost of each user interaction with the AI:

```
per_call_cost =
  (input_tokens × input_price) +
  (output_tokens × output_price) +
  (cache_read_tokens × cache_price - savings) +
  (other costs: embedding / tool calls / 3rd-party APIs)
```

Critical reminder: **output is 3-10× more expensive than input**. **This is where CFOs get blindsided most often.**

Real chatbot math:
- input: 1M tokens × $0.15 = $0.15
- output: 2M tokens × $0.60 = $1.20
- Total: **$1.35/M tokens** — 9× more than the "$0.15" headline price

#### Layer 2: Per-User Active Cost

```
monthly_cost_per_user =
  per_call_cost × calls_per_month × (1 + retry_factor)
```

The retry factor is a huge trap — a single retry doubles cost.

Example: customer-service chatbot at ¥0.05/call, 30 conversations per user per month, retry factor 1.3:
- Monthly cost per user = 0.05 × 30 × 1.3 = **¥1.95/month**

#### Layer 3: Monthly Budget Ceiling

```
monthly_budget = monthly_cost_per_user × DAU × top_1%_spike_factor
```

The top-1% spike factor is the other big trap — **the top 1% of users burn 99% of the tokens**.

Example: DAU 100K, monthly cost per user ¥1.95, top-1% spike factor 1.5:
- Monthly budget = 1.95 × 100,000 × 1.5 = **¥292,500**

If you charge ¥29.9/month, gross-margin headroom is:
- ¥29.9 − ¥1.95 = ¥27.95
- 93% gross margin — **looks beautiful**

But if 1% of users burn ¥50/month (the chat addicts):
- That 1%'s margin = ¥29.9 − ¥50 = **−¥20.1 (negative)**
- The 99% of normal users' profit has to subsidize this 1%'s loss

**That's why your product looks profitable but the CFO keeps asking "why is there never enough cash?"**

### Reverse Workflow: Back-Solve the Budget from ARPU

Forward calculation (pick model first, then cost):
- Choose Opus → calculate cost → set price → calculate margin

**Wrong.**

Reverse calculation:
- How much can the user pay (ARPU)?
- What gross margin do you want (e.g., 50%)?
- Back-solve per-call budget
- Back-solve context-length ceiling
- Back-solve which model to choose

Example:
- ARPU ¥29.9/month, target gross margin 50%
- Ceiling for monthly cost per user: ¥15
- 30 conversations per month average
- Per-call budget: ¥0.5
- On Sonnet at $3 input / $15 output → max 5K input + 1K output per call
- This means the system prompt must use cache (otherwise a single call blows the budget)

**Reverse-solving tells you whether the business model is viable before you pick a model** — instead of discovering after launch that "every order loses money."

### A Token Ledger CFOs Can Actually Read

CFOs can't read "5K input + 1K output." CFOs read this:

```
| Dimension | Value |
|-----|------|
| MAU | 100,000 |
| Avg calls per user per month | 30 |
| Total calls | 3,000,000 |
| Per-call cost (incl. retry) | ¥0.05 |
| Monthly total LLM cost | ¥150,000 |
| Monthly ARR (subscription) | ¥899,400 |
| LLM cost as % of ARR | 16.7% |
| Other costs (server / bandwidth / support) | ¥200,000 |
| Monthly gross profit | ¥549,400 |
| Gross margin | 61% |
| Top-1% spike risk | +¥30,000-50,000 uncertain cost |
```

**The CFO version must include**:
- RMB, not USD
- MAU/month, not token/second
- Explicitly mark retry factor and top-1% spike risk
- Benchmark against traditional SaaS margins (traditional 70-80%; AI products today per ICONIQ 41-52%)

### Business-Model Warning Signals

> **When LLM cost exceeds 30% of ARPU, the model is in trouble.**

Why 30%? Because traditional SaaS still has servers, bandwidth, support, sales, ops, taxes — non-LLM costs alone need 30-40%.

If LLM is 30%, that leaves 60-70% for everything else plus margin. **Margin can't compress into a healthy band.**

> **When LLM cost exceeds 50% of ARPU, the model is dead.**

Examples:
- ARPU ¥29.9, LLM cost ¥18 → LLM 60% → **dead**
- ARPU ¥199, LLM cost ¥30 → LLM 15% → healthy

If your project is in the first bucket today — **fix the business model or cut features now, don't wait for the CFO to scream at you post-launch.**

---

## Part 2 · Engineering Reality

### 5 Common Token Miscounts

#### Miscount 1: Quadratic Context Bloat

20-step agent loop, 1K output per step:
- Intuition: cumulative input = 20K
- Reality: cumulative input = **210K** (quadratic bloat)

Why? Because step N's input contains the accumulation of steps 1 through N-1.
- Step 1 input = 0
- Step 2 input = 1K
- Step 3 input = 2K
- ...
- Step 20 input = 19K
- Total input = 0 + 1 + 2 + ... + 19 = **190K** (plus original 1K ≈ 210K)

If your agent has 20+ steps — **cost is 20× single-step or more**.

#### Miscount 2: Retry Stuffs Error Info Back into Context

Retry isn't "recompute," it's "recompute carrying the error."

Each retry stuffs the last failed output + error message + original input into context — **the more retries, the more expensive**.

3 retries can cost 5-10× the original.

#### Miscount 3: Fallback Cost

PM designs "primary model fails → fall back to backup model."

That means 1 user request triggers **two model calls** — primary + fallback.

If the primary fails 10% of the time, fallback cost = 10% × backup per-call cost.

If the backup is more expensive (e.g., primary on Haiku, fallback to Opus) — **fallback cost can exceed primary cost**.

#### Miscount 4: Cache Miss

Prompt caching sounds beautiful. But **the cache expires in 5-10 minutes**.

If your users behave like "one query every 30 minutes" — **every call is a cache miss**, and caching does nothing.

You need to calculate "actual cache hit rate" against real user behavior. The ProjectDiscovery case: moving dynamic content out of the cacheable prefix raised hit rate from 7% to 74% — **a 6× gap**.

#### Miscount 5: Overlong Input Splits Into Two Calls

The model truncates overlong inputs. Some PMs / engineers design "if it's too long, split into 2 calls."

Translation: 1 user request → **2 model calls + 2× input** → cost doubles.

If your product has a "upload long document" feature — **this is the biggest hidden cost sink**.

---

## Real Bill-Blowout Incidents

### Incident 1: Claude Code recursive loop burns 1.67B tokens in 5 hours

A single Claude Code instance fell into a recursive loop — burning **1.67 billion tokens in 5 hours**.

Single-incident cost: **$16,000-$50,000**.

### Incident 2: Subagent enters 809-step infinite loop

A subagent entered an **809-step infinite tool-call loop** — burning $350 in 3.5 hours.

### Incident 3: Retry loop burns $72,000 overnight

A team misconfigured a retry loop — burning **$72,000 of OpenAI credit overnight**.

### Incident 4: Enterprise "$150K shadow AI crisis"

A software company spent **$150,000 in token charges in a single billing cycle** — post-mortem found zero business output.

### Incident 5: Cursor June 2025 billing blowup

Cursor silently shifted to credit-based billing in June 2025 with no warning:
- Long-time users went from "$20 mental model" to $200-$400 in overages
- Hacker News users posted "$350 in a week" — **monthly cost spiked 10-20×**
- CEO publicly apologized and refunded on July 4

**This is the best public sample for telling your CFO "what if we did the same thing."**

---

## High ARR / Low Margin: Industry Financials

The industry baselines every PM doing token math should know:

### Anthropic's inference cost once exceeded revenue
Per The Information, during Anthropic's aggressive scaling of inference capacity, inference cost briefly exceeded period revenue — **burning faster than earning** (specific margin numbers vary across reports; use the vendor's own financial disclosures).

### OpenAI 2025 revenue ~$13B with large projected net loss (per The Information / Reuters)
Revenue is up, losses are up.

### Industry-joke real data
One AI-coding startup at "$100M ARR / $120M model bill" — **gross margin negative**.

### ICONIQ 2025 survey
AI product average gross margin: 2024 = 41% / 2025 = 45% / 2026 = 52% — still far below traditional SaaS's 70-80%.

### A live sample of Jevons' Paradox
Token unit price fell 99.7%, yet enterprise AI total spend rose to **$37B**.

---

## How to Pitch the Number to the CFO

CFOs don't ask about tokens. They ask about RMB.

**Translation template:**

Wrong: "We use GPT-5.1, input is $1.25/M and output is $10/M."
Right: "Our LLM cost is **¥3.2 per monthly active user**, with ¥X of margin headroom."

Wrong: "Context window is 8K."
Right: "**Single-conversation cap is 5,000 characters** — beyond that gets truncated."

Wrong: "Prompt-caching hit rate is 74%."
Right: "**With caching enabled, monthly bill dropped from ¥450K to ¥45K**."

**The CFO doesn't understand tokens, but they understand ¥3.2, 5,000 characters, and ¥45K.**

---

## QE Lens on the Token Ledger

**8 years in QE has taught me this** —

Any production-grade system design must include a **resource budget** — CPU, memory, bandwidth, disk IO. The core actions of a resource budget are **unit-economics model + monitoring thresholds + automatic circuit-breakers**.

Applied to AI products, tokens are the new "resource":
- Unit-economics model = monthly cost per user
- Monitoring threshold = monthly LLM cost as % of ARR < 30%
- Automatic circuit-breaker = monthly budget hard cap

**The 5 miscounts above all stem from PMs treating tokens as "engineering's problem" instead of "my resource budget."**

A traditional software PM asks "how many servers does this feature need?" — that's table stakes.
An AI-era PM must ask "how many tokens does this capability burn per month?" — that's the new table stakes.

Can't answer this = **not a competent AI PM**.

---

## Action Checklist

#### Action 1: Build a token ledger at every project kickoff
- Use the reverse method, back-solving from ARPU
- Calculate LLM cost as % of ARR
- Warning at > 30%, dead at > 50%

#### Action 2: Stick the 5 miscounts on your desk
- Context accumulation / retry / fallback / cache miss / overlong split
- Run through them every time you do the math

#### Action 3: Cache every system prompt > 1024 tokens immediately
- 1 day of work
- 60%-90% bill reduction

#### Action 4: Use RMB / MAU / card format when presenting to the CFO
- No tokens, no English
- Explicitly mark the top-1% spike risk

---

## Counter-Consensus

- **"Token unit price dropped 99.7% in 3 years; corporate bills tripled. That's not a bug — that's Jevons' Paradox in the AI era, and the first counter-intuitive curve every PM must understand."**
- **"Agents don't crash. They just quietly spend money — a runaway retry loop burns $72K overnight, no alert, no crash, just the CFO @-ing you in the group chat the next morning."**
- **"$100M ARR paired with a $120M model bill — that's the most expensive 'looks sexy' P&L of 2026."**

---

## Closing

This essay covered the token ledger. The next essay is the final one in the Solutions section — **the technical-path decision tree**.

RAG / Prompt / Agent / Fine-tune are not parallel options. They form a prioritized decision tree. **Choosing the wrong path costs far more than choosing the wrong model.**

The next essay gives you a simple decision rhyme: **"Prompt before Agent, RAG before Fine-tune"** + the reverse-applicability conditions for all 4 paths.

See you next essay.

---

## Next Up

**10 · Tech Path Decision Tree — How to Choose Among RAG / Prompt / Agent / Fine-tune**

## Companion Resources

Token ledger calculator (Excel) + 5-miscount self-audit checklist + CFO communication scripts (unlocked for paid readers).

## Feedback / Reader Community

WeChat Official Account 「蔡逸雯」

---

> **Reading the Chinese original?** See [09-token-economics.md](./09-token-economics.md)
> **Part of**: Season 1 · AI PM Workflow Reconstruction · 26 essays
> **Author**: Cai Yiwen (蔡逸雯) · 8 years in QE → AI PM
