# 02 · The New Coordinate System for PMs in the AI Era—From Managing "Features" to Managing "Capabilities"

> Season 1 · AI PM Workflow Reconstruction · Essay 2 · Prelude

---

In Essay 1, I said the most painful thing for PMs in the AI era is not "I don't know how to do this anymore." It's "**the dismissive blind spot.**"

This essay tackles the first dismissive blind spot:

**90% of PMs are still reviewing AI products with feature lists.**

It's not that PMs are being lazy. The paradigm shift hidden in the one-word difference between "feature" and "capability" is something **most PMs in the industry have not even noticed needs to happen.**

By the end of this essay, you'll see—if you're still reviewing AI products with feature lists, you and your engineers will never be talking about the same thing.

---

## Part 1 · Workflow: All 5 Dimensions Must Change

### Dimension 1: The Deliverable Has Changed

**Feature era**: Your deliverable is a feature list—an Excel sheet, one feature per row, with status, owner, and ship date.

**Capability era**: Your deliverable is a **capability card**—a set of Markdown / Notion docs, each card mapping to one capability, containing:
- Capability name (e.g., "Customer Intent Recognition")
- Input / output schema
- **Reliability range** (e.g., "95% accurate, 5% fallback")
- **Dependencies** (e.g., "depends on GPT-5, retry cap of 3, cache strategy X")
- **Degradation path**

Mature frameworks already exist:

- **Google's Model Card (2018)** was the earliest prototype, later extended by Cambridge's *Data & Policy* journal into the "**AI Product Card**" framework (2024), now a standard template in public-sector deployments
- **Miqdad Jaffer (OpenAI Product Lead)** publishes an "AI PRD Template" on productcompass.pm—structure: capability boundaries / IO schema / eval set / failure modes / cost ceiling

**It is no longer "pages + buttons."**

### Dimension 2: Definition of Done (DoD) Has Changed

**Feature era**: DoD is "feature shipped, acceptance passed"—binary, pass / fail.

**Capability era**: DoD is "capability meets bar"—distributional, the minimum pass rate across N repetitions.

The Scrum.org blog *Definition of Done for AI Agents* puts it bluntly:

> "**AI is probabilistic—the same prompt run 100 times might be right 95 times and hallucinate 5 times. If your DoD is still a Pass/Fail binary check, you're not testing an agent, you're gambling.**"

The new DoD must contain 4 items:
1. **Minimum pass rate over N repetitions** (e.g., ≥95 out of 100 runs match expectations)
2. **No regression on the regression set** (old-case accuracy doesn't drop)
3. **Confidence threshold** (output carries confidence; below threshold triggers fallback)
4. **Degradation path implemented** (fallback mechanism is live)

If your DoD is still a checkbox in the "feature shipped" column—**you're not managing an AI product, you're gambling.**

### Dimension 3: Test Cases Have Changed

**Feature era**: Test cases are "does input A produce output B"—single-point, deterministic.

**Capability era**: Test cases are "does the distribution of outputs from running input A 100 times match expectations"—distributional, probabilistic.

That means your test case library shifts from "N cases" to "N cases × M repetitions × K evaluation dimensions." **The order of magnitude explodes.**

But the harder part is—**you need a new role.**

- Traditional QA doesn't write evals
- Anthropic / OpenAI are openly hiring Evals-related Engineering Managers, with base in the **$300K+** range
- Netflix is hiring "Software Engineer L4/L5, LLM Evaluation & Infrastructure"
- **Eval engineers are becoming a distinct profession** (in China still called "AI test engineer" or "LLM evaluation algorithm engineer," but it's the same thing)

More in Essay 25 on building AI-native teams.

### Dimension 4: Product Docs Have Changed

**Feature era**: Product docs are "feature list + user journey."

**Capability era**: Product docs are "**capability inventory + model journey**."

A widely-shared essay on 人人都是产品经理 proposed this localized concept—"**model journey.**" The interaction is no longer "user-product," it's a "**user-model-product**" three-way relationship.

A product doc must now answer 3 new things:
- What prompts will the user's input pass through?
- What post-processing will the model's output pass through?
- When the model gets it wrong, what does the user see?

If your PRD doesn't have these 3 sections, it's not an AI product PRD. It's a "**traditional product PRD that happens to include AI features.**" Two different things.

### Dimension 5: Team Language Has Changed

**Feature era**: You discuss "pages / buttons / navigation" with engineers.

**Capability era**: You discuss "**prompt / eval / case**" with engineers.

David Haberlah on Medium analyzed the actual output of 638 PMs—AI-related content **grew from 4% in early 2023 to 67% in Q1 2026.** Topics shifted from "growth loops / A/B testing" toward "evaluations, agentic architecture, non-deterministic systems." Mocking & prototyping work dropped from 60-70% to 30-40%.

If in a 1-hour meeting with an engineer you say "page" more than 5 times and "prompt" fewer than 3 times—**you two are not talking about the same thing.**

---

## Part 2 · Engineering Reality: 3 Engineering Realities You Must Understand

### Reality 1: A Capability's Reliability Has a Ceiling

Traditional features can hit 100%. Click button A, you always land on page B. Deterministic.

**AI capability reliability is distributional. It will never reach 100%.**

Anthropic itself repeatedly emphasizes in evaluation papers: eval results **must come with confidence intervals.** 0.85 vs 0.87 may not be significant on small samples. This isn't "the model is bad," it's **the nature of probabilistic systems.**

Meaning: when you write a PRD, "100% accuracy" is a phrase you **can no longer write.** Write "95% case pass line + 5% fallback mechanism."

**From a Quality Engineering perspective**—across 8 years in traditional software QE, I kept seeing the same counter-consensus pattern: **products that chase 100% accuracy end up not delivering 100%—because you'll ship the version that "looks like 100%," then production hits out-of-distribution samples and the cracks appear.**

The correct approach: **accept the "95% + 5% fallback" reality and engineer the fallback rigorously.** This is the single biggest cognitive gap between AI products and traditional software.

### Reality 2: Capabilities Influence Each Other

Traditional features are independent—working on feature A doesn't affect B.

**AI capabilities affect each other.** Optimizing capability A may degrade capability B.

This isn't a bug. It's engineering reality.

#### Academic backing

An EMNLP 2024 paper on RLHF alignment tax measured: when OpenLLaMA-3B's preference alignment reward rose from 0.16 to 0.35—SQuAD F1 **dropped 16 points**, DROP F1 **dropped 17 points**, WMT BLEU **dropped 5.7.**

"Safety capability up = translation / reading-comprehension capability down" **is quantifiable.**

#### Industry evidence

The Cursor team openly acknowledged: **after Claude 3.7 was post-trained for Claude Code, coding improved substantially but general capability dropped.** Even leading firms can't dodge this phenomenon.

#### Design implications

A capability-flow diagram must reflect this coupling (see Essay 7). Suggested drawing:
- Use dashed lines between capabilities that "affect each other"
- Annotate the dashed line with "if A is optimized, B may drop X%"
- The review meeting discusses "do we want to sacrifice B for A"

If your capability-flow diagram has no dashed lines—**your design has ignored the hardest engineering reality of AI products.**

### Reality 3: "Managing Capabilities" Means a PM Must Understand 3 New Things—Boundaries / Cost / Evolvability

A traditional PM managing features needs to understand "**user scenarios + business processes.**"

An AI PM managing capabilities needs to understand 3 new things:

#### Boundaries
You must know what this capability **cannot do.**

Example: the 2024-Q4 snapshot of OSWorld (a computer-use benchmark): OpenAI Operator (CUA) **38.1%**, Anthropic Computer Use **22.0%**, human baseline **72.4%** (model scores expire in 6 months—by H2 2025 numbers crossed 40-50%, but human baseline is still far higher). Operator is essentially "a beta you're paying for."

Without this number, your PRD will dare to claim "AI handles the user's entire flow end-to-end"—**a guaranteed disaster after launch.**

#### Cost
You must know how much this capability **burns.**

Not "GPT-5 output costs $30/M tokens"—that's engineer-level. It's the CFO-readable "**every monthly active user burns ¥3.2, gross margin headroom ¥X.**"

Cursor's June 2025 billing blowup—long-time users burning $350 in a week, monthly cost surged 10-20x, CEO apologized and issued refunds on July 4—**delivered a public masterclass to every AI product PM.** After watching it, your boss will ask: "Could this happen to us?"

If you can't answer that question, **you're not doing your job.**

#### Evolvability
You must know how this capability **keeps improving.**

The model is upgrading (GPT-5 → 5.1 → 5.5 → Opus 4.6 → 4.7, each release 6-8 weeks). Prompts are iterating (weekly). The eval set is expanding (every new bad case gets added).

**Traditional features barely change after launch. AI capabilities change every week.**

A PM's job is not "shipping," it's "**continuously governing the direction in which this capability evolves.**"

---

## A Counter-Consensus: The Industry Has No Settled Term for Capability-Flow Diagrams—This Is a Land Grab

Honest disclosure—**the industry currently has no unified term or template for "capability-flow diagrams."**

Anthropic has the Claude Design philosophy (progressive disclosure), Cursor has its "engine vs car" framing, Anthropic's AI-First Dev workflow uses a plan/act/review triad—**these are all relevant methodologies, but none of them is called "capability-flow diagram."**

Essay 7 will give a concrete capability-flow template. What this column tries to do is **stitch together the scattered methodologies from Anthropic / Cursor / OpenAI into a workflow Chinese PMs can use directly.**

If you accept this lens—the action checklist below is immediately useful.

---

## Your Action Checklist

#### Action 1: Replace the "feature list" in your next PRD with "capability cards"
- Rewrite each feature as a card
- Each card contains: capability name / IO schema / reliability range / dependencies / degradation path
- Attach the eval set design at the end

#### Action 2: Upgrade "Definition of Done" from binary to 4 items
- Minimum pass rate over N repetitions
- No regression on the regression set
- Confidence threshold
- Degradation path implemented

#### Action 3: In reviews, replace "page / button" with "prompt / eval / case"
- Write these 3 words on the whiteboard before pitching
- If you catch yourself saying "page" more than 5 times in an hour—stop and restart the review

#### Action 4: Run a "boundaries / cost / evolvability" 3-dimensional check on every capability
- Boundaries: run a public benchmark like OSWorld / SWE-bench
- Cost: calculate "LLM cost per MAU per month," not "per token"
- Evolvability: write a 6-month "capability roadmap"

#### Action 5: Schedule a "terminology alignment session" with engineers
- Spend 30 minutes aligning on the definitions of 6 terms: prompt / eval / case / agent / RAG / fine-tune
- After alignment, all reviews use the same vocabulary

---

## Counter-Consensus Quotes

- **"In a feature-flow world, PMs draw mockups; in a capability-flow world, PMs draw model-inference diagrams—it's not the same job in new skin, it's two different professions."**
- **"The side effects of a traditional product are written in a bug list; the side effects of an AI product are written as 'another capability's score dropped 17 points.'"**
- **"The moment DoD shifts from Pass/Fail to a confidence threshold, the traditional PM is already out of a job."**

---

## Closing Thoughts

This essay covered the first concrete move in the paradigm shift—**from "feature" to "capability."**

The next essay enters Part 1 of the season—**Requirements.**

The first collapse point in the requirements stage (Collapse Point 1) is "user interviews don't surface real needs."

But the next essay isn't about "how to interview better"—it's about **"why AI product requirements no longer originate from user interviews"**—capability ceilings define requirement boundaries, not the other way around.

If you're still doing AI products on the traditional "interview → PRD → build" path—you've already taken a wrong turn.

See you in the next one.

---

> **Companion Resources**: Capability card template (editable) + 5-dimension DoD self-check + case visual library (paid readers)
> **Next Up**: 03 · AI Product Needs No Longer Come from User Interviews
> **Feedback / Reader Community**: WeChat Official Account 「蔡逸雯」

---

> **Reading the Chinese original?** See [02-from-features-to-capabilities.md](./02-from-features-to-capabilities.md)
> **Part of**: Season 1 · AI PM Workflow Reconstruction · 26 essays
> **Author**: Cai Yiwen (蔡逸雯) · 8 years in QE → AI PM
