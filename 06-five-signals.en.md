# 06 · Requirements Review SOP — 5-Signal Scorecard + 5 Disguised Phrases Decoded

> Season 1 · AI PM Workflow Reconstruction · Essay #6 · Part 1: Requirements
> Estimated length: 2000 words

---

The fifth dismissive blind spot —

**90% of PMs treat the "review meeting" as "stakeholder pitches the requirement + I nod along."**

The stakeholder says: "You get the gist of this requirement, right? Just build something first, we'll figure out the standards as we go."

The dismissive PM agrees — and starts building. Three months later they discover what got built is not what the stakeholder wanted.
The PM who recognizes the trap pushes back: **"Hold on. Before we even enter this review meeting, please fill out this 5-Signal Scorecard. Score too low — no review today."**

After reading this essay you'll know — **Essay #4 covered the strategic judgment of "should we build it." This essay hands you the toolkit you actually use inside the review meeting** —

- The 5-Signal Scorecard (stakeholder fills it out before pitching)
- 5 disguised phrases + counter-question templates
- A review meeting rhythm SOP

**Use the two together — your win rate for rejecting fake requirements goes from 30% to 80%.**

---

## Part 1: Workflow

### The 5-Signal Scorecard (designed for 10-minute review meetings)

The scorecard is for the stakeholder to fill out *before* the review — **no scorecard, no review**. This single move flips the PM from "being chased by stakeholders" to "stakeholders proactively coming to align."

| Signal | One-Line Definition | Passing Bar | Engineering Disaster If Missing |
|------|-----------|---------|------------------|
| 1. Are IO clear? | One sentence each for input and output | Engineers can start coding immediately after reading | Fuzzy IO → 3 months of finger-pointing |
| 2. Evaluation metrics | 3 quantifiable metrics | Pick any: accuracy / recall / latency / cost | Fuzzy eval → never able to close out |
| 3. Error tolerance | Cost of a single error | See Essay #4, Dimension 2 | Zero tolerance → guaranteed crash on launch |
| 4. Ground truth | Where do the gold answers come from | See Essay #4, Dimension 3 | No GT → permanent hallucination |
| 5. Sustained investment | Who owns data iteration post-launch | Stakeholder has 12-month budget | No investment → back to square one in 3 months |

Note: Signals 3 and 4 were unpacked in Essay #4. They're used here only as scoring dimensions, not re-explained.

### Scoring Rules (stakeholder self-fills)

Each signal scores 0 / 1 / 2:
- **0**: Completely unanswerable
- **1**: Answerable but vague
- **2**: Clear, specific, executable

Total thresholds:
- **≥ 8**: Cleared for review, engineers can start
- **5-7**: Requirement needs more signal completion before review
- **< 5**: Sent back immediately — stakeholder needs to think harder

**90% of fake requirements score below 5** — this is the PM's *objective basis* for rejection, not "the PM subjectively doesn't want to do it."

### Signal 1 Deep Dive: When Are IO Actually Clear

Signal 1 is **the most underrated** of the five — readers assume "IO is easy," but 80% of stakeholder IO descriptions are fuzzy.

**Passing examples**:
- "Input: user-uploaded contract PDF (≤ 10MB). Output: JSON with 20 risk points (fields: risk type / severity / cited clause)"
- "Input: customer's WeChat conversation log (last 50 messages). Output: 3-5 reply suggestions (each ≤ 50 characters)"
- "Input: product title + description + image URL (up to 3). Output: category tags (L1 + L2) and price prediction range"

**Failing examples**:
- "Input… you know, when users use our product the AI helps out a bit"
- "Output? Something that makes the user experience better"
- "We just want an intelligent customer service bot" (no IO at all)

**Key test**: Can the engineer start coding **without asking a single question**? Yes = pass. No = fuzzy.

### Signal 5 Deep Dive: What Counts as Real Sustained Investment

Signal 5 is **the most commonly missing** of the five — stakeholders only think "let's ship it first" when proposing, never "who maintains it post-launch."

**Passing examples**:
- "Our operations team labels 100 bad cases per week, dedicated owner"
- "Monthly retrospective meeting, led by stakeholder, engineering follows up"
- "12-month data iteration budget already planned, ¥X"

**Failing examples**:
- "Just launch it, we'll deal with problems later"
- "This project has budget through year-end, next year depends on ROI"
- "Your AI team handles maintenance — business side only files requirements"

**Counter-consensus truth**: A stakeholder dumping a one-shot requirement on the AI team and expecting "launch delivery" — **that requirement is essentially doomed**. One core finding from the MIT NANDA report: **external procurement + co-build mode has a 67% success rate; pure internal builds only 1/3** — the gap is not technology, it's **whether the stakeholder sustains investment**.

If Signal 5 has no answer — **even if the other 4 signals pass, the PM should recommend delaying project kickoff**.

---

## Part 2: Engineering Reality

### The 5 Disguised Phrases + PM Counter-Question Templates

Stakeholders won't directly say "I haven't thought this through." They use disguised phrases. **The PM must be able to recognize them + counter on the spot**.

Print this table and tape it to your desk — you can use it in the review meeting **immediately**.

#### Disguise 1: "Good enough is fine" → masking missing evaluation criteria

> **Stakeholder**: "This AI customer service reply just needs to be good enough — usable is fine."
>
> **PM counter**: "How good is 'good enough'? Give me a specific number — for instance, accuracy ≥ 85% is 'good', ≥ 70% is 'good enough.' That number determines which model we use and how many tokens we burn per month."

#### Disguise 2: "Let's just build it first" → masking missing ground truth

> **Stakeholder**: "Build a demo first, we'll define the standards as we go."
>
> **PM counter**: "Once the demo is built, how do we judge whether it's right or wrong? Who labels? How many labels are enough? If we don't answer these 3 questions first, we can iterate on the demo for a month and you still won't be satisfied — because no one knows what 'right' looks like."

#### Disguise 3: "Show me a few cases and I'll know" → masking missing systematic evaluation

> **Stakeholder**: "Show me 10 cases and I'll know if it works."
>
> **PM counter**: "Out of 100 cases, 95 are right and 5 are wrong — how do you judge if that's good or bad? Looking at 10 cases and seeing 0 errors might just mean those 10 were the easy ones. We have to see the overall distribution — that's why the PRD must have an eval section."

#### Disguise 4: "Your AI team handles maintenance" → masking missing sustained investment

> **Stakeholder**: "After launch, your AI team handles maintenance. The business side only files requirements."
>
> **PM counter**: "Who owns bad case labeling in 3 months? Where does the labeling budget come from? How much time per week is your operations team willing to spend reviewing bad cases? If these 3 questions go unanswered, **this project is highly likely abandoned in 3 months** — industry data shows pure internal builds only hit 1/3 success rate."

#### Disguise 5: "Just have humans backstop the errors" → masking missing fallback design

> **Stakeholder**: "When the AI makes mistakes, just have customer service backstop it."
>
> **PM counter**: "Where's the fallback entry point? Who reviews? Response SLA? Whose team budget covers the fallback cost? If the AI error rate is 10% and we have 1000 conversations a day = 100 need human backstop — can your CS team handle that? Fallback isn't a post-hoc patch, it's something the PRD must design upfront."

**Memorize these 5 counters** — 70% of stakeholder AI requirements will trigger one of them.

### Review Meeting SOP (10-minute model)

Convert the review meeting from "stakeholder talks for 30 minutes + PM nods" into "10-min scorecard + 5-min counter-questioning + 5-min conclusion."

#### Phase 1: Send the scorecard 1 week ahead (stakeholder self-fills)
- Scorecard template (5 signals + one-line definitions)
- Stakeholder completes and returns it
- PM reviews scores first + flags key counter-question points

#### Phase 2: 10 minutes before review, PM also scores it independently
- Don't be biased by the stakeholder's scores
- Flag signals where the two scores disagree

#### Phase 3: 10-minute review meeting
- **First 3 min**: PM puts the scorecard on the table, confirms both scores
- **Middle 5 min**: Counter-question on disagreements / disguised phrases
- **Final 2 min**: Decision — kickoff / complete signals / rejected

#### Phase 4: Written meeting minutes within 24 hours
- Scorecard + counter-question record + decision
- Sent to stakeholder + CC'd to boss
- **Creates a written paper trail** — critical evidence in later project reviews

### Reverse Play: Make "Completing Signals" Standard Process

Many PMs are afraid of stakeholders saying "why are you being so difficult."

Here's the reverse play — **make "completing signals" the standard requirements review process, not a PM's unilateral move**.

Concrete approach:

```
Stakeholder files requirement for the first time:
  → PM doesn't review yet, first sends the "5-Signal Requirements Review Scorecard"
  → Stakeholder self-fills against the 5 signals
  → One week later, the review starts based on the scorecard

Benefits of the scorecard:
  → Stakeholder thinks it through before coming back — efficiency rises
  → Review meeting is no longer "PM interrogating stakeholder," it's "both sides checking against the scorecard"
  → Stakeholder has ownership, downstream cooperation is higher
  → When the boss sees low-scoring requirements, they'll proactively pause them — PM doesn't have to reject alone
```

Once this flow runs smoothly, **the quality of stakeholder requirements rises exponentially** — 3 months later your review meetings will be 3× more efficient.

---

## A Real Counter-Consensus Truth from the Review Floor

**A pattern that recurs across the industry** —

Stakeholder says: "This requirement is simple, just build a demo to show the boss." Missing Signal 1 (fuzzy IO) + Signal 2 (vague eval) + Signal 4 (no ground truth) — **scorecard total: 4 (passing only 2 signals at 1 point each)**.

By this essay's SOP, this requirement is **rejected outright**, no review.

But 90% of PMs will accept it — because they don't want to offend the stakeholder, because the boss is already pushing, because "let's build it first and fix it later."

The result:
- 3 weeks later the demo goes to the boss, who says "doesn't feel that intelligent"
- PM tweaks the prompt, demos again 2 weeks later
- Boss says "still not quite right"
- PM tweaks prompt again, 1 month later the stakeholder says "maybe let's not build it after all"

**3 months burned, zero output** — this isn't an isolated case, it's the standard portrait of the 95% of failed projects in MIT NANDA's data.

The scorecard's true value — **it gives the PM an objective basis to reject in the review meeting**, not "the PM subjectively doesn't want to do it."

---

## QE Lens: 5-Signal Scorecard = PRD-Level FMEA

**8 years in Quality Engineering, I've seen far too many "looks reasonable, actually unbuildable" requirements** — on AI products this phenomenon is just amplified 10×.

Any complex system, before kickoff, should run an **FMEA (Failure Mode and Effects Analysis)** — "**before building, list all possible failure modes + assess the impact of each + design mitigation strategies.**"

The 5-Signal Scorecard is essentially **PRD-level FMEA** —
- Signal 1 (fuzzy IO) = system IO failure mode
- Signal 2 (vague eval) = acceptance failure mode
- Signal 3 (zero tolerance) = exception handling failure mode (see Essay #4 + #14)
- Signal 4 (no ground truth) = quality measurement failure mode (see Essay #4 + #12)
- Signal 5 (no sustained investment) = evolution failure mode

**Each missing signal = a class of failure modes with no mitigation strategy — project failure probability rises exponentially.**

Essay #14 on Bad Case Tiering will go deeper on applying FMEA thinking at the PRD stage.

---

## Your Action Checklist

#### Action 1: Make the "5-Signal Requirements Review Scorecard" a standard template
- 5-row table + 0/1/2 scoring
- Send the scorecard when stakeholders file requirements
- Pass rate < 60% → no review

#### Action 2: Tape the "5 disguised phrases + counter-questions" to your desk
- Counter immediately when you hear a disguised phrase
- Train your "anti-disguise" reflex

#### Action 3: Run the 10-minute SOP in review meetings
- 3 min scorecard + 5 min counter-questions + 2 min decision
- Written minutes within 24h

#### Action 4: Monthly stat: "% of requirements filtered out by the 5 signals"
- A high-quality review meeting funnel should be ≥ 30%
- Funnel < 10% means you're being dragged along by stakeholders

---

## Counter-Consensus Quotes

- **"The moment the stakeholder says 'good enough is fine,' your AI project is already buried."**
- **"Ground truth is the foundation of an AI project — not every project deserves a foundation."**
- **"To judge whether a stakeholder is genuine about AI — see if they'll show up weekly to read the evals report."**

---

## Closing Thoughts

This essay closes out the Requirements arc (Essays 3-6).

By now you should have a complete new workflow for requirements discovery:

- Essay #3 — Requirement sources are no longer user interviews, they're 4 real sources
- Essay #4 — 3-dimension framework decides "should we build it" (strategic layer)
- Essay #5 — 4 Agent boundary types decide "can we build it" (technical layer)
- Essay #6 — 5-Signal Scorecard + Review SOP (review meeting tools)

**Essay #4 sets direction (whether to kick off), Essay #6 sets execution (how to reject in review) — use them together for highest win rate.**

The Requirements arc closes. We enter Part 2 — **Solutions**.

Next essay we start on the PM drawing diagrams — **why function flow diagrams mislead on AI products, and how to draw capability flow diagrams**.

This one will change your solution review approval rate.

See you in the next essay.

---

> **Companion Resources for this essay**: 5-Signal Scorecard Excel template + 5 disguised phrases quick reference + 10-minute Review Meeting SOP (paid readers unlock)
> **Next up**: 07 · The Paradigm Shift in AI Product Solution Design — From Function Flow to Capability Flow
> **Feedback / Reader Community**: WeChat Official Account 「蔡逸雯」

---

> **Reading the Chinese original?** See [06-five-signals.md](./06-five-signals.md)
> **Part of**: Season 1 · AI PM Workflow Reconstruction · 26 essays
> **Author**: Cai Yiwen (蔡逸雯) · 8 years in QE → AI PM
