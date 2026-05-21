# 12 · How to Write the Eval Section — The Most Overlooked Chapter in Your PRD

> Season 1 《Rebuilding the PM Workflow for the AI Era》· Chapter 12 · Part Three: PRD (the Hard Goods of this Column)
> Target length: ~5,500 words

---

The eleventh "dismissive blind spot" —

**90% of PMs are still doing AI product evaluation by "eyeballing a few cases."**

It's not that PMs don't want to be rigorous. It's that most PMs **believe "if I personally look at 10 cases and they feel good, then it's good"** — then after launch the user feedback splits in half, and the PM realizes for the first time that the 10 cases they reviewed were all happy paths, and the out-of-distribution samples were never covered at all.

By the end of this chapter you will know — **the Eval section is the soul of any AI product PRD. A PRD without Evals is no PRD at all**.

Hamel Husain put it most sharply: **"Writing good evals is becoming the defining skill for AI PMs."**

---

## Part 1 · Workflow

### The 5 Elements of an Eval Section

#### Element 1: Evaluation Dimensions

Back out from the core capability — what are the core standards by which your AI system's output is considered "good"?

Example: Three eval dimensions for a customer-service agent:
- **Did it resolve the issue?** (state check) — was the ticket closed?
- **Did it finish within 10 turns?** (transcript constraint) — length limit
- **Was the tone appropriate?** (LLM rubric) — polite, professional, empathetic

3-5 dimensions is enough. **Any eval set with more than 5 dimensions will collapse** — you cannot optimize that many objectives simultaneously.

The paradigm Anthropic offers in *Demystifying evals for AI agents*:

> "Combine three kinds of graders: **code-based** (fastest and most stable, but lacks nuance) / **LLM-as-judge** / **human review**."

Don't use one type of grader to cover every dimension.

#### Element 2: Number of Cases

**Anthropic's official recommendation**:

> "**20-50 simple tasks drawn from real failures is a great start.**"

20-50! Not 1,000!

This is counter-consensus — many PMs think "rigorous means accumulating 1,000 cases before shipping." **In reality, 20-50 is enough to start.**

Why? Because early-stage changes have outsized impact, and small samples are enough to surface problems. Only after a few iteration rounds do you scale to 200-500 cases for regression testing.

**SWE-bench Verified provides another counter-consensus data point**:

OpenAI assembled a team of professional engineers plus multi-person cross-review and filtered **500 hand-curated Python samples** out of the full SWE-bench set — those 500 hand-curated examples are **far more useful** than tens of thousands of noisy scraped samples (refer to the official SWE-bench Verified announcement for the exact engineer count and review process).

**Quality > quantity.** 50 human-reviewed cases beat 5,000 GPT-labeled ones.

#### Element 3: The Pass Bar

**Higher is not always better.**

The cost of setting the bar wrong — McDonald's × IBM is the textbook counter-example: **85% accuracy, 1 out of 5 orders needs human bailout**. In fast food, 85% equals 100% disaster — the remaining 15% all happens in front of the customer.

Pass bars must be reverse-derived from business tolerance:
- How many errors can users tolerate?
- How costly is a single error?
- Can a failing case fall back?

If the cost of error is high and there is no fallback → pass bar must be ≥ 99% (finance, healthcare).
If the cost of error is low and there is a fallback → 90% is enough (general customer support).

The essence of the pass bar: **give engineers a clear target**. A vague "good enough" is not a pass bar.

#### Element 4: Labeling Method

Who labels?

| Labeler | Use case | Pros / Cons |
|---|---|---|
| **PM themselves** | First 50-100 cases at start | Accurate but slow |
| **Ops / Support** | Continuous labeling of user-feedback cases | Medium accuracy + medium speed |
| **Domain experts** (lawyers / doctors / finance) | Specialized domains | Extremely accurate, extremely expensive |
| **User feedback** (thumbs up / down) | Large-scale collection after launch | Noisy but high volume |
| **LLM-as-judge** | Automated scaling | Fast but biased |

**Hamel Husain's field advice**: hand-label 100-200 cases first → train the LLM judge to align with humans → then scale.

**Do not start with LLM-as-judge** — its bias is untrustworthy until it is aligned.

#### Element 5: Eval Cadence

Three triggers:
- **Every commit**: run cheap code-based graders (near-zero cost)
- **Every release**: run the full eval set (including LLM-as-judge)
- **Every week**: run the historical regression set (to prevent "fixed A, broke B")

If your eval set **runs only once before launch** — **99% chance something goes wrong**.

**Notion AI's dual-track eval practice** (Braintrust case):
- **Regression eval** prevents regression
- **Frontier eval** discovers which sub-tasks a new model beats the old one on

70 engineers, issue-handling speed lifted from 3 per day to 30 — **all because evals run frequently.**

---

## Hamel's Three-Tier Eval Framework (the most-cited in the industry)

L1 → L2 → L3, escalating in scope:

### L1: Unit Tests
Break the LLM into features × scenarios, write assertion-style tests.

Example:
```python
def test_intent_classification():
    response = model("I want a refund")
    assert response.intent == "refund_request"
    assert response.confidence > 0.8
```

Cheapest, fastest, **runs on every commit in CI**.

### L2: Human & Model Eval
Log traces → human labeling → align LLM judge with humans → large-scale evaluation.

**Key counter-consensus**: use **binary (good/bad) scoring** instead of a 5-point scale.

Hamel verbatim: "more granular ratings is more onerous to manage than binary ratings."

A 5-point scale sounds more refined, but in practice **inter-rater agreement is poor**. Binary is crude but stable.

### L3: A/B Testing
Online metrics are the safety net to validate whether offline metrics are a good proxy.

Versions passing L1+L2 ship to 5-10% of traffic for A/B, and you observe real business metrics (conversion, retention, NPS) for improvement.

**Hamel's field data**: on his projects, **60-80% of dev time goes into error analysis and evaluation.**

It's not prompt-writing that consumes the most time — it's looking at traces + labeling cases + writing evals.

---

## A Complete Eval Section Template

```markdown
## 5. Eval Set Design

### 5.1 Evaluation Dimensions (3-5)
1. [Dimension 1]: [code-based / LLM-as-judge / human]
2. [Dimension 2]: ...
3. [Dimension 3]: ...

### 5.2 Case Count and Coverage
- Starter: 20-50 real-failure cases
- Steady state: 50-200 cases per dimension
- Coverage: 60% normal + 30% edge + 10% adversarial

### 5.3 Pass Bar
- [Dimension 1] pass rate ≥ X%
- [Dimension 2] pass rate ≥ Y%
- Launch gate: [critical dimension] ≥ Z%

### 5.4 Labeling Method
- Starter phase: PM + Ops + 1 domain expert
- Scaling phase: train LLM judge aligned with humans
- Steady phase: user feedback + sampled human re-review

### 5.5 Eval Cadence
- Every commit: L1 unit tests (< 1 min)
- Every release: L2 full eval set (< 1 hour)
- Weekly: regression eval (prevent regression)
- Monthly: frontier eval (evaluate new models)
```

Fill in this template and your PRD now has a soul.

---

## Part 2 · Engineering Reality

### The Hard Part of Evals Isn't "Writing" — It's "Coverage"

Writing an eval is easy — find 50 cases and label them.

**The hard part is covering OOD samples, adversarial samples, and real-traffic skew.**

#### Difficulty 1: Out-of-Distribution Samples (OOD)

Your eval set comes from historical user behavior. **Future user behavior may be completely different.**

Example: an education AI product's eval set is 100 math problems. After launch, users ask it about history, language, and philosophy — the eval set never covered it.

Response: regularly refresh the eval set with real-traffic data (monthly / quarterly).

#### Difficulty 2: Adversarial Samples

Malicious users will try to break your AI — prompt injection, jailbreaks, deliberate inducement.

Example: a user instructs the chatbot to "agree with anything I say" — the Chevy Tahoe case is exactly this kind of adversarial failure.

Response: the eval set must include 10% "adversarial cases" — purposefully designed inducing inputs.

#### Difficulty 3: Real-Traffic Skew

The distribution of cases in your eval set doesn't match real-traffic distribution.

Example: the eval set is 50% refunds + 50% queries. Real traffic is 90% queries + 10% refunds. **A 90% eval pass rate does not mean 90% user satisfaction.**

Response: the case-frequency distribution of the eval set should match real traffic. Or compute a weighted overall pass rate.

### Drift Between Eval and Production Is the Norm

Eval pass bar ≠ production stability. This is a reality AI PMs must accept.

**Real-world gap cases**:

#### DPD Chatbot (Jan 2024)
The UK delivery company's chatbot — pre-launch eval passed, **but no regression was run after the post-launch update**.

UK musician Ashley Beauchamp coaxed it into producing profanity and a poem declaring "DPD is the world's worst courier," generating millions of impressions in a single tweet.

#### NYC MyCity Bot (2024)
**Eval did not cover "compliance correctness"** — the bot gave businesses illegal advice without being caught.

#### Air Canada Moffatt Case (Feb 2024)
**Eval did not cover "policy consistency"** — the bot fabricated a non-existent policy and the court ruled compensation.

**The common thread across all three**: the eval passed, but the failing dimension wasn't covered by the eval dimensions.

**Response**: every time a real bad case appears, immediately add it to the eval set. **The eval set is alive, not a one-time deliverable.**

---

## Evolution of Evals: From Static Case Sets to Dynamic Sampling of Real Traffic

The most advanced eval practice isn't "write a fixed case set" — it's "dynamically sample real traffic."

Concretely:
- Every 1,000 production calls, randomly sample 1
- Auto-add to eval set
- Weekly human re-review of the most recent 100
- New failure modes discovered → write new evaluators → add to CI

**This "living eval" is the only way to keep up with model upgrades + user behavior changes.**

Notion's 70 engineers use exactly this approach to lift issue-handling speed from 3 per day to **30**.

---

## Mature Industry Eval Tools

### OpenAI Evals Repo
GitHub: https://github.com/openai/evals

Structure:
- `evals/registry/evals/*.yaml` (YAML-defined evals)
- `evals/registry/data/*.jsonl` (JSONL datasets, one case per line)
- Two CLIs: `oaieval` (run one) + `oaievalset` (run a group)

**Takeaway for PMs**: use **JSONL not CSV/Excel** for eval data — version-controllable, Diff-friendly, lives alongside Git.

### Inspect AI (the UK AISI official framework)
URL: https://inspect.aisi.org.uk/

Design philosophy: four-layer abstraction **Dataset → Task → Solver → Scorer**. Sandbox execution (Docker built in) + web log viewer + VS Code plugin.

Already adopted by US CAISI / METR / Apollo Research.

**Takeaway for PMs**: treat evals as software engineering — with a data layer, execution layer, scoring layer, and visualization layer.

### Anthropic's Statistical Approach
URL: https://www.anthropic.com/research/statistical-approach-to-model-evals

**Key counter-consensus**: eval results **must come with confidence intervals**.

0.85 vs 0.87 may not be statistically significant on small samples. Learn to report evals as "based on X samples, 95% CI is ±Y."

---

## QE Lens: Evals Are the Infrastructure of AI Products

**Speaking from 8 years in software quality engineering** —

Any mature ML project treats evals as infrastructure — fraud detection, churn prediction, demand forecasting all have holdout test sets + cross-validation + production monitoring as three pillars. **This is foundational for ML engineers.**

The LLM scene lost this discipline — only because prompt engineering looks so "light" that people assumed they could skip evaluation and ship directly.

**Counter-consensus punchline**: Hamel Husain cuts to the truth in one line — "EDD is not a new invention. It's the old ML rule the LLM crowd forgot. Nobody cares about a fraud model that isn't accurate — but the LLM product world somehow tolerates it."

When a PM writes an Eval section into a PRD, it's not innovation — it's **bringing the foundational discipline of ML engineering back into the PM workflow**.

---

## Action Checklist

#### Action 1: Your next PRD must fill an Eval section following the 5-element template
- Dimensions / case count / pass bar / labeling method / cadence
- Missing any one of the five → not a qualified PRD

#### Action 2: Start from 20-50 real failure cases
- Don't accumulate 1,000 cases first
- Anthropic's official recommendation

#### Action 3: Every bad case goes straight into the eval set
- Evals are alive, not one-time
- Review newly added cases monthly

#### Action 4: Manage evals using Hamel's three-tier framework
- L1 unit tests → run in CI every commit
- L2 full eval → run every release
- L3 A/B test → run after launch

---

## Counter-Consensus Punchlines

- **"The moat of an AI product isn't data, isn't the model — it's a high-quality eval set."**
- **"Anthropic recommends starting with 20-50 real-failure cases. Teams that wait to accumulate 5,000 before launch usually use exactly zero of them."**
- **"SWE-bench Verified teaches us: 500 hand-reviewed cases beat 50,000 scraped, noisy ones."**

---

## Closing

This chapter covered how to write evals. The next one is the most philosophical chapter in the PRD section — **Eval-Driven Development (EDD)**.

If Chapter 12 is the "operational layer" — how to write an Eval section — **Chapter 13 is the "philosophical layer" — how to drive the entire dev process with evals**.

The next chapter will tell you: traditional is "write code, then test." AI products invert it — **write evals first, then code**.

This isn't a change of testing method — it's a change of development philosophy.

See you next chapter.

---

## Next Up
**13 · Eval-Driven Development — Letting the eval set drive the entire dev process.**

## Companion Resources
**Eval section template + 5-element self-check + case library (including real eval-set examples from SWE-bench / Anthropic / OpenAI)** (paid subscribers unlock).

## Feedback / Reader Community
WeChat Official Account 「蔡逸雯」.

---

> *This article was originally published in Chinese on the WeChat Official Account 「蔡逸雯」 and translated into English by the author. If discrepancies arise, the Chinese original prevails.*
