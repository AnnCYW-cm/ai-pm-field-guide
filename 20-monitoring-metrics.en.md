# 20 · AI-Product Monitoring Metrics — Beyond the Traditional Funnel, What Else to Watch

> Season 1 *PM Workflow Reconstruction in the AI Era* · Article 20 · Part V Operations
> Estimated word count: 5000

---

The 19th "dismissive blind spot"—

**90% of PMs still monitor AI products with the traditional funnel.**

It's not that PMs can't read metrics. It's that most PMs **assume "AI products and traditional products both watch DAU / retention / conversion"**—then a week into launch all metrics are green, day 8 the user reputation craters—**because not one of the 4 AI-specific metric categories was being monitored.**

By the end of this article you'll know—**AI-product monitoring must include 4 AI-specific metric categories on top of the traditional funnel.**

---

## Part 1 · Workflow

### The 4 AI-Specific Metric Categories

#### Metric 1: Quality Distribution (Not Average, the Distribution)

**Why average isn't enough**?

Example. A customer-service AI's overall satisfaction is 4.2/5—looks fine.
But break it out by distribution:
- 30% give 5
- 40% give 4
- 20% give 3
- **10% give 1**

That 10% giving 1 **will go bash you**. The average buries them.

**How to monitor**:
- Don't monitor the mean
- Monitor distribution (use histogram)
- Focus on the "low-score tail" share

**Industry best practice**:
- **Datadog LLM Observability** splits into three distribution dimensions: factuality / toxicity / relevance
- **Braintrust** leads with "eval-driven development with CI/CD gates"—embedding quality distribution into release gates

#### Metric 2: Bad Case Ratio

**How to classify and count**:

Tag by failure mode (don't collapse to a single "error rate"):
- hallucination: X%
- refusal: X%
- format error: X%
- off-topic: X%
- safety violation: X%

**Arize's standard practice**: cut bad cases into 4-5 classes, tag each separately, count separately.

Why not collapse? Because each class has a different fix path:
- hallucination → fix RAG / add grounding
- refusal → fix prompt / adjust safety filter
- format error → use structured output
- off-topic → adjust system prompt boundary
- safety violation → add content filter

**Collapsing into one "error rate" = losing diagnostic information.**

#### Metric 3: Degradation Trigger Rate

**Why monitor**: The degradation paths you designed (Article 14 Bad Case Tiering) — how often are they actually triggered?

Healthy range:
- Tier 2 (alert): < 10/day
- Tier 3 (block): < 5/day
- Tier 4 (catastrophic): **< 1/month**

Abnormal:
- Tier 3 trigger rate suddenly > 50/day → the model may be regressing
- Tier 4 trigger rate > 0 → run a postmortem immediately

**Helicone's approach**: one-line proxy integration natively exposes three degradation request flags—"rate-limited / rerouted / fallback to another provider"—so you can view each share separately.

#### Metric 4: Cost-per-Active-User

**Why monitor**: See Articles 9 / 15.

- Monthly cost per user (the most important financial metric)
- Top 1% user spend share
- Monthly LLM cost as a fraction of ARR

**a16z 2025 enterprise survey**: enterprise LLM annual spend has grown from $4.5M to $7M average—**CFOs are now demanding explainable marginal cost per active user.**

**Traceloop approach**: use OpenTelemetry to inject user_id into traces, automatically correlating to token usage—"**which user's which action triggered which spend**".

### Alert Thresholds Per Metric Category (Starting-Point Reference Values)

| Metric | Warning Threshold | Critical Threshold |
|--------|------------------|-------------------|
| Quality distribution low-score tail (≤ 2 share) | > 15% | > 30% |
| Hallucination rate | > 5% | > 10% |
| Refusal rate | > 10% | > 20% |
| Tier 3 degradation trigger rate | > 20/day | > 100/day |
| Tier 4 degradation trigger rate | > 0 | any |
| Cost-per-active-user vs. budget | > 80% | > 100% |
| P99 latency vs. SLA | > 80% | > 100% |
| User-initiated human-handoff rate | > 15% | > 30% |

⚠️ **The thresholds above are starting-point anchor values for a team, not an industry standard.** Reasonable thresholds for different business scenarios (customer service / coding / creative / medical) can differ 5-10× — **calibrate to your own business**. The numbers in this column exist only to break the "no baseline" state.

If a threshold trips—the dashboard alerts immediately, the PM gets involved within 1-2 hours.

### Minimum Monitoring Dashboard Set

#### Boss-facing version (5 items)
1. MAU trend
2. User satisfaction (NPS or 5-star average)
3. Monthly LLM cost / ARR ratio
4. Tier 4 bad case count (must = 0)
5. Business core metric (conversion / retention)

#### Team-facing version (15+ items)
- The 5 above
- Quality distribution histogram
- Bad case count split by type
- Trigger rates of each degradation tier
- Cost-per-user distribution
- P50 / P99 latency
- Top 1% user spend
- Refusal rate / Hallucination rate
- User-initiated human-handoff rate
- ...

### Metric Review Cadence

**Daily report** (auto-sent):
- Today's data for the 4 AI-specific metric categories
- Highlight any metric above warning threshold
- Anomalous bad case examples (5-10)

**Weekly report** (PM writes):
- Weekly trend across the 4 categories
- New bad case types
- This week's release actions vs. metric changes correlation

**Monthly report** (PM + business owner together):
- Monthly trend across the 4 categories
- Is LLM cost / ARR healthy?
- Next month's iteration direction

---

## Part 2 · Engineering Reality

### The "Delayed Exposure" Problem in Monitoring

**AI-product problems often take 2-7 days to surface.**

Why? Because:
- Bad cases concentrate on long-tail users — collection takes time
- Users average 3-5 days from problem to feedback
- Model quality degradation is gradual, not a cliff
- Monitoring statistics need sample size

**Anthropic's own postmortem** (2025):

For "seemingly reasonable" optimizations to cut latency, cut verbosity, change caching—**HTTP 200, latency normal, dashboard all green**—but actual output had regressed.

**Key failure point**: ~**2 weeks** of delay between user feedback and eval coverage—this is precisely the standard window of "AI delayed exposure" (industry-wide 2-7 days).

### Why "Average" Is Useless for AI Products

Example.

An AI customer-service product's overall satisfaction is 4.2/5.

But if you look at the distribution:
- 70% give 5 (happy path normal)
- 25% give 3-4 (minor issues, usable)
- **5% give 1 (utterly broken)**

Who is that 5%? Typically:
- Edge-case users (special needs)
- High-value customers (high expectations)
- Public figures / KOLs (loud voices)

**This 5% determines user reputation**—they'll go bash you on Weibo, Jike, Xiaohongshu.

The 4.2 average looks great—**the product is already on the verge of collapse.**

### Industry Monitoring Failure Cases

#### Case 1: Google AI Overviews Glue Pizza (2024-05)

Zero infrastructure anomalies—**but "put glue on your pizza" and "eat one rock a day" became internet memes within 24 hours**—failure happened at the content layer, not the infra layer.

Infra was monitored, content quality was not.

#### Case 2: DPD Chatbot (2024-01)

After system update the AI was "all green"; UK musician Ashley Beauchamp **coaxed it into swearing and writing poetry about "DPD is the world's worst courier"**, with a single tweet pulling millions of impressions on X before it was forcibly taken offline.

System stability was monitored; resistance to adversarial input was not.

---

## AI Monitoring SaaS Tools

There are mature industry tools—PMs don't need to build from scratch:

### Helicone
- One-line proxy integration
- Native support for cost / latency / failure monitoring

### LangSmith
- LangChain official
- Suited for RAG / Agent debugging

### Arize
- Enterprise-grade AI observability
- Most granular bad case classification

### Braintrust
- Full eval-driven development
- CI/CD integration

**Selection guidance**:
- Early (< 100K calls/month): Helicone (cheap and simple)
- Mid (100K-10M calls/month): LangSmith / Braintrust
- Large (> 10M calls/month): Arize Enterprise

---

## QE Lens: AI Monitoring = Observability for a Probabilistic System

**Eight years in software QE talking—**

Traditional software monitoring centers on **observability**—the logs + metrics + traces triad.

AI products **add one more category on top**—**distributional observability**.

- Traditional: monitor "is the system responding, how fast" (log + metric)
- AI: monitor "where is the response distribution sitting, how much in the low tail" (distribution + histogram)

The essence of "**average hides the low tail**" is—**using deterministic metrics to monitor a probabilistic system inevitably misses critical failure signals**.

The PM must learn to "look at the distribution, not the mean"—this is the fundamental move of AI-era monitoring.

---

## Action Checklist

#### Action 1: Your product monitoring must include the 4 AI-specific categories
- Quality distribution / Bad case ratio / Degradation trigger rate / Cost-per-user
- Any one missing → monitoring is non-compliant

#### Action 2: All metrics—look at distribution, not mean
- Use histograms
- Focus on the low-score tail

#### Action 3: Bad cases — classify and count
- hallucination / refusal / format / off-topic / safety
- Monitor each of the 5 separately; never collapse

#### Action 4: Three-layer cadence — daily / weekly / monthly
- Daily auto-sent
- Weekly written by PM
- Monthly by PM + business owner together

---

## Counter-Consensus Lines

- **"AI products' 200 OK is genuinely OK, but your users are already screaming."**
- **"A dashboard all green doesn't mean the product is healthy—it just means your monitoring is still stuck in the web era."**
- **"Generic eval is a placebo; bad case classification is the stethoscope."**

---

## Closing

This article covered monitoring metrics. The next covers—**Bad Case Management**.

After monitoring discovers a bad case, what do you do? A traditional bug is "fix it and you're done"—**an AI bad case is "fix it and you might make it worse"**.

The next article covers the 5-step Bad Case Management + real cases of "fixed A, broke B" (GPT-4o sycophancy + Gemini image over-tune) + the prioritization framework.

See you in the next one.

---

## Next Up

> **Next**: 21 · Bad Case Management — The Mindset Shift from "Fixing Bugs" to "Tuning a System"

## Companion Resources

> **Article companion assets**: AI Product Monitoring Dashboard template + 4-category alert threshold reference + tool comparison (paid subscriber unlock)
> **Feedback / Reader Community**: WeChat Official Account 「蔡逸雯」

---

> **Reading the Chinese original?** See [20-monitoring-metrics.md](./20-monitoring-metrics.md)
> **Part of**: Season 1 · AI PM Workflow Reconstruction · 26 essays
> **Author**: Cai Yiwen (蔡逸雯) · 8 years in QE → AI PM
