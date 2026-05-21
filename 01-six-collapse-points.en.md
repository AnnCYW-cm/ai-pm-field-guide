# 01 · 6 Collapse Points — Why AI-Era PM Workflow Must Be Reconstructed

> Season 1 · *AI PM Workflow Reconstruction* · Article 1 · Opening
> Estimated length: ~4,000 words

---

After 8 years in software Quality Engineering plus two years deep in AI product consulting, here's the observation:

The most painful thing in the 2026 AI PM circle isn't **"I don't know how"** — it's **"I don't think it matters."**

A senior PM who has written PRDs for 8 years says, "It's just a PRD — add an AI section, what's the big deal?" — until the review meeting, when an engineer asks, "**Where's your eval set?**" and they freeze for the first time.

A product director who has led teams for 5 years says, "It's just a review — follow the process." — until day three after launch, when bad cases erupt and they discover that "**tweaking the prompt**" across 3 rounds has only made things worse.

A leader who can secure budget from the boss says, "It's just cost — engineers will calculate it." — until the CFO holds up the bill and asks, "**How much are we burning monthly?**" and they can't produce a number.

This isn't "skill atrophy." It's **doing AI products with a traditional PM mindset — superficially functional, but loaded with landmines underneath**.

But what's even more painful — **landmines are just the consequence**. **The real cost of "the dismissive blind spot" is being left behind by the era at 5–10x speed**.

---

## Setting the Urgency: Where Does the 5–10x Efficiency Gap Come From?

**Lovable**: a Swedish startup founded in Stockholm in 2024. 2025-Q3 snapshot — **18 people, ~$17M ARR, nearly $1M revenue per employee** — several times the traditional SaaS benchmark. (The company is still scaling; numbers shift over time.)

**Cursor / Anysphere**: 2025-Q3 engineering team of roughly 100 people supporting $1B-scale ARR — **revenue per employee far above traditional SaaS**.

**Anthropic**: a ~2,000-person company with only **a few dozen** sales quota carriers serving hundreds of thousands of enterprise customers — customer-to-salesperson ratio orders of magnitude above traditional SaaS. (Anthropic Research alone is **over 1/3** of headcount.)

(Numbers reflect publicly cited figures; AI application-layer companies grow extremely fast, so verify the latest data against your own context.)

These aren't isolated cases. This is **the output of the "AI Native workflow"** —

- 1 PM + Claude Code + 2 AI Engineers + 1 Eval Engineer ships in **3 months what a traditional team ships in 12**
- Write a Product Note + run Claude Code validation, **decide go/no-go in 30 minutes** — traditional process takes 2–4 weeks
- Tweak prompt, run eval, ship directly — **8-hour iteration cycle** — traditional PRD-RD-QA cycle is 2–4 weeks

**Speed delta: 10–50x.**

David Haberlah, in Medium, dissected the actual output of 638 PMs — AI-related content rose from 4% in early 2023 to **67% in Q1 2026**, while **mocking & prototyping work dropped from 60–70% to 30–40%**.

What ate the 30% that opened up? **Evaluation, agentic architecture, debugging non-deterministic systems** — i.e., the new work corresponding to the six collapse points below.

**That 67% only represents the PMs already pivoting.**

The flip side, even more painful — **33% of PMs are still doing AI products the old way, each project cycle 5–10x longer than their peers**.

---

## The Essence: 3 Things Are Changing Simultaneously

After reading the above you might ask — why is the gap so wide? Are the AI tools that good, or are the new PMs that good?

Neither.

It's because **3 things are changing simultaneously in the foundation of PM work** — and the PM community has wildly different levels of awareness across them.

### Shift 1: Thinking Changed (Deterministic → Probabilistic) — Most PMs are aware

Traditional software is a **deterministic system** — input A always produces output B. The entire PM workflow (interview, PRD, review, dev, launch, ops, retrospective) is built on this assumption.

AI products are **probabilistic systems** — input A might produce B, B', B''. Running the same prompt 100 times might be right 95 times and hallucinate 5 times.

Scrum.org's 2024 piece *Definition of Done for AI Agents* puts it most bluntly:

> "**AI is probabilistic — the same prompt run 100 times might be right 95 times and hallucinate 5. If your DoD is still a binary pass/fail check, you're not testing an agent, you're gambling.**"

This layer is explicit — most PMs know it.

### Shift 2: Pace Changed (Pipeline → Feedback Loop) — Some PMs are aware

A traditional software team is a **PM-RD-QA pipeline** — one baton handed to the next:
- PM writes PRD, hands to RD (2 weeks)
- RD writes code, hands to QA (4 weeks)
- QA tests, ships (1 week)

Each step has clear handoffs, deliverables, and responsibility boundaries. **Pace unit is "weeks/months."**

An AI Native team is a **PM-Prompt-Eval feedback loop** — three roles running in parallel continuously:
- PM writes Product Note + defines eval (continuous)
- Prompt engineer / AI engineer tunes prompt (continuous)
- Eval engineer runs regression + reads traces (continuous)

Async dialogue daily. Weekly eval data drives direction. **Pace unit compresses from "weeks" to "days/hours."**

This layer is semi-explicit — those who get it are already reshaping their workdays; those who don't are still waiting for RD to schedule them in.

### Shift 3: Tools Changed (Old PRD → BMAD / Spec / Claude Code) — Most PMs haven't seen this

This layer is the most lethal.

It isn't "PM tools getting upgraded" — it's **the entire deliverable form of the PM profession being rewritten by a new methodology**:

#### BMAD-METHOD (Breakthrough Method of Agile AI-Driven Development)

Splits the LLM into multiple specialized Agent roles (Architect / PM / Developer) — **documents, not code, become the source of truth**. When the Developer Agent finds a conflict between requirement and architecture, it **must halt and report** — it cannot decide autonomously.

This means — the form of the PRD a PM writes must change completely. **No longer a "document for humans to read," but a "structured spec for multiple Agents to consume collaboratively."**

#### GitHub Spec Kit (Spec-Driven Development)

Open-sourced 2025-09. Core idea in one line:

> "**Specifications become executable, directly generating working implementations rather than just guiding them**."

— specs themselves are executable, **directly generating implementations rather than guiding them**.

The flow: `/specify` → `/plan` → `/tasks` → `/analyze` → executed directly by Claude Code / Copilot / Gemini CLI.

This means — how a PM writes a spec must change completely. **No longer "write and hand to RD to read," but "write and let the Agent run."**

#### Anthropic's "Product Note" Replaces the PRD

Mike Krieger (former Instagram co-founder, Anthropic CPO) publicly said — PMs no longer write 10-page PRDs, they write **3–4 paragraph Product Notes** (user intent + desired outcome + concrete metrics), paired with two context files:
- `product_area_context.md` (business rules, owned by PM)
- `code_context.md` (technical state, owned by engineering)

Cat Wu (Head of Product for Claude Code at Anthropic) has the line:

> "**Prototypes over PRDs**."

— if you can prototype it in Claude Code, don't write a spec.

This means — **the PM's document form compresses from "10-page PRD" to "3-paragraph Note + a working prototype."**

#### Claude Code / Cursor Let PMs Validate Themselves

**Boris Cherny (Anthropic Claude Code lead) publicly stated**: since 2025-11, 100% of his code is written by Claude Code — he no longer types by hand.

**Sachin Rekhi (former LinkedIn) demonstrated**: at a webinar with 1,500 PMs, he showed 13 PM-built skills — customer interview synthesis, NPS triage, SQL-free EDA, product strategy critique, release notes automation.

This means — **PMs no longer need to "wait for engineers to validate a need."** 30 minutes in Claude Code to validate, then decide go/no-go — versus a traditional process of 2–4 weeks of scheduling + review + dev.

---

### 3 Layers of Change Stacking = 6 Collapse Points Collapsing Together

| Shift Layer | Corresponding Collapse Points |
|--------|----------|
| Thinking changed (probabilistic) | #1 Interviews fail, #5 Bad cases, #6 Retro attribution |
| Pace changed (feedback loop) | #3 Eval review, #5 Iteration speed |
| Tools changed (BMAD/Spec/Claude Code) | #2 PRD won't write, #4 Cost estimation, all of them |

**Three things change simultaneously, six nodes of the PM workflow collapse simultaneously.**

---

### Before You Read the 6 Collapse Points — Lift Your View to 2027

The 6 collapse points are about **the present** collapse. But while writing this book, one thing is clear — **in 12–24 months the PM workflow will collapse again, in a completely different way**.

Three signals already happening:

**Context Engineering is replacing prompt engineering.** By 2026 the industry consensus is "who controls the agent's context controls its behavior" — the PM's new foundational skill isn't writing prompts, it's designing the agent's working memory + tiered storage + when it should forget. MemGPT, Letta, and Mem0 are no longer research projects — they're production components.

**Memory enters the PM's required skillset.** Anthropic's Dreaming/Orchestration Memory (rolled out in 2026) — agents themselves identify "which workflows the team repeatedly converges on." What a PM designs is no longer a single conversation, it's **how the model learns your product across sessions**.

**Agent SDK changes product form.** Anthropic 2026-06 spun out Agent SDK billing — meaning "call the API once" is being replaced by "dispatch a group of sub-agents to run for 6 hours." Claude Mythos (2026-05) 50% horizon already reaches 16 hours — **"task as product" is replacing "feature as product."**

Read the 6 present-day collapse points first. But while reading each — carry a question in your head: **does this still hold in 2027?** The answer is mostly "the form remains, the content has changed." This is why a PM must **simultaneously run an L2 present-day workflow + an L3 future vision** — these 26 essays are the L2 toolkit, **and for L3 vision, Article 26 of this book will give you the calibration framework** (the L2/L3/L4 three-tier freshness model).

---

Below are the 6 collapse points laid out on the table. Each is a concrete moment of friction between **"old way vs new way."**

After reading —
- If you say "I've hit all 6" — this column was written for you
- If you say "I've hit none of these" — **don't swipe away yet**. Two possibilities: either you haven't actually built an AI product yet, or you're already stepping on the mines without realizing it. The second is the most dangerous.

---

## Collapse Point 1: User Interviews Can't Surface the Real Need

This is the first one to appear, and the most counterintuitive.

A traditional PM is trained: do user interviews first, then write the requirement doc, then build. **The interview is the source.**

In the AI era, after one round of user interviews you'll discover: **the AI users tell you they want is the AI from sci-fi movies; the AI they're willing to pay for is the AI in the toolbar.**

That chasm in the middle — interviews can't cross it.

A user research review in *Springer Nature* gave this phenomenon an academic name: **"the systematic gap between pre-experience expectations and post-experience evaluation"** — what users expect before using your AI and how they evaluate it after using it are simply not the same thing.

It's not that users are dishonest. Their expectations come from ChatGPT, from *Her*, from Jarvis. They sit across from you, and what's in their head isn't your product — **it's a sci-fi movie**.

**Humane AI Pin is the most expensive sample of this collapse point.** Raised $230M, peak valuation $700M, with positive signals from both user interviews and prototype testing — and ultimately sold to HP in February 2025 for just $116M, with **return units exceeding units sold**. The need for "an AI on my chest I can ask questions to" only holds in sci-fi movies.

Marty Cagan put it more directly in a 2025 SVPG piece:

> "Product discovery is judgement. AI can automate delivery, but discovering unmet needs and validating value — AI can't do that."

What he didn't say: **humans are finding it harder too** — because in the AI era, users' "unmet needs" have been **redefined by sci-fi movies**.

**Through a Quality Engineering perspective** — this is a fundamental mismatch between "the need as a probability distribution" and "the interview as a single-point sample." What you sample in an interview is the user's sci-fi expectation; what the model can deliver is a distribution of 75% accuracy + 5% hallucination. The two simply don't line up.

---

## Collapse Point 2: The PRD Won't Write Itself

The second collapse point follows directly from the first.

You've gathered a "requirements list" from interviews. You open Word. You start writing the PRD.

Halfway through, you stop —

- What's the "definition of done" for this feature? The traditional answer is "runs as expected." But AI output is probabilistic; expectation is a distribution.
- How do you draw the "page transitions" for this interaction? The traditional answer is "click button A, jump to page B." But AI product interactions increasingly have no "pages" — they are dialogue, context, agent flows.
- How do you define the "acceptance criteria" for this need? The traditional answer is "all items in the feature list checked off." But AI product features aren't discrete — capabilities are continuous.

You can't keep writing.

It's not that you don't know how to use Word — it's that **"the PRD form itself" has failed for AI products**.

Microsoft CPO Aparna Chennapragada said it most sharply on Lenny's podcast:

> "**Prompt sets are the new PRDs.**"

It's not "PRD templates need updating." It's that **the PRD itself is being replaced**. Aparna said: "A prompt set is a living artifact — half spec, half training data; every prompt is a sample that shapes agent behavior."

There's a widely shared article on Renrendoushichanpinjingli (a Chinese PM community) titled *Countdown to the PRD's Exit* — in it, PMs vent: "When the PRD changes mid-stream or hits phase-two iteration, **context is lost, historical business constraints get overwritten, triggering global format collapse.**"

It's not that the PM writes badly — it's that the PRD as a tool is no longer enough.

**A PM who has written AI PRDs typically gets stuck in 3 sections**:

- **Eval section** — traditional PRDs don't have this; the PM doesn't know how to set case count, pass line, or who labels
- **Bad Case grading section** — the 4-tier degradation strategy needs to be defined at the PRD stage, but without having stepped on the landmines you can't imagine it
- **Cost budget section** — the token ledger for the CFO; PMs have always relied on engineers and never calculated it themselves

Stuck on 1 of these 3 sections and the PRD can't continue. Articles 11–15 will unpack these 3 sections one by one.

---

## Collapse Point 3: At Tech Review You're Asked "Where's the Eval Set?" — and You Can't Answer

The PRD is done. Grit your teeth and take it to review.

The engineer reads it and asks:

> "Where's your eval set?"

The PM freezes.

A traditional PM doesn't need to bring an eval set — they bring acceptance criteria, QA writes test cases, and review passes for dev.

An AI PM **must bring an eval set**. **Without an eval set, the engineer cannot define what "done" means.**

Hamel Husain and Shreya Shankar, in their 2025 Lenny Newsletter piece, made the core point:

> "**Writing good evals is becoming the defining skill for AI PMs.**"

They've taught 2,000+ PMs and engineers, including teams at OpenAI and Anthropic. The collapse moment that recurs in class: **the PM walks into review with a demo, and the engineer asks back — "Where's your golden set, and what's the scoring rubric?"**

The PM hasn't prepared for that question.

It's not that the PM is lazy — it's that **"the eval set" simply doesn't exist in the traditional PM workflow**. You can be a PM without knowing SQL; you can't be an AI PM without doing evals — this is what Hamel calls **"the new analytics."**

**From 8 years of Quality Engineering experience** — eval sets aren't actually new. Any traditional ML project (fraud detection, churn prediction, sales forecasting) treats evals as infrastructure. The LLM community lost this practice — simply because prompt engineering looks so "light" that people mistakenly think evaluation can be skipped. **The result: launch equals crash.**

---

## Collapse Point 4: The Boss Asks "How Much Does This Feature Cost?" and You Can't Do the Token Math

PRD review passes. Development begins. Then the boss comes by:

> "Once this feature ships, how much do we burn per month?"

The PM can't calculate it.

Not because they can't do math. Because they **simply don't know how many tokens one conversation triggers, how many retries, how deep context accumulates, what cache hit rate is, or how many times more expensive output is than input**.

They mumble something like "shouldn't be expensive."

The boss is skeptical.

So the PM goes and asks the engineer. The engineer says: "Based on this prompt length, one conversation is about 1,500 tokens; at GPT-5 output price of $30/M…"

The PM doesn't follow.

What's even scarier — **Cursor gave every AI product leader a public lesson**: in June 2025, Cursor switched without warning to credit-based billing. Existing users went from a "$20/month mental model" suddenly to $200–$400 in overage; on Hacker News someone posted "$350 in a week" — **monthly cost effectively grew 10–20x**. On July 4 the CEO publicly apologized and refunded.

After this incident, every AI product leader's boss started asking: "Could that happen to us?"

And most PMs' answer is — **"I don't know."**

**From doing AI product consulting, here are 3 token-math pitfalls I see repeatedly**:

1. **Counted input but not output** — output tokens are 3–10x more expensive than input; the bill the boss sees is always 5x higher than the estimate
2. **Counted first call but not retries** — 1 failed retry = double cost, 3 retries = 4x cost
3. **Counted base prompt but not context accumulation** — multi-turn dialogue input doesn't grow linearly, it **expands quadratically**

A PM who's hit all 3 — usually has already been called into the boss's office for a chat.

(Article 9 on the Token Ledger will unpack these 3 + 5 common missed-counts one by one.)

---

## Collapse Point 5: After Launch, Bad Cases Appear — Should You Fix the Prompt or Change the Product?

You grit your teeth and ship.

Day three, ops finds you: "User feedback — AI answered wrong in scenario X."

You open the backend, read 5 cases, start tweaking the prompt.

Tweak done. Ship.

Day seven, ops finds you again: "User feedback — AI answered wrong in scenario Y."

You open the backend and look — this scenario Y, **was running fine last week**.

This is **"fixed A, broke B."**

OpenAI's own GPT-4o sycophancy incident was this exact mechanism — to make conversation "friendlier," they trained the model to agree with harmful decisions (even agreeing with stopping medication). OpenAI's own postmortem admits: **"sycophancy was not a blocking item in the launch evaluation."**

Rolled out April 25 → fully rolled back April 29. **4 days.**

Roll back? Keep tweaking? Admit this case can't be solved by a prompt and the product design needs to change?

A traditional PM fixing a bug is like fixing a pipe — fixed is fixed.
An AI PM fixing a bad case is like tuning a piano — **tune one string and the others all vibrate**.

There's no concept of "regression set" in the workflow. There's no "failure taxonomy" in the PM's head. You can only guess.

**A PM who has actually run AI projects discovers** — the same bad case, prompt tweaked 3 rounds with no effect, root cause might not be in the prompt at all:

- **Retrieval missed a key document** (changing the prompt won't ever save it)
- **The business flow itself shouldn't let AI decide** (what needs changing is product design, not the prompt)
- **User input contains prompt injection** (add an input filter, don't change the system prompt)

5 failure modes (hallucination / refusal / drift / format breaking / safety violation), **each requiring a completely different fix path** — but 90% of PMs reflexively say "tweak the prompt."

**Through a Quality Engineering perspective** — this conflates "test cases" with "distribution correction." Traditional bugs are binary (errored / didn't error); AI bad cases are distributional (which tail of the distribution erred). **Fixing a distribution with a bug-fixing mindset — you inevitably play whack-a-mole.**

(Article 21 on Bad Case Management will unpack the 5 failure modes + 4-pick-1 repair strategy completely.)

---

## Collapse Point 6: In the Retrospective You Can't Tell "Is It a Model Issue or a Design Issue?"

Week-one retrospective.

The data looks bad. Retention low, conversion low, complaints high.

Engineer says: "The model isn't there yet — wait for the next version."
Designer says: "User path has issues — needs a walkthrough."
PM says: "…"

The PM can't articulate the attribution.

Not because they aren't professional. Because **AI product failures have 4 completely different attribution paths** — hallucination, refusal, drift, format breaking. Each has a completely different fix. Hamel calls this **"failure taxonomy."**

But Chinese PM circles have barely popularized the concept.

In the retro, the engineer blames "user path," the designer blames "model capability" — **in the end, no one moves**. The next week the data is still bad. The week after, the boss comes — "Why is our AI worse than ChatGPT?"

That's when the PM realizes — **they've gone from being "the PM" to "the person stuck in the middle with no idea what to do."**

---

## The Real Cost of the Dismissive Blind Spot: Left Behind at 10x Speed

By now, the 6 collapse points should be clear.

But more painful than the 6 collapse points is — **dismissive PMs don't just step on landmines; they're left behind by the new workflow at 5–10x speed**.

What does that mean concretely?

| Work scenario | Old way (dismissive PM) | New way (PM who has pivoted) |
|---------|------------------------|-------------------|
| Validate whether an AI need is feasible | Write PRD → review → schedule → RD dev → wait for demo (2–4 weeks) | Run validation yourself in Claude Code (**2–3 hours**) |
| Write PRD | 10-page Word + multiple reviews (3–5 days) | Product Note + Spec + working prototype (**1 day**) |
| Reproduce a bad case | Schedule RD → wait for trace (3–7 days) | Claude Code reads codebase, reproduces locally (**1 hour**) |
| Align with engineering on capability boundaries | Back-and-forth meetings + repeated prompt tweaks (1–2 weeks) | Run evals together, let the data talk (**1–2 hours**) |
| Calculate token cost for the boss | Get RD to estimate → back and forth (3–5 days) | Self-serve with spreadsheet + Claude (**30 minutes**) |

**Across 5 scenarios, average — the new way is 10x faster.**

Meaning:
- **In 6 months**: the new-way PM has validated 10 projects; the dismissive PM is still on their first PRD
- **In 1 year**: the new-way PM has accumulated product judgment; the dismissive PM is still chasing "why is our AI worse than ChatGPT"
- **In 2 years**: the new-way PM may be core at an AI Native team; the dismissive PM gets an invitation from HR for a chat

**This isn't a skill gap, it's a cognition gap.**

Skill gaps can be closed — take a course, read a book, follow a tutorial.
Cognition gaps are tacit — you don't know what you're missing, because you think "it's just being a PM."

---

## What the Next 25 Articles Will Do

This article is the opener. From the next article onward, **we'll swap out the old way for the new way one node at a time**:

- Article 2 clarifies the paradigm shift — from "managing features" to "managing capabilities"
- Articles 3–6 fix the Requirements stage (Collapse Point 1)
- Articles 7–10 fix the Solution stage (Collapse Points 2, 4)
- Articles 11–15 fix the PRD stage (Collapse Points 2, 3) — the hard-currency stretch of the column
- Articles 16–19 fix the Delivery stage (Collapse Points 3, 5) — **including a PM's killer move with Claude Code**
- Articles 20–22 fix the Ops stage (Collapse Point 5)
- Articles 23–25 fix the Collaboration stage (Collapse Point 6) — **including building an AI Native team (the B-side funnel core)**
- Article 26 closes — a PM's AI-era growth path

Each article follows a **two-layer structure** — the first half is **Workflow** (methods, templates, judgment frameworks you can use next week), and the second half is **Engineering Reality** (why you do it this way, the underlying engineering constraints, real-world failure cases).

Read just the first half — apply immediately next week.
Read both layers — build a judgment you won't find elsewhere.

---

## QE Lens on the 6 Collapse Points

If you read the 6 collapse points side by side, one pattern emerges that 90% of PMs miss — **all 6 are essentially Quality Engineering problems incorrectly framed as PM problems**:

- Collapse Point 1 (interviews fail) — a sampling problem: single-point samples can't characterize a probability distribution
- Collapse Point 2 (PRD won't write) — a specification problem: deterministic specs can't describe non-deterministic systems
- Collapse Point 3 (no eval set) — a test infrastructure problem: missing the most basic QE asset
- Collapse Point 4 (can't calculate cost) — an observability problem: no instrumentation, no metrics
- Collapse Point 5 (whack-a-mole on bad cases) — a regression problem: missing both regression set and failure taxonomy
- Collapse Point 6 (can't attribute in retro) — a root cause analysis problem: no FMEA framework

This is why I claim: **AI PMs without a QE foundation will keep stepping on landmines, because they're solving QE problems with PM mental models**.

This isn't "PMs must become testers." It's that **the QE perspective (probability thinking, distribution thinking, failure modes, regression sets, FMEA) is becoming a core PM skill**.

This column will systematically pour the QE perspective into every chapter — not as an extra section, but as the underlying view.

---

## Closing Thoughts: Why Write These 26 Articles

If you've been following AI PM content for a few years, you may have noticed —

The industry isn't short of AI PM tutorials. Lenny, Marty Cagan, Sachin Rekhi, Hamel Husain, Aparna Chennapragada are all writing. Geek Time, Qidian Academy, and Sanjieke all have courses.

So why write another?

**Not because the methodology is exclusive** — Anthropic, OpenAI, and Hamel have all covered these methods.

**It's because most AI PM content in the industry only covers the "thinking changed" layer (root cause 1), and doesn't systematically cover "pace changed + tools changed" (root causes 2 + 3).**

A counter-consensus I see after 8 years of Quality Engineering plus pivoting to AI products —

> **In the next decade of AI products, the winners aren't those with the strongest models — they're those with the highest quality bar.**
> **In the next decade of AI PMs, the winners aren't those who know the most — they're those whose workflow is the fastest.**

These 26 articles are an attempt to fully cover both: **looking at AI products through a Quality Engineering lens + the practical methods of an AI Native workflow** —

- Not just teaching you to write prompts
- Not just teaching you to pick a model
- Not just teaching you to build a demo

But teaching you **the full step-by-step transition from the old way to the new way** —
- How to write the new form of PRD (Product Note + Spec + working prototype)
- How to use Claude Code to compress the validation cycle from 2 weeks to 2 hours
- How to build a PM-Prompt-Eval feedback loop that replaces the PM-RD-QA pipeline
- How to use a Quality Engineering lens to see AI product failure modes, probability distributions, and decision boundaries

— this is the spot that neither Chinese nor international PM circles have systematically covered.

The next article switches the first tool — **from "managing features" to "managing capabilities."**

If you're still reviewing AI products with a "feature list," you and engineering will never be on the same page.

---

## Your Action Checklist

Before reading Article 2, do these three things:

1. **Self-check against the 6 collapse points** — which have you hit? Which haven't you?
2. **Pick the most painful one** — make it the through-line problem you carry as you read this column
3. **Open Claude Code and run something small** — even just "read my latest PRD and tell me what 5 problems would appear if I used it for an AI product" — to get a feel for the new workflow's speed

If you've completed these 3 — your reading of Articles 2–26 will be 3x more efficient.

---

## Counter-Consensus Quotes

> "**Prototypes over PRDs**." — Cat Wu, Head of Product, Claude Code, Anthropic

> "**Prompt sets are the new PRDs.**" — Aparna Chennapragada, CPO, Microsoft

> "**Writing good evals is becoming the defining skill for AI PMs.**" — Hamel Husain & Shreya Shankar

> "**AI is probabilistic — if your DoD is still a binary pass/fail check, you're not testing an agent, you're gambling.**" — Scrum.org, *Definition of Done for AI Agents*

> "**Product discovery is judgement. AI can automate delivery, but discovering unmet needs and validating value — AI can't do that.**" — Marty Cagan, SVPG

> **In the next decade of AI products, the winners aren't those with the strongest models — they're those with the highest quality bar.** — Cai Yiwen

---

## Next Up

**Article 02 · The AI PM's New Coordinate System — From "Managing Features" to "Managing Capabilities"**

If you're still reviewing AI products with a "feature list," you and engineering will never be on the same page. Article 02 will give you the new coordinate system.

---

## Companion Resources

> **Companion asset for this article**: *6 Collapse Points Self-Check Checklist* PDF (unlocked for paid subscribers)
> **Feedback / Reader Community**: WeChat Official Account 「蔡逸雯」

---

> **Reading the Chinese original?** See [01-six-collapse-points.md](./01-six-collapse-points.md)
> **Part of**: Season 1 · AI PM Workflow Reconstruction · 26 essays
> **Author**: Cai Yiwen (蔡逸雯) · 8 years in QE → AI PM
