# 22 · Courage to Downgrade — When You Must Fall Back to Rules: A PM's Checklist

> Season 1 *AI-Era PM Workflow Reconstruction* · Article 22 · Part V Operations
> Estimated length: ~2,000 words

---

The twenty-first dismissive blind spot —

**90% of PMs treat "downgrading to rules" as the failure of an AI project.**

It's not that PMs want to push through. It's that most PMs **assume "downgrade = I didn't do my job"** — so they push for three more months, until a production incident forces a rollback, **at a cost 10x higher than a proactive downgrade**.

By the end of this piece you'll know — **when these 4 scenarios appear, a PM must have the courage to downgrade the AI capability to rules.** "Downgrade" is not failure. It is responsibility.

Article 14 covered Bad Case triage at the PRD stage (pre-incident defense). **This article is about post-launch downgrade decisions (during and after the incident).**

---

## Part 1 · Workflow

### The 4 Scenarios Where You Must Downgrade

#### Scenario 1: High Risk (Finance, Healthcare)

**Signature**: A single error can cause major financial or health damage.

**Decision criteria**:
- Cost of one error > value of 1,000 correct answers
- The cost of being wrong is settlements / medical incidents / legal liability

**Typical scenarios**:
- Automated financial trading decisions
- Medical diagnosis / medication recommendation
- Automatic insurance claim approval

**Downgrade design**:
- AI provides the recommendation, **a human makes the final decision**
- AI flags risk points, **rules + human serve as the safety net**
- Critical nodes must be human-in-the-loop

#### Scenario 2: Strong Compliance (Data, Legal)

**Signature**: Touches regulatory requirements / legal liability / data privacy.

**Decision criteria**:
- Regulators explicitly prohibit or restrict AI decisioning
- Touches sensitive personal information
- Touches contracts or legal terms

**Typical scenarios**:
- Legal consultation / contract review
- Hiring / employment decisions
- Credit approval / personal credit reporting

**Downgrade design**:
- AI assists with analysis, **lawyer / HR / loan officer reviews**
- Decision authority does not sit with the AI
- Keep a complete audit log

**Industry precedent**:
- **Illinois state law (2025)**: legislation explicitly **prohibits** AI from drafting mental-health treatment plans or interacting directly with patients; AI is only allowed in administrative support roles.
- **Texas TRAIGA (effective 2026-01)**: requires physicians to provide written disclosure when AI is used in diagnosis.

**This is regulator-mandated downgrade.**

#### Scenario 3: Hard Low-Latency Requirement (Real-Time Interaction)

**Signature**: Response latency must be < 1 second; LLM inference simply can't keep up.

**Decision criteria**:
- The business scenario demands real-time response (games / livestream / high-frequency trading)
- P99 latency must be < 500ms

**Typical scenarios**:
- In-game AI (real-time reaction)
- Real-time livestream interaction
- High-frequency trading decisions

**Downgrade design**:
- Replace real-time LLM inference with **rules + cache**
- Pre-compute offline + look up in real time
- Use AI only in asynchronous scenarios

#### Scenario 4: Long-Tail Loss of Control (80% Good, 20% Catastrophic)

**Signature**: Strong performance on common cases, terrible performance on the long tail — **and the long-tail failures are visible to users**.

**Decision criteria**:
- Top 80% cases: accuracy ≥ 95%
- Long-tail 20% cases: accuracy < 60%
- Long-tail failures will trigger a PR incident

**Typical scenarios**:
- Customer service auto-reply (multilingual / dialects / special requests)
- Recommendation systems (edge content)
- Content moderation (boundary cases)

**Downgrade design**:
- Run AI on the head, route long-tail cases through rules + humans
- Have the AI proactively detect "long-tail case" and hand off to a human
- Do not require AI to cover 100%

**Industry precedent**: **McDonald's × IBM drive-thru AI ordering** — 100+ store pilot over 2 years, social media flooded with "wrong order added." In 2024-06 the IBM partnership was terminated, with all locations rolled back to human ordering.

The lesson: **85% accuracy with 1 in 5 orders needing a human catch — in fast food, 85% equals 100% rollover.**

### Design Principles for a Downgrade Plan

Downgrade is not "cutting the AI" — it is "**AI assist + rule-based fallback**."

The concrete pattern:

```
Original: user request → AI makes the decision → output
        ↓
Downgraded:
        user request → AI recommends → rule / human review → output
                            ↑              ↑
                            AI returns N candidates
                                            ↑
                                Human or rule picks 1
                                or human rejects and regenerates
```

**The key**: the AI is still in the loop, but the AI is no longer the final decision-maker.

### Industry Best Practice for Downgrade Strategy

**a16z 2025 survey of 100 enterprise CIOs**:

**37% are running 5+ models in parallel**, with a "**high-risk path on rules, low-risk path on the LLM**" dual-track design as the default architecture.

**This means "AI assist + rule fallback" is not a step backward — it is the default shape of a production-grade AI product.**

---

## Scripts: How to Explain a Downgrade to Your Boss or Business Owner

The boss whose project is being downgraded will push back. That's normal.

Do not say "AI doesn't work" — say "**this is the responsible design.**"

### Script 1: Finance Scenario

> "Zhang, this financial decisioning scenario has to be downgraded. You may have heard of the Air Canada precedent — the bot invented a bereavement policy that didn't exist, and the BC tribunal ordered the company to pay CAD 650.88 (about USD 480). **The money isn't the point — the point is that after this ruling, chatbot legal exposure was opened up for every airline globally.**
>
> If we push pure autonomous AI decisioning into this scenario, **the cost of a single error is way more than that fine**. Downgrading to AI assist + human review keeps **risk inside the acceptable envelope**, and business efficiency still climbs 50%.
>
> Stepping back now saves 10x the money. Pushing through pays 10x the money."

### Script 2: Healthcare / Mental Health Scenario

> "Li, Illinois already legislated in 2025 to prohibit AI from creating mental-health treatment plans, and Texas TRAIGA — effective 2026-01 — requires physicians to disclose AI use in diagnosis in writing. **Regulators are telling us: this class of decision must have a human in the loop.**
>
> We're downgrading early — not because AI doesn't work, but because **the compliance red line is right there**. Waiting for regulators to force a retrofit costs 10x more than designing it correctly now."

### Script 3: Long-Tail Loss-of-Control Scenario

> "Chen, McDonald's spent 2 years across 100 stores piloting AI ordering — **and ultimately terminated the partnership, reverting to human order takers**. The reason: 85% accuracy with 1 in 5 orders needing a human safety net — in fast food, 85% equals 100% rollover.
>
> Our scenario is more complex than fast food; the long-tail failure rate will be higher. **Klarna's CEO publicly admitted before IPO that they cut too many people — that wasn't backing down, it was governance transparency, and the valuation actually held up.**
>
> Proactively downgrading is making the product solid, not retreating."

After this kind of conversation, 70% of business owners will agree.

---

## Part 2 · Engineering Reality

### The Engineering Basis for "Courage"

Behind each downgrade type is a clear engineering reality:

#### Scenario 1 (Finance / Healthcare)
- Cost of one error >> value of 1,000 correct answers
- LLM failure rate will never reach 0
- The mathematical expected value is negative

#### Scenario 2 (Compliance)
- Regulators have legislated, or are about to
- Legal liability cannot be transferred to the AI
- The company has to carry the final responsibility

#### Scenario 3 (Real Time)
- LLM inference latency has physical limits
- Even the fastest models have P99 > 500ms
- Real-time scenarios must use cache or rules

#### Scenario 4 (Long Tail)
- LLM weakness on long-tail distributions is structural
- Training data inherently under-represents the tail
- Fixing the tail introduces new bad cases (see Article 21)

### The Cost of "Just Push the AI Anyway"

Many bosses think "ship the AI first, deal with errors later" — **this is the most expensive mistake.**

| Dimension | Cost of pushing AI | Cost of downgrading to rules |
|---|---|---|
| Short term | Looks like saving labor | Still need human safety net |
| Mid term | Customer churn / complaint spikes | Stable customer experience |
| Long term | PR incidents / legal settlements | Smooth scale-up |
| Aggregate | **10× more expensive** | Baseline cost |

Concrete arithmetic:
- Monthly cost of pushing AI customer service: ¥10K (LLM calls)
- Post-incident handling: ¥100K (PR + complaints + churn)
- Monthly cost of the downgraded path: ¥30K (AI + human)

Three months in — pushing AI totals ¥130K, downgrade totals ¥90K. **The downgrade is actually cheaper.**

---

## 4 Real Industry Downgrade Cases

### Case 1: Finance — Klarna (2024 → 2025)

- **2024**: CEO Siemiatkowski announced that AI handled the workload equivalent of roughly 700 customer service agents (achieved via hiring freeze, not a single layoff event).
- **2025**: Publicly admitted "AI lacks empathy and can't handle complex problems," **started rehiring and moving to a hybrid model**.
- **The downgrade evidence**: Proactively raising this before IPO is itself a textbook downgrade script.

### Case 2: Legal Liability — Air Canada (2024-02)

- The BC tribunal ruled that Air Canada was liable for the chatbot's "hallucination" as negligent misrepresentation.
- Awarded **CAD 650.88** (≈ USD 480).
- The airline's defense — "the correct policy was in the linked page" — was rejected: **"the AI said it wrong" is not a valid legal shield.**
- After the ruling, the industry collectively downgraded toward "AI answer + strict validation against the rules page + critical clauses must hand off to a human."

### Case 3: Food Service — McDonald's × IBM (2021 → 2024-07)

- 100+ stores piloted AI ordering for 3 years.
- Social media flooded with "wrong items added / cross-lane orders / cannot remove items."
- 2024-06: IBM partnership terminated; all locations rolled back to human ordering.
- **Three years of piloting were ultimately voted down by customers.**

### Case 4: Healthcare / Mental Health — Regulator-Mandated Downgrade (2025)

- **Illinois state law (2025)**: legislatively prohibits AI from creating mental-health treatment plans.
- **Texas TRAIGA (effective 2026-01)**: requires physicians to disclose AI use in diagnosis in writing.
- **This is regulator-mandated downgrade.**

---

## QE Lens: Downgrading = Knowing When to Stop

**From the perspective of 8 years in software quality engineering** —

The hardest thing in quality engineering is not "do better" — it's "**know when to stop.**"

Any over-optimization eventually destabilizes the system —
- Chasing 100% test coverage → exponential maintenance cost
- Chasing 100ms performance → code complexity explosion
- Chasing 100% AI accuracy → long tail goes out of control

"**Downgrade to rules**" is fundamentally "**knowing when to stop chasing 100% AI coverage**" — and that is the foundational judgment of a quality engineer.

PMs who view downgrade as failure = PMs who threw the QE lens away.
PMs who view downgrade as "the default shape of a mature product" = PMs who actually understand the nature of probabilistic systems.

---

## Action Checklist

#### Action 1: Print the 4 downgrade scenarios and stick them on your monitor
- High risk / strong compliance / low latency / long-tail loss of control
- Check every new feature against the list before kickoff

#### Action 2: Stand up a "downgrade decision process"
- Weekly bad-case review
- Any scenario triggered → immediately evaluate downgrade
- Don't drag it out

#### Action 3: Memorize the 3 downgrade scripts
- Finance / healthcare / long-tail loss of control
- Have them ready when the boss bangs the table

#### Action 4: Use Klarna as your reference
- Proactive downgrade vs reactive rollback
- The proactive cost is far smaller than the reactive one

---

## Counter-Consensus Lines

- **"Downgrade isn't failure — pushing through is."**
- **"Before launch it's gambling. After launch it's responsibility."**
- **"Whether AI *can* ship is a technical question. Whether AI *should* ship is a common-sense question."**

---

## Closing

This article closes out the operations section (Articles 20-22).

By here you should have a complete operational toolkit for an AI product:
- Article 20 — the 4 categories of AI-specific monitoring metrics
- Article 21 — the 5-step Bad Case management loop
- Article 22 — the courage-to-downgrade checklist (4 scenarios)

The next article opens Part VI — **Collaboration.**

In the AI era, team language has to change wholesale. Article 23 starts with the new collaborative language between PMs and engineers — **how much Prompt and Eval should a PM actually understand?**

**Half-understanding is more dangerous than not understanding** — that's the core counter-consensus of the collaboration section.

See you next time.

---

> **Companion Resources**: 4-scenario downgrade decision checklist + downgrade explanation script templates + 4 real case comparisons (unlocked for paid readers).
> **Next Up**: 23 · The new collaborative language with engineers — how much Prompt and Eval should a PM understand?
> **Feedback / Reader Community**: WeChat Official Account 「蔡逸雯」

---

> **Reading the Chinese original?** See [22-courage-to-downgrade.md](./22-courage-to-downgrade.md)
> **Part of**: Season 1 · AI PM Workflow Reconstruction · 26 essays
> **Author**: Cai Yiwen (蔡逸雯) · 8 years in QE → AI PM
