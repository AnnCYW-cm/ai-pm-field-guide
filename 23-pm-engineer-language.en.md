# 23 · The New Collaborative Language with Engineers — 4 High-Frequency Scripts + the PM's Minimal Trace Set

> Season 1 *AI-Era PM Workflow Reconstruction* · Article 23 · Part VI Collaboration
> Estimated length: ~2,200 words

---

The twenty-second dismissive blind spot —

**90% of PMs are still talking to engineers about AI requirements in the language of "button → page jump."**

It's not that PMs refuse to learn new vocabulary. It's that most PMs **assume "the PM doesn't need to understand prompts or eval — that's the engineer's job"** — and the result is that at every requirement review the engineer has to go back and rework the spec three times — **because the PM doesn't understand where the collaboration boundary sits, so the requirements end up either "AI can't do that" or "AI absolutely could, but the PM didn't think of it."**

By the end of this piece you'll know — **a PM doesn't need to master prompt syntax, but they must speak the right language in 4 high-frequency collaboration scenarios**:

- Requirement review
- Eval result disagreement
- Launch GO / NO-GO
- Production Bad Case emergency

And — they must know which experiments the PM should run themselves, which the engineer runs, and the **3 accident modes where half-understanding is more dangerous than no understanding**.

Finally, the piece you've been hearing referenced all season but never explicitly defined — **the PM's minimal trace-reading set.**

---

## Part 1 · Workflow

### 4 High-Frequency Collaboration Scripts

This section is the ultimate tool — **review meeting / eval disagreement / canary decision / urgent bad case** — with a "right vs wrong" script pair for each. Memorize and use.

#### Scenario 1: Requirement Review

**❌ Old-PM wrong version**:
> "Can you build me an intelligent assistant that helps users write copy?"

Engineer reaction: dark face. "Intelligent assistant" is unbounded / "writing copy" has no standard / "user" is unspecified → **3 rounds of rework minimum.**

**✅ New-PM right version**:
> "I want a marketing copy generator. **Input is [product name + 3 selling points + target audience]; output is 3 Xiaohongshu-style captions (each ≤ 100 characters + 1 hashtag).**
>
> I have 50 eval cases prepared (already shared on Feishu). **Pass rate ≥ 85% is the launch gate.**
>
> P99 latency ≤ 5 seconds. **Cost per call ≤ ¥0.3.**
>
> I've defined 4 Bad Case severity levels: Level 4 (generates non-compliant content) must be blocked 100%."

Engineer reaction: a 3-minute conversation is enough to confirm feasibility + a rough timeline.

**Core**: the PM speaks in **business standards** (input/output / pass rate / latency / cost / bad case levels) — not prompt / model / parameters. **That's the engineer's job.**

#### Scenario 2: Eval Result Disagreement

**❌ Old-PM wrong version**:
> "Eval pass rate is 92%, we can ship." (calling the shot off a single number)

**✅ New-PM right version**:
> "Eval pass rate 92% — **but I need to see the distribution.**
>
> Which categories does the failing 8% land in? I need to know:
> 1. **Which sub-scenario is the failure concentrated in?** (e.g., 60% accuracy for marketing copy in 'B2B SaaS', 99% in 'C-end beauty')
> 2. **Severity distribution of the failures** (proportion at Level 3+ above 1%?)
> 3. **Does it cover the top 20% highest-frequency user scenarios?**
>
> If failures are concentrated in niche scenarios → ship + canary.
> If failures are concentrated in core scenarios → **don't ship**, fix prompt / RAG / fine-tune first."

Engineer reaction: the feeling of being respected — the PM is discussing eval distribution in the same language I use, not throwing "92% pass rate" over the wall.

#### Scenario 3: Launch GO / NO-GO

**❌ Old-PM wrong version**:
> "Boss is pushing, ship today."

**✅ New-PM right version** (against the 5-category pre-launch eval checklist from Article 19):
> "We walk through the 5 pre-launch eval categories:
>
> ✅ Category 1 core cases: pass rate 92% (passes)
> ✅ Category 2 performance: P50 1.2s / P99 4.8s (passes)
> ⚠️ Category 3 cost: ¥0.45 per call (50% over the ¥0.3 budget)
> ❓ Category 4 adversarial: red-team eval not yet run
> ❌ Category 5 regression: 7% degradation on historical cases (over the 5% threshold)
>
> **Category 4 not run + Category 5 regressed = NO-GO.**
>
> I'll handle the boss — once I show him the cost of OpenAI's full GPT-4o rollback on 4-29 over sycophancy, he'll agree to a 3-day delay."

Engineer reaction: relief — finally a PM who absorbs the pressure from the boss for me.

#### Scenario 4: Production Bad Case Emergency

**❌ Old-PM wrong version**:
> "This case errored, quick, change the prompt to fix it." (see Article 21 — fix A, break B)

**✅ New-PM right version**:
> "We hit a production bad case — I'll start by reading the trace to classify it:
>
> - hallucination (fabricated facts)? → add RAG grounding, don't change the prompt
> - refusal (refused when it should have answered)? → tune the safety filter
> - format error (JSON parse failure)? → structured output
> - off-topic (drifted off-task)? → tighten the system prompt boundary
> - safety violation (non-compliant content)? → add a content filter
>
> **Classify first, then decide which layer to fix.** After the fix, run regression eval — historical case degradation > 5% = the fix failed.
>
> If it's a Level 4 bad case (PR risk) — **trigger the downgrade to rules immediately**, don't wait for the fix."

Engineer reaction: at last the PM treats bad cases as 5 distinct problem classes, instead of throwing "fix the prompt" over the wall.

### Which Experiments the PM Runs vs Which the Engineer Runs — Boundary Map

| Experiment | PM runs | Engineer runs | Joint |
|---|---|---|---|
| Evaluate "can this requirement be done" | ✅ (Claude Code prototype) | | |
| Write the system prompt | | ✅ | |
| Write eval cases (business standard) | ✅ | | |
| Write LLM-judge prompt | | | ✅ (PM defines the standard, engineer writes) |
| Run batch eval | | ✅ | |
| Read traces (business lens) | ✅ | | |
| Read traces (technical lens, prompt tuning) | | ✅ | |
| Handle bad cases (classify + decide which layer to fix) | | | ✅ |
| Canary decision (business impact) | ✅ | | |
| Canary technical configuration | | ✅ | |
| Pre-launch eval (Category 1 + business side of 4) | ✅ | | |
| Pre-launch eval (Category 2 perf + 3 cost + 5 regression) | | ✅ | |
| Cost case for the CFO | ✅ | | |
| Cost optimization (caching / batching / model choice) | | ✅ | |

**Core boundary**: PM runs **business-related work + Claude Code prototypes**; engineer runs **technical implementation + batch eval + prompt engineering.**

Draw the boundary clearly — **collaboration friction drops from 80% to 20%.**

---

## Part 2 · Engineering Reality

### The PM's Minimal Trace-Reading Set (Spelled Out for the First Time)

All season I've said "the PM reads 20-50 traces every day" — but what does "reading traces" actually mean? Here's the minimal set.

#### Tools
- **Helicone** (the simplest, one-line proxy install)
- **LangSmith** (LangChain official)
- **Braintrust** (eval + trace in one)
- **Arize** (enterprise grade)

If your company hasn't plugged in any of these — **you can still get a feel by using ChatGPT's built-in conversation export.** Build the instinct first, then push the company to deploy a dashboard.

#### The 5 Fields a PM Must Watch on Every Trace

| Field | What to look at | Instinct to build |
|---|---|---|
| `input` | Raw user input | Is this a real business scenario or an edge case? |
| `system_prompt` | The active prompt | Does the prompt boundary cover the user scenario? |
| `output` | The AI's final output | Accurate? Complete? Right format? |
| `latency` | Time-to-first-token + total time | Will the user perceive this as slow? |
| `cost` | Tokens used per call | If a single user calls 100x in a day, do we blow up? |

#### The PM's "30-Second Judgment Method" for a Trace

After looking at a trace for 30 seconds, answer 3 questions:

1. **Will the user be satisfied with this result?** (subjective 0-5 score)
2. **If not — which failure mode is it?** (hallucination / refusal / format / off-topic / safety)
3. **Is this an isolated case or a repeating pattern?** (see Article 21 — bad case contagion)

Judgment in 30 seconds — note it down → accumulate 20-30 of the same type → take it to engineering for a fix conversation.

**Core**: PMs reading traces is not "decoding technical logs" — it's "training the alignment instinct between business intent and AI output."

### The 3 Accident Modes of the Half-Understanding PM

A **"fully ignorant"** PM gets a safety net from engineering. A **"half-understanding"** PM gives confident bad orders — that's the most dangerous case.

#### Accident 1: "ChatGPT can do it, why can't we?"

PM sees a ChatGPT demo doing something, demands their product do the same.

Engineer explains: "ChatGPT is using RAG + tool use + reasoning" — PM thinks the engineer is making excuses.

**3 weeks after launch** — turns out our RAG has no data, no tool use, no reasoning. **Everything gets torn up and rebuilt.**

**Root cause**: the PM half-understands the demo but not the infrastructure behind the demo.

**Avoidance**: every time a PM sees any AI demo, ask first — "**what infrastructure (RAG / tool / reasoning) did ChatGPT call here? Do we have it? If not, what do we build first?**"

#### Accident 2: "Just change the prompt, we're fine."

A bad case appears — PM's first instinct: change the prompt.

Engineer keeps explaining: "changing the prompt will affect other cases" — PM thinks engineering is stalling.

**The prompt change goes through** — 5 other scenarios regress (see Article 21 — fix A, break B).

**Root cause**: PM half-understands prompts as "instructions" rather than "system-level configuration."

**Avoidance**: classify the bad case first (5 classes) → decide which layer to fix (see Article 21's 5 steps). The prompt is the **last** option, not the first.

#### Accident 3: "Eval pass rate is 95%, we can ship."

PM sees the eval dashboard showing "95% pass" — calls the launch.

After launch, it blows up — because:
- The failing 5% are **core cases**
- That 5% of cases hits 30% of users
- Mean was watched, distribution wasn't

**Root cause**: PM half-understands eval as "a score," doesn't look at distribution.

**Avoidance**: always look at distribution, never just the mean — use the Scenario 2 script with the engineer.

### What a PM Must Understand vs Must Not

| Must understand | Don't need to understand |
|---|---|
| The 4 high-frequency collaboration scripts | The specifics of prompt writing (engineer's job) |
| 5-field trace + 30-second judgment | Eval framework implementation (promptfoo / DeepEval code) |
| Bad case 5-class taxonomy | Model training theory |
| 4-class downgrade strategy framework | RAG vector retrieval algorithms |
| 4 categories of AI monitoring | Model inference optimization |
| 5-category pre-launch checklist | LLM internal attention mechanisms |
| 5-number boss report | Tokenizer implementation details |

**Core**: a PM should understand "the concepts the collaboration scenarios require," not "the details of the engineering implementation."

---

## Industry Consensus on the PM Role Shift

### Consensus 1: PMs must be able to run Claude Code prototypes themselves

See Article 17 — this is the PM's "prerequisite homework" before the 4 collaboration scenarios.

### Consensus 2: PMs must read traces every day

See "minimal trace set" above — this is the "instinct training" of the collaboration.

### Consensus 3: PMs must have "engineering sense"

What is engineering sense? Knowing:
- Roughly how long this will take
- Roughly how much it will cost
- What risks it introduces
- Which things AI fundamentally cannot do (physical limits)

A PM without engineering sense = a PM the AI era washes out.

---

## QE Lens: PM-Engineer Collaboration = a Shared Language for System Boundaries

**From the perspective of 8 years in software quality engineering** —

The core method of quality engineering is **FMEA** (Failure Mode and Effects Analysis).

FMEA requires **business and engineering to discuss in a shared language**:
- Which failure modes can occur
- How large the impact of each is
- Which are acceptable (let them happen, but catch them)
- Which are unacceptable (must block)

**An AI product's PM-engineer collaboration is essentially a joint FMEA** —
- PM provides the "business impact" lens
- Engineer provides the "technical feasibility" lens
- Shared language: 4 high-frequency scripts + bad case 5 classes + 5-category pre-launch eval

A PM who doesn't speak that language = a PM who can't participate in FMEA = a PM who leaves the engineer alone with product decisioning responsibility.

**90% of PMs still saying "button → page jump" = 90% of PMs pushing all AI product responsibility onto engineering.**

---

## Action Checklist

#### Action 1: Print the 4 scripts and stick them on your monitor
- Review / eval disagreement / launch GO/NO-GO / bad-case emergency
- Glance at them before every meeting

#### Action 2: Build a 30-min/day trace-reading habit
- Five fields + 30-second judgment
- Cluster same-class bad cases for the engineering conversation

#### Action 3: Memorize the PM vs engineer experiment boundary
- Don't step over into engineering's job (Accident 1)
- Don't punt back decisions that belong to the PM (the business standard has to come from PM)

#### Action 4: Build a "half-understanding self-check" reflex
- Before saying "just change the prompt" — pause 3 seconds
- Before seeing "95% pass rate" — ask "what's the distribution?"
- Before pointing at a competitor demo — ask "what's the infrastructure?"

---

## Counter-Consensus Lines

- **"Half-understanding is more dangerous than no understanding — engineering catches the ignorant PM, but the half-knowing PM gives confident bad orders."**
- **"PMs don't need to write prompts — but they must speak the right language in 4 high-frequency collaboration scenarios."**
- **"The core competency of a PM in the AI era is not 'using AI' — it's 'knowing where AI can't go.'"**

---

## Closing

This article covered the new collaborative language with engineers — 4 scripts + minimal trace set + boundary map + half-understanding self-check.

The next article — **the new alignment language with your boss.**

Bosses are anxious, pushing on timelines, demanding ROI — but AI projects are inherently uncertain. How do you align with the boss?

Next: 3 boss anxieties + 4 alignment scripts + industry alignment frameworks from Anthropic / OpenAI / Microsoft RAI.

See you next time.

---

> **Companion Resources**: 4-scenario collaboration script playbook + PM 5-field trace cheat sheet + PM vs engineer experiment boundary table + half-understanding self-check (unlocked for paid readers).
> **Next Up**: 24 · The new alignment language with the boss — how to manage expectations on AI projects.
> **Feedback / Reader Community**: WeChat Official Account 「蔡逸雯」

---

> **Reading the Chinese original?** See [23-pm-engineer-language.md](./23-pm-engineer-language.md)
> **Part of**: Season 1 · AI PM Workflow Reconstruction · 26 essays
> **Author**: Cai Yiwen (蔡逸雯) · 8 years in QE → AI PM
