# 18 · The Gradual-Rollout Strategy for AI Products — After Traditional A/B Stops Working

> Season 1 《Rebuilding the PM Workflow for the AI Era》· Chapter 18 · Part IV: Delivery
> Estimated length: 5000 words

---

The seventeenth "dismissive blind spot" —

**90% of PMs are still doing AI rollout using "traditional A/B testing"**.

It's not that PMs don't know A/B. It's that most PMs **assume "AI product rollout works the same as traditional feature rollout"** — they roll out a prompt version to 50% of users, and three days later discover P99 latency has tripled — **and that's the kind of thing traditional A/B does not catch**.

By the end of this chapter you will know — **AI product rollout isn't A/B group splitting; it's multi-axis switching across prompt version / model version / parameter version**.

---

## Part 1 · Workflow

### The 3 Axes of AI Rollout

Traditional A/B is single-axis — group A vs group B.

AI product rollout is **multi-axis** — at minimum 3 axes:

#### Axis 1: prompt version
- system prompt changed
- few-shot examples added / removed
- output format changed

#### Axis 2: model version
- switching from GPT-5 to GPT-5.1
- switching from Sonnet to Opus
- switching from Claude to Gemini

#### Axis 3: parameter version
- temperature changed
- max_tokens changed
- top_p changed

**3-axis crossing** means at any time you may be running:
- prompt v3 + model GPT-5.1 + temperature 0.7
- prompt v3 + model GPT-5.1 + temperature 0.5
- prompt v3 + model Sonnet 4.5 + temperature 0.7
- prompt v4 + model GPT-5.1 + temperature 0.7
- ...

Without proper management — **combinatorial explosion**.

### Design Principles for Multi-Axis Rollout

#### Principle 1: change only one axis at a time
- Don't switch models while changing the prompt
- Don't tune temperature while switching models
- Otherwise when something breaks, you can't isolate which variable caused it

#### Principle 2: every change goes through shadow eval
- shadow traffic duplicates a copy to the candidate version
- candidate output goes to logs only, never to the user
- LLM judge compares old vs new

#### Principle 3: every rollout runs regression eval
- the historical case set must not degrade
- prevents "fixed A, broke B"

#### Principle 4: small steps for rollout percentage
- 5% → 20% → 50% → 100%
- observe at least 24 hours at each step

### Rollout Evaluation Metrics

Don't just look at conversion — **look at quality distribution**:

| Dimension | What to watch | Threshold |
|-----------|---------------|-----------|
| Business | conversion / retention / NPS | rollout group ≥ control group |
| Quality | eval pass rate / bad case ratio | rollout group ≥ control group |
| Latency | P50 / P99 | rollout P99 ≤ control × 1.2 |
| Cost | per-call cost / monthly budget | rollout ≤ control × 1.1 |

**The key counter-consensus**: quality distribution must look at the distribution, not just the mean.

A 90% average accuracy hides "5% of cases at <50% accuracy". **That 5% determines user reputation.**

### Rollback When the Rollout Fails

Traditional feature rollout fails → switch back to the old version.

AI product rollout fails → not only switch back to the old version, **but also roll back the eval baseline**.

Why? Because the real traffic captured during the new version's window may have polluted the eval set — what you thought was your "baseline" is no longer the baseline.

**Rollback SOP**:
1. Cut traffic back to old version (< 5 minutes)
2. Tag and isolate the eval data captured during the rollout
3. Re-run historical eval set (verify the baseline hasn't drifted)
4. Postmortem (within 24 hours)

---

## Industry Practices for Multi-Axis Rollout

### Practice 1: Notion AI dual-track eval ⭐

70 engineers, **two eval suites**:
- **regression eval**: prevent regressions
- **frontier eval**: discover which sub-tasks a new model is better at than the old one

Within hours of a new frontier model release, they can pinpoint "this is the case class where switching is worthwhile."

Issue handling speed went from 3 per day to **30 per day** — 10x throughput. (Notion × Braintrust dual-track eval pattern.)

### Practice 2: DoorDash customer-service chatbot simulator

Method:
- Generate multi-turn synthetic conversations from historical transcripts
- Run hundreds of conversations in minutes
- Score with LLM judge

Pre-launch, they **significantly reduced hallucination rate** (from DoorDash engineering blog public case; specific reduction per official figures).

### Practice 3: Shadow traffic — industry-standard implementation

Method:
- Duplicate a copy of each production request to the candidate model
- Candidate output goes to logs only, never returned to the user
- Compare with LLM judge; track token / latency / cost

**Cost**: API spend doubles (set budget alerts).

### Practice 4: Canary 5–10% + auto-block PR

Method:
1. PRs that change prompts auto-run eval; if score < baseline, block merge
2. Canary at **5–10% real traffic**
3. Prompt versions are immutable; keep instant rollback ready
4. Production sampling compared against staging in real time

### Practice 5: Hamel Husain Eval-Driven Workflow

SOP:
1. First look at 100 real traces and do error analysis
2. Cluster failure modes
3. Write eval (not the other way around — don't write eval first and then look for problems)
4. Every prompt change runs full regression

**Hamel's principle**: "**until you stop finding new failure modes**" — Hamel emphasizes "stop when you see no new categories", not "stop after a fixed count".

---

## Part 2 · Engineering Reality

### Shadow Traffic — the Engineering Implementation

Why do AI products need shadow traffic more than traditional products?

Because AI output is a **probability distribution** — looking at the new version's eval pass rate is insufficient; you must see how it performs **on the real traffic distribution**.

Shadow traffic implementation essentials:
- **Asynchronous execution**: don't block the user request
- **Sample, not full duplication**: typically 5-10% traffic shadowed (cost-controllable)
- **Results only to logs**: never returned to user
- **Comparison dimensions**: quality / latency / cost — all three

### Shadow Eval: Evaluating a New Version Without Affecting Users

Shadow eval is the next step beyond shadow traffic — not only logging old-vs-new comparison, **but also running LLM judge to score both versions**.

Concrete flow:
```
1. User request enters the system
2. Main traffic goes to old version (user sees old version output)
3. A copy of the request is asynchronously sent to new version
4. Old output + new output → both go into LLM judge
5. LLM judge scores: which version is better
6. Accumulate 7 days of data → decide whether to cut over
```

**Key**: the LLM judge must first be human-aligned (see Chapter 12 on Eval).

### Regression Eval: Run the Historical Case Set on Every Rollout

Why is regression mandatory?

Because AI systems are **globally coupled** — changing prompt A may worsen performance on B.

**Real case 1: OpenAI GPT-4o sycophancy (2025-04)**

In an attempt to make conversations "friendlier", the training drove the model to agree with harmful decisions (including agreeing with stopping medication).

**Critical failure point**: sycophancy was not added as a blocking item in the release evaluation. **Several testers "felt off", but there was no mechanism for that feedback to halt the release.**

After the fix, OpenAI explicitly documented "behavior issues must be able to block release".

**Real case 2: Gemini image generation over-tune (2024-02)**

To fix "output not diverse enough", they over-tuned to the point of forcing diversity into 1800s American senators and Nazi soldiers, and the model became excessively refusal-prone.

CEO Pichai publicly called it "unacceptable".

### A Real Rollout Disaster: "Single-Axis Looked Fine, Multi-Axis Crossed Broke Everything"

Industry case: **ChatGPT "gibberish incident" (2024-02-20)**

A "UX optimization" release introduced a token-selection bug — the model emitted streams of meaningless repetition (e.g. "a synonym for 'overgrown' is 'overgrown'" 30+ times), interspersed with German and "fantasy language".

**It took about 5 hours to roll back** (OpenAI status page reported as "several hours").

**Lesson**: even a "minor UX optimization" can blow up the model layer; every change must go through shadow eval.

---

## The 4-Phase Rollout Model

```
Phase 1: Internal testing (0% real traffic)
  - 5-10 internal users
  - run core eval set
  - pass → enter Phase 2

Phase 2: Shadow eval (0% user-visible)
  - 5% real traffic duplicated to new version
  - asynchronous execution + LLM judge comparison
  - accumulate 3-7 days of data
  - new version quality ≥ old version → enter Phase 3

Phase 3: Canary rollout (5% user-visible)
  - 5% real traffic sees new version
  - monitor business + quality + latency + cost
  - any metric regresses → immediate rollback
  - pass → enter Phase 4

Phase 4: Staged ramp (20% → 50% → 100%)
  - observe 24 hours per step
  - keep regression eval running throughout
  - after 100%, observe 7 more days before confirming stability
```

The full path takes **2-4 weeks** — that's the responsible rollout cadence for AI products.

---

## QE Lens: AI Rollout = Controlled Experiment

**8 years of software quality engineering perspective** —

Any production-grade system release follows one principle: "**controlled experiment, gradual ramp**".

Traditional software follows canary deployment — 5% → 20% → 50% → 100%.

AI products add 2 dimensions on top of that:
1. **Shadow eval** — pre-release 0% user-visible comparison
2. **Regression eval** — regression testing of old cases at release time

Why does an AI product need 2 more dimensions than traditional software?
- AI output is a probability distribution — point comparison is insufficient
- AI systems are globally coupled — changing A may affect B

The "**4-phase rollout**" is essentially the AI-era canary deployment — with two extra layers: shadow and regression.

---

## Action Checklist

#### Action 1: Your next release must go through the 4-phase model
- Internal testing → Shadow eval → Canary 5% → Staged ramp

#### Action 2: Strictly isolate the 3 axes
- Change only one axis at a time
- Don't change prompt / model / parameters simultaneously

#### Action 3: Every change runs regression eval
- Historical case set must not regress
- PR auto-blocks on regression

#### Action 4: Build the shadow traffic infrastructure
- 5-10% traffic asynchronously duplicated
- LLM judge compares old vs new versions
- Accumulate at least 3-7 days before a decision

---

## Counter-Consensus Lines

- **"Traditional A/B fails in the AI era — green A/B metrics don't mean it's safe to ship. The OpenAI GPT-4o sycophancy episode is the textbook counter-example: A/B all green, full rollback 4 days later."**
- **"Notion's 70 engineers survive on two eval tracks: regression eval prevents regressions, frontier eval finds improvements. Teams running only one of the two either don't dare ship new models, or don't know why the old model went bad."**
- **"Knight Capital lost $440M in 45 minutes — 8 servers, 1 missed update. Doing multi-axis rollout in the AI era is fundamentally about not letting your model version × prompt version × feature flag end up in an '8 servers, 1 missed' state."**

---

## Closing

This chapter covered rollout. The next chapter is the closing piece of the Delivery section — **the Pre-launch Eval Checklist**.

Before launch, the PM must personally run a full pre-launch eval. **All 5 categories — not one missed.**

The next chapter gives you 8 categories of mandatory Eval + minimum bar per category + the DPD chatbot disaster + Air Canada / NYC MyCity and other real-world gap cases.

See you next chapter.

---

> **Companion Resources**: Multi-axis rollout design template + Shadow eval workflow + 4-phase rollout SOP (unlocked for paid subscribers)
> **Next Up**: 19 · Pre-launch Eval Checklist — the round the PM must personally run before launch
> **Feedback / Reader Community: WeChat Official Account 「蔡逸雯」**

---

> **Reading the Chinese original?** See [18-gradient-strategy.md](./18-gradient-strategy.md)
> **Part of**: Season 1 · AI PM Workflow Reconstruction · 26 essays
> **Author**: Cai Yiwen (蔡逸雯) · 8 years in QE → AI PM
