# 14 · Writing Bad Case Grading and Degradation Strategy into the PRD

> Season 1 《Rebuilding the PM Workflow for the AI Era》· Chapter 14 · Part Three: PRD (the Hard Goods of this Column)
> Target length: ~5,500 words

---

The thirteenth "dismissive blind spot" —

**90% of PMs still treat bad cases as a "deal-with-it-after-launch" thing.**

It's not that PMs don't take it seriously. It's that most PMs **believe "I can't think of bad cases right now, I'll see them once we ship"** — then on Day 3 after launch the cases erupt, and the PM discovers for the first time that "catastrophic cases" and "acceptable cases" require drastically different handling, **and the PRD designed for none of it.**

By the end of this chapter you will know — **the 4-tier bad-case grading + corresponding degradation strategy must be decided during the PRD phase, not patched after launch.**

---

## Part 1 · Workflow

### The 4 Tiers of Bad Case Grading

#### Tier 1: Acceptable

**Criteria**:
- User perception < 5% (the vast majority won't notice)
- Business loss negligible (no impact on conversion, retention, compliance)
- No fix needed, log only

Examples:
- The AI agent's reply is a bit verbose
- A summary misses a minor piece of info
- A translation isn't fully idiomatic but conveys the meaning

**Strategy**: do nothing, only log in traces. Ops review monthly.

#### Tier 2: Alert Required

**Criteria**:
- User perception 5%-30%
- Quantifiable business loss (conversion drop, NPS drop)
- Triggers monitoring alerts but does not block the flow

Examples:
- AI agent accuracy on a certain question type drops from 90% to 75%
- Summary generation p99 latency exceeds 5s
- A model's refusal rate suddenly triples on a given day

**Strategy**:
- Real-time dashboard monitoring
- Alert thresholds (e.g., accuracy < 80% / latency > 3s)
- PM steps in to diagnose within 1-2 hours
- Doesn't affect users, but ops must see it

#### Tier 3: Block Required

**Criteria**:
- User perception 30%-80%
- Large business loss (user churn / surge in complaints)
- Auto-fallback to rules or humans

Examples:
- AI output format corrupted (JSON parse failure)
- Tool call failure (API timeout / auth failure)
- Model refusal rate > 20% (mass refusal of things it should answer)

**Strategy**:
- Auto-fallback path triggered
- Users see rule-based fallback or human takeover
- Users don't see the raw failure
- PM steps in within 30 minutes

#### Tier 4: Catastrophic

**Criteria**:
- Legal / compliance / PR risk
- Large-scale reputational incident (one mistake might hit headlines)
- Immediate circuit-break + human intervention

Examples:
- Air Canada chatbot–type (fabricating a non-existent policy, court-ordered compensation)
- NYC MyCity–type (advising businesses to break the law, media exposure)
- Chevy Tahoe–type (prompt-injected into selling for $1)
- Involving sensitive groups / politics / violence / sexual content

**Strategy**:
- Immediate circuit break (feature offline)
- Switch to backup model / full human takeover
- Sev-1 response: PM + Legal + PR engaged simultaneously
- Postmortem within 24 hours

### The 4-Tier Decision Matrix

Score along two axes: **user perception × business loss**:

```
              user perception → high
              │
              │ Tier 3     Tier 4
              │ (block)    (catastrophic)
              │ auto-fb    circuit-break + PR
              │
business loss ├─────────────────────
              │
              │ Tier 1     Tier 2
              │ (accept)   (alert)
              │ log only   dashboard
              │
              └─────────────────────
                              user perception → high
```

Every bad case in the PRD must be labeled with a tier + corresponding strategy.

### The Core Requirement of Microsoft RAI Standard v2

Industry-authoritative backing: **Microsoft Responsible AI Standard v2** requires every use case to establish a "**frequency × severity**" metric table.

These two axes are the industry standard:
- **Frequency**: low / medium / high
- **Severity**: low / medium / high / catastrophic

**PM takeaway**: the two core dimensions of bad-case monitoring are always frequency × severity — not "looks good or not."

### Bad Case Section Template for the PRD

```markdown
## 6. Bad Case Grading and Degradation Strategy

### 6.1 Bad Case Type Inventory
| Type | Description | Est. frequency | Severity | Tier |
|---|---|---|---|---|
| Hallucination | Fabricates non-existent facts | Medium (5-10%) | Medium-High | Tier 3 |
| Refusal | Refuses legitimate request | Low (< 2%) | Medium | Tier 2 |
| Format corruption | JSON parse failure | Low (< 1%) | High | Tier 3 |
| Over-privileged op | Triggers unauthorized tool call | Very low | Catastrophic | Tier 4 |
| Bias | Discriminatory output | Very low | Catastrophic | Tier 4 |
| ... | ... | ... | ... | ... |

### 6.2 Degradation Strategy per Tier
- Tier 1: log only, no action
- Tier 2: dashboard alert + PM diagnosis within 1-2h
- Tier 3: auto-fallback to [rules / backup model / human]
- Tier 4: circuit-break + human takeover + 24h postmortem

### 6.3 Trigger Conditions and Response Times
| Tier | Metric | Threshold | Response time |
|---|---|---|---|
| 2 | Accuracy | < 80% | 1-2h |
| 3 | Failure rate | > 5% | 30min |
| 4 | Catastrophic event | Any 1 occurrence | Immediate |
```

Fill this template and PRD Chapter 6 is done.

---

## Three Industry Grading Standards Side by Side

### Microsoft Azure AI Content Safety: 4 Severity Levels

**Grading**: four harm categories (hate / sexual / violence / self-harm) × four severity levels (Safe / Low / Medium / High). Safe is always labeled but never blocked.

Use case: content moderation / safety filtering.

### Anthropic ASL (AI Safety Levels)

**Grading**: four capability tiers (ASL-1 → ASL-4, analogous to biosafety levels).
- Three policy layers (Universal Usage Standards / High-Risk Use Cases / Additional Guidelines)

**PM takeaway**: grade by "capability threshold" rather than "incident severity" — predict which capabilities will cause disasters, set red lines in advance.

### OpenAI Model Spec: Prohibited / Restricted / Sensitive

**Grading**:
- **Prohibited** (CSAM only, absolute zero tolerance)
- **Restricted** (e.g., weapons, biochemical)
- **Sensitive** (contextually legal adult content, violence portrayals)

**PM takeaway**: distinguish "must never happen, period" from "depends on context" — the former needs hard rules, the latter relies on model judgment.

---

## Part 2 · Engineering Reality

### The Engineering Reality of Degradation Strategy

#### Reality 1: Trigger conditions must be quantifiable

Don't write "degrade when AI fails" — too fuzzy. Write "trigger degradation when accuracy < 80% for 5 consecutive minutes" — quantifiable, monitorable, automatable.

#### Reality 2: Degradation paths must be canaried

Main path fails → switch to backup path — sounds reasonable, but **a backup path that hasn't been canaried may be worse than the main path.**

**Response**: every degradation path must be pre-validated via shadow eval (shadow-traffic evaluation) to confirm it's actually more stable.

#### Reality 3: UX compensation

What users see after degradation cannot be "system busy, try later" — that punishes the user.

Proactively tell them: "**we've temporarily switched to a human agent, expect a reply within 5 minutes**" — give them an expectation.

Best case: users have no idea a degradation occurred (rule-based fallback is seamless).

### "Degrading to Rules" Isn't Failure — It's Being Responsible

Many PMs see "degrading to rules" as a failure of the AI project.

Wrong. **Degradation is a sign of AI product maturity.**

Why? Because an AI product is fundamentally a **probabilistic system** — it can never reach 100%. Degradation isn't because the AI can't do it; it's because, in certain scenarios, **AI should yield to rules.**

**Industry best practice**: a16z's 2025 survey of 100 enterprise CIOs found **37% running 5+ models simultaneously**, with a "high-risk paths use rules, low-risk paths use LLMs" dual-track design now the default architecture.

"AI-assist + rule-fallback" isn't a step back — it's **the default form of a production-grade AI product.**

### A Real Case: Why a Seemingly Harmless Bad Case Was Tagged "Catastrophic"

Industry case: the Air Canada bot fabricated a refund policy, **single judgment only CAD 650.88** — but the court ruled "the chatbot is not an independent legal entity, it's part of the website."

**CAD 650.88 isn't the point** — the point is that after this precedent, **the legal risk of chatbots across global airlines was kicked wide open**. Air Canada's "small payout" actually manufactured massive uncertainty for the entire industry.

**Takeaway for PMs**: judging a bad case's tier can't be based only on "single-instance cost" — it must include "precedent effect." One small payout turning into an industry precedent = catastrophic.

---

## OpenAI GPT-4o Sycophancy: A Textbook Case

The classic "fixed A, broke B" case.

**Timeline (April 2025)**:
- 2025-04-25: OpenAI rolled out a full GPT-4o update (to make conversations "friendlier")
- A/B test metrics all looked good (short-term user feedback positive)
- After launch, users found the model had turned into a yes-bot:
  - Endorsed terrible startup ideas like "sticking a pole in poop"
  - Endorsed decisions to stop medication
  - Endorsed dangerous plans
- 2025-04-29: OpenAI fully rolled back

**OpenAI's own postmortem cited the root cause**:

> "Sycophancy was not gated as a blocking criterion in the release evaluation."

A few testers "felt something was off" but there was no mechanism to stop the release on their input.

The fix explicitly added "**behavior issues must be able to block release**" to policy.

**This is the strongest argument for why a PRD must have a Bad Case grading chapter** — even a top-tier company like OpenAI got burned for not having one.

---

## QE Lens: Bad Case Grading = FMEA at the PRD Phase

**From 8 years in software quality engineering** —

The 4-tier bad-case grading is essentially **FMEA (Failure Mode and Effects Analysis)** applied at the PRD phase. The core of FMEA is "**before you build anything, list every possible failure mode + assess each one's impact + design mitigation strategies.**"

In traditional software engineering, FMEA was used mainly in hardware reliability / nuclear / aerospace — because those fields have extremely high failure costs.

**AI products bring "high cost of failure" into software** — a single chatbot fabricating policy can lead to a court ruling + a precedent. This means doing FMEA at the PRD phase has moved from "nice to have" to "mandatory action."

No FMEA = missing a PRD chapter = guaranteed pain post-launch.

---

## Action Checklist

#### Action 1: Your next PRD must have Chapter 6 — Bad Case Grading
- List 5-10 possible bad-case types
- Tag each with frequency × severity
- Classify into the 4 tiers

#### Action 2: Each tier paired with an explicit degradation strategy
- Tier 1: log only
- Tier 2: dashboard alert
- Tier 3: auto-fallback
- Tier 4: circuit-break + human takeover

#### Action 3: Quantify trigger conditions
- Don't write "degrade on AI failure"
- Write "trigger degradation when accuracy < 80% for 5 consecutive minutes"

#### Action 4: Self-check using the GPT-4o sycophancy case
- Does your PRD have a "behavior issues must be able to block release" mechanism?
- No → add it immediately

---

## Counter-Consensus Punchlines

- **"Bad cases aren't binary — happens or doesn't. Microsoft uses 4 categories × 4 levels, OpenAI uses 3 layers, Anthropic uses ASL 4 tiers. Any PM who treats bad cases as a single bucket will get schooled by reality, by tier."**
- **"OpenAI admitted the root cause of the GPT-4o blowup: sycophancy was not made a blocking gate at release. So if your product doesn't have a 'behavior risk one-vote veto,' you'll eventually have your April 29th — a full rollback day."**
- **"The minimum set of evaluation dimensions is frequency × severity. That's the first line of Microsoft RAI Standard, not an optional add-on."**

---

## Closing

This chapter covered PRD Chapter 6: Bad Cases. The next is the final chapter of the PRD section — **Cost Budget and Ceilings.**

The first question a CFO asks when first looking at an AI product PRD is "how much money does this thing burn per month?" — most PMs only learn to write the cost section after that day.

The next chapter gives you a 3-layer structure + a Token-to-RMB formula + ceiling circuit-break design + a full postmortem of the Cursor June 2025 blowup.

After reading it, you'll be able to talk costs with the CFO. **This is the most underestimated hard skill of an AI PM.**

See you next chapter.

---

## Next Up
**15 · Cost Budget and Ceilings — An AI Product PRD that Finance Can Understand.**

## Companion Resources
**Bad case grading template + degradation strategy library + GPT-4o postmortem teardown** (paid subscribers unlock).

## Feedback / Reader Community
WeChat Official Account 「蔡逸雯」.

---

> **Reading the Chinese original?** See [14-bad-case-grading.md](./14-bad-case-grading.md)
> **Part of**: Season 1 · AI PM Workflow Reconstruction · 26 essays
> **Author**: Cai Yiwen (蔡逸雯) · 8 years in QE → AI PM
