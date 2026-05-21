# 03 · AI Product Needs No Longer Come from User Interviews

> Season 1 · AI PM Workflow Reconstruction · Essay 3 · Part 1 Requirements

---

The second dismissive blind spot:

**90% of PMs are still treating "user interviews" as the starting point for AI product requirements.**

The method isn't wrong. But **the very premise that "user interviews are the source of requirements" has stopped working for AI products**—while most PMs in the industry are still running interviews, building personas, drawing user journeys on the traditional playbook.

The result: AI features built from interviews ship and nobody uses them.

By the end of this essay you'll see—real AI product requirements come from 4 sources, and **interviews are the weakest of the four.**

---

## Part 1 · Workflow: 4 Real Sources of AI Product Requirements

### Source 1: Capability Ceiling Observation (Most Important)

It's not the user telling you what they want. It's **the model telling you what it can do.**

The concrete method: a "**1-day capability probe**":
- Take the strongest current model (Claude Opus 4.7 / GPT-5.5 / Gemini 3 Pro)
- Pick 5-10 real tasks from your target scenarios
- Run them and observe which dimensions the model handles well, which it can't
- Record the **"accuracy distribution"**—not the average

**The output of this one day is more valuable than 20 user interviews.**

Why? Because **users have no concept of what AI can do.** A Springer Nature user-research review gives this phenomenon an academic name: "the systematic gap between pre-experience expectations and post-experience evaluation." **Users' expectations come from sci-fi movies, not from model boundaries.**

The requirements you extract in interviews: **half are things the model can't do** (user expectations too high), and **half are things the model can easily do but the user never thought to ask for** (expectations too low).

Only by running the capability ceiling first can you find which requirements fall in the intersection of "the model can" and "the user wants."

### Source 2: Competitor Bad-Case Analysis

The second real source: watch where competitors break.

The method:
- List 3-5 direct competitors (including ChatGPT / Claude / Tongyi / Kimi / Doubao)
- For each, collect 20-50 publicly aired bad-cases (sources: Xiaohongshu, Jike, X, Reddit)
- Classify by failure mode (hallucination / refusal / drift / format)
- Find the cases **every competitor fails at**—**that's your opportunity.**

**Competitors' bad-cases are more honest than your own user interviews.** In interviews, users say what they want; in comment sections, they curse the real pain points.

### Source 3: Cost Back-Calculation

The third real source runs backward—from "how much revenue this could earn" reverse-derive "what the technology must hit."

The method:
- Assume you charge users ¥29.9/month
- Assume gross margin must be ≥ 50%
- Then token spend per user per month must not exceed ¥15
- Reverse-derive: how many conversations per day, max context per conversation

If the "technical constraint" you reverse-derive is something the current model can't do—**the requirement isn't commercially viable.** Cut it.
If the "technical constraint" is something the model handles easily—**it's low-hanging fruit.** Build now.

ICONIQ's 2025 AI product study gave the hard data: average AI product gross margin 2024=41%, 2025=45%, 2026=52%—**still far below traditional SaaS's 70-80%.** If you can't do token economics, you're not building an AI product. You're running a charity.

(Essay 9 on the Token Ledger walks through this back-calc in detail.)

### Source 4: Mapping User Pain Points to "AI-Solvable Space"

The final source is user interviews—but **used completely differently from traditional interviews.**

Traditional interviews ask: "What do you want?"
AI interviews ask: "**How do you solve this problem today? Which step is most painful?**"

Don't collect wishes—**observe behavior.**

The "painful step" you observe is the real pain point. Then go back and ask yourself: can AI solve this step?

If yes—build it.
If no (requires professional judgment, compliance, accountability)—don't.

---

## The "Capability-First" Requirements Workflow

Stringing together the 4 sources gives you the new AI-era requirements workflow:

```
Day 1: Capability probe (Source 1)
  → Run 5-10 real tasks, record model capability distribution

Days 2-3: Competitor bad-cases (Source 2)
  → Collect 100+ real bad-cases from 3-5 competitors
  → Find scenarios where every competitor fails

Day 4: Cost back-calculation (Source 3)
  → Run token economics
  → Cut requirements that can't pencil out

Days 5-7: Behavioral observation interviews (Source 4)
  → Watch 5-10 target users solve the problem today
  → Find the "painful step"
  → Map to AI-solvable space

Day 8: Cross-validation
  → Requirements that land in all 4 circles—capability-reachable × competitors haven't nailed it × cost-bearable × user genuinely pained
  → That's the real requirement
```

8 days—**faster and sharper than the traditional "3 weeks of interviews → 1 week of synthesis."**

---

## Part 2 · Engineering Reality: Why User Interviews Have Failed

### Failure Cause 1: User Expectations Aren't Based on Capability—They're Based on Sci-Fi

I quoted Springer Nature earlier—saying it again: "the systematic gap between pre-experience expectations and post-experience evaluation."

What users tell you they want is *Her*, *Jarvis*, sci-fi.
What's actually usable is ChatGPT's 75% accuracy + 5% hallucinations + occasional refusals.

**Interviews can't bridge that chasm.**

Worse: the model itself is sycophantic. TechXplore had a study in July 2025 verifying exactly this: **chatbots are confident even when wrong.** Users in demo trials get bewitched by output that "pretends to know," then give over-optimistic feedback in interviews.

You take that "optimistic feedback" into product. Once it ships and real-world data hits, **feedback collapses instantly.**

### Failure Cause 2: The Engineer's "What Can Be Built" and the PM's "What Should Be Built" Are Often Misaligned

A traditional PM doesn't need to understand the engineer's lens. If a requirement makes sense, the engineer should build it.

An AI PM must understand the engineer's lens. **Otherwise the requirement you submit will not, after the engineer builds it, be what you wanted.**

Example. From interviews you get the requirement: "Users want AI to automatically summarize meetings and send out the notes."

Engineer hears it, fine, goes to build. Delivers in 3 weeks.

Open the test—

- Short meetings (10 minutes) summarized beautifully
- Medium meetings (30 minutes) somewhat off
- Long meetings (1 hour+) summaries wildly wrong
- Multi-person meetings (5+ people) speakers indistinguishable

PM says "doesn't work, tune it again."
Engineer says "can't tune further, this is a context window limit."

That's when the PM realizes—**"automatically summarize meetings" is, in engineering terms, a composition of 4-5 different capabilities**, each with completely different boundaries.

If the engineer's lens had been used from day one, the requirement would have become: "**Automatic summaries for short meetings (< 30 min, < 3 people)**"—what the model can do today, what closes the loop commercially, the slice of the user's pain that's truly painful.

The rest—long meetings, multi-person meetings—wait until model capability catches up.

### Failure Cause 3: "Capability Ceiling Observation" Is a Baseline QE Move

**From the Quality Engineering perspective of 8 years building software**—

Any mature ML project (fraud detection, churn prediction, demand forecasting) treats the "**capability probe**" as the first move before project approval. **No company anywhere approves a project without knowing the model's baseline performance**—because that would amount to telling engineers to build something "maybe possible, maybe not."

The LLM world dropped this move—only because ChatGPT made "looks like it can do anything" a constantly-demonstrated illusion, and PMs were misled into skipping the probe and going straight to project kickoff.

**The result is user interviews failing + PRD impossible to write + crashes on day-one launch**—three symptoms of the same root cause.

---

## Recent Takes From Several PM Thought Leaders

### Marty Cagan (SVPG, 2025)
> "Product discovery is judgment. AI can automate delivery, but it can't discover unmet needs or validate value."

He defines the core AI-era capability as **discovery capability**, not interview technique.

### Teresa Torres (2025 webinar)
After building her first AI product:
> "Customer interviewing itself has to change. In AI products, the outcome isn't deterministic—interviews can no longer ask 'what do you want.' They have to **log traces / have humans review / label error classes / write evals / A/B test fixes.**"

The object of "interviewing" expands from "user opinion" to "system trace."

### Lenny Rachitsky quoting Kevin Weil (OpenAI CPO)
> "Quarterly roadmaps and annual strategy no longer reflect real shipping cadence—**roadmaps must be redefined as rolling bets.**"

The implication: the traditional "interview → requirement → roadmap" pipeline has failed. **Requirements are rolling bets, not pre-planned.**

---

## Your Action Checklist

#### Action 1: Delete the "user interview" week from your next project
- Replace with a "capability probe" week
- 1 day for model capability boundaries
- 4 days for competitor bad-cases + cost back-calc
- 2 days for behavioral observation interviews (not wish-list interviews)

#### Action 2: Make the "4-circle intersection" your requirements review framework
- Every new requirement passes 4 circles: model-capable × competitors haven't nailed it × cost-bearable × user genuinely pained
- All 4 pass → build
- Any 1 missing → cut

#### Action 3: Upgrade your interview script
- From "what AI do you want" to "how do you solve this today, which step is most painful"
- From "collecting wishes" to "observing behavior"
- Minimum 5 interviews to form a baseline

---

## Counter-Consensus Quotes

- **"The AI users tell you they want is the AI in sci-fi movies; the AI they'll pay for is the AI in the toolbar."**
- **"AI-era interviews aren't 'what do you want'—they're 'what are you already secretly doing inside ChatGPT.'"**
- **"Discovery no longer precedes build—it runs alongside build. Capability itself is research material."**

---

## Closing Thoughts

This essay covered the fundamental change in requirement sources. The next essay enters a more concrete judgment:

A business stakeholder drops an "AI-ification requirement" on your desk. How do you tell, in the review meeting, whether it's a real need or a fake one?

I'll give you a 3-dimension judgment framework—3 questions to ask the stakeholder, and you'll immediately know "build / don't build / think again."

More importantly: **90% of "AI-ification requirements" dumped on PMs' desks are false propositions.**

Why 90%? See you in the next one.

---

> **Companion Resources**: AI requirement source 4-dimension checklist + behavioral observation interview script variants (paid readers)
> **Next Up**: 04 · "Should AI-ify vs Shouldn't AI-ify" Judgment Framework—What 90% of Pseudo-AI Needs Look Like
> **Feedback / Reader Community**: WeChat Official Account 「蔡逸雯」

---

> **Reading the Chinese original?** See [03-not-from-user-interviews.md](./03-not-from-user-interviews.md)
> **Part of**: Season 1 · AI PM Workflow Reconstruction · 26 essays
> **Author**: Cai Yiwen (蔡逸雯) · 8 years in QE → AI PM
