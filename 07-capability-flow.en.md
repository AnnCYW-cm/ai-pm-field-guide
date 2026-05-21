# 07 · The Paradigm Shift in AI Product Solution Design — From Function Flow to Capability Flow

> Season 1 · AI PM Workflow Reconstruction · Essay #7 · Part 2: Solutions
> Estimated length: 2100 words

---

The sixth dismissive blind spot —

**90% of PMs still use "function flow diagrams" to review AI products.**

It's not that PMs don't want to switch diagrams. It's that most PMs **assume "whether the diagram changes isn't that important — it'll get approved either way"** — the result is engineers silently redraw a "capability flow diagram" in their heads before coding, **tripling communication cost**, and post-launch you discover "everything the diagram didn't say is broken."

After reading this essay you'll know — **Traditional PMs draw function diagrams (button A → page B → API C); AI PMs draw capability diagrams (Capability 1 + Capability 2 + Capability 3 = user experience). The paradigm shift begins with the drawing.**

---

## Part 1: Workflow

### Function Flow vs Capability Flow: Visual Comparison

**A function flow diagram** looks like this:

```
[User login] → [Enter query] → [Click search button]
            → [Return results list] → [Click detail] → [Display detail page]
```

Each arrow is a deterministic transition. Each box is a deterministic feature.

**A capability flow diagram** looks like this:

```
[User input]
    ↓
[Intent recognition capability] (accuracy 92%, p99 latency 800ms, unit cost ¥0.003)
    ↓
[Route by intent]
    ├→ [Information retrieval capability] (recall 85%, depends on GPT-5)
    │       ↓
    │   [Answer generation capability] (depends on retrieval result, hallucination rate < 3%)
    │       ↓
    │   [Confidence judgment]
    │       ├→ High confidence → return directly
    │       └→ Low confidence → fallback to human
    │
    └→ [Action execution capability] (tool calls ≤ 3 steps)
            ↓
        [Failure detection]
            ├→ Success → return result
            └→ Failure → retry 1× → fail → fall back to rules
```

**Fundamental differences**:
- Function flow annotates **transition relationships**; capability flow annotates **capability + reliability + cost + degradation paths**
- Each function flow box is deterministic; each capability flow box is **a probability distribution**
- Function flow can be drawn in PowerPoint; capability flow requires annotation-friendly tools (Notion / Excalidraw / Mermaid)

### How to Draw a Capability Flow Diagram in 4 Steps

#### Step 1: Identify Core Capabilities

Decompose requirements into minimum capability units. Each capability must satisfy:
- Single responsibility (does one thing only)
- Clear IO (what's input, what's output)
- Independently evaluable (has its own evals)

Example: "Auto-summarize meeting notes" decomposes into:
- Speech-to-text capability
- Speaker diarization capability
- Key point extraction capability
- Summary generation capability
- Action item extraction capability

**5 independent capabilities, not 1 "auto-summarize meeting notes" feature.**

#### Step 2: Annotate Capability Reliability

Next to each capability, annotate 3 numbers:
- **Accuracy** (eval result based on 100+ cases)
- **p99 latency** (how long the slowest 1% of requests take)
- **Unit cost** (¥/call)

If you can't fill in these 3 numbers — this capability **isn't ready to be drawn yet**. Go back and run a capability probe first (Essay #3).

#### Step 3: Annotate Capability Dependencies

Explicitly draw which capabilities depend on which.

Example: Summary generation depends on speech-to-text output → if transcription is wrong, summary is necessarily wrong.

**Dependency relationships determine failure propagation paths** — when an upstream capability errors, downstream capabilities error along with it.

#### Step 4: Annotate Capability Degradation Paths

Next to each capability, annotate "what happens if it fails":
- Retry N times
- Fall back to a cheaper model
- Fall back to rules
- Fallback to human
- Throw an error and ask the user to retry

Every capability must have a degradation path. **A capability with no degradation path = guaranteed crash post-launch.**

---

## Running a Solution Review Meeting with Capability Flow Diagrams

The script in a traditional function-diagram review meeting:

> PM: "Click button A here jumps to page B."
> Engineer: "OK, when do you need it done?"

The script in a capability-flow review meeting:

> PM: "Here we call the intent recognition capability. Accuracy 92%, the wrong 8% go through fallback. p99 latency 800ms, on timeout falls back to rules. Unit cost ¥0.003, at 100K MAU monthly cost is ¥X."
> Engineer: "OK, how is the 92% accuracy measured? How big is the eval set?"
> PM: "200 cases, 3 independent labelers, IRR ≥ 0.85."
> Engineer: "Got it, let's build."

**Fundamental difference between the two reviews**:
- Function-diagram review discusses "**when will it be done**"
- Capability-diagram review discusses "**what does done-and-acceptable look like**"

**The second kind of discussion is what actually closes the loop on an AI project.**

---

## Part 2: Engineering Reality

### Reality 1: Why Function Flow Diagrams Mislead on AI Products

The base assumption of function flow diagrams: **deterministic systems**.

Every box, every arrow defaults to 100% working. If something fails, it's a bug — to be fixed.

The substrate of an AI product is a **probabilistic system**. Every capability has a failure probability. **Failure isn't a bug, it's the norm.**

Function flow diagrams render a probabilistic system as a deterministic one — **they hide the most important design variables of AI products**: reliability distribution, cost distribution, latency distribution.

The engineer looks at the function diagram while mentally calculating "how many retries for this arrow, what reliability for this box, where does timeout degrade to" — **they're silently redrawing a capability diagram in their head**.

If you hand them the capability diagram directly — you and they are looking at the same diagram from the start. **Communication cost drops to 1/3.**

### Reality 2: Capability Reliability, Cost, and Latency Must Be Measured Independently

Traditional PM estimate:
> "This feature will take about 2 weeks."

One number.

AI PM estimate:
> "Intent recognition capability accuracy 92% / p99 800ms / cost ¥0.003.
>  Information retrieval capability recall 85% / p99 1200ms / cost ¥0.005.
>  Answer generation capability hallucination rate < 3% / p99 2000ms / cost ¥0.012."

**3×3 = 9 numbers.**

Why? Because **capability reliability / cost / latency cannot be "bundle-estimated" like a feature**. Each capability has a completely different bottleneck — intent recognition might be latency-bound, answer generation might be cost-bound, information retrieval might be recall-bound.

**Bundle estimation = hiding the true bottleneck.** Post-launch you discover "oh, it was answer generation cost that blew up" — by then it's too late.

### Reality 3: Coupling Between Capabilities Is an Engineering Reality

Optimizing capability A may degrade capability B. **This is not a bug, it's engineering reality.**

#### Academic backing
An EMNLP 2024 paper on the RLHF alignment tax measured it directly: when OpenLLaMA-3B's preference alignment reward rose from 0.16 to 0.35 — SQuAD F1 **dropped 16 points**, DROP F1 **dropped 17 points**, WMT BLEU **dropped 5.7**.

"Safety capability up = translation / reading comprehension capability down" **is quantifiable**.

#### Industry confirmation
The Cursor team publicly acknowledged: **after Claude 3.7 was post-trained on Claude Code, coding rose significantly but general capability dropped**.

#### Design implication
A capability flow diagram must be able to express this coupling. Suggested drawing convention —
- Use **dashed lines** to connect capabilities that "interact with each other"
- Annotate "if you optimize A, B may drop X%" on the dashed line
- Discuss in the review meeting: "are we willing to sacrifice B for A?"

**If your capability flow diagram has no dashed lines — your solution design ignores the hardest engineering reality of AI products.**

---

## QE Lens on Capability Flow Diagrams

**8 years doing software Quality Engineering, I've seen one pattern repeat** —

Any complex system's design diagram needs to annotate 3 things: **failure mode, blast radius, mitigation**.

A capability flow diagram is essentially the **failure mode visualization** of an AI product —
- Each capability's "accuracy 92%" = annotating the failure mode
- Each capability's "dependency relationship" = annotating the blast radius (A goes down, B goes down too)
- Each capability's "degradation path" = annotating the mitigation

Traditional software design diagrams have these 3 things too, but because deterministic systems have fewer failure modes, people got used to omitting them.

**AI products amplify failure modes from "a few edge cases" into "the norm of a probability distribution" — so capability flow diagrams must explicitly draw these 3 things.**

Not drawing them = your design diagram reverts to the deterministic-system level of 20 years ago, unable to handle the complexity of the AI era.

---

## Industry Status of "Capability Flow Diagrams": No Unified Term Yet

Honest disclosure — **the industry currently has no unified "capability flow diagram" term or template**.

Anthropic has Claude Design philosophy (progressive disclosure), Cursor has the "engine vs car" framing, Anthropic's AI-First Dev workflow has plan / act / review three phases — **these are all related methodologies, but no one calls it a "capability flow diagram"**.

What this column tries to do — **stitch the scattered methodologies from Anthropic / Cursor / OpenAI into a workflow Chinese PMs can use directly**.

If you accept this framing — the action checklist below is usable immediately.

---

## Your Action Checklist

#### Action 1: Convert the function flow diagram in your next solution doc into a capability flow diagram
- Draw in Excalidraw / Mermaid / Notion
- Annotate 3 numbers per capability (accuracy / latency / cost)
- Annotate a degradation path per capability

#### Action 2: 30 minutes before the review, draw it yourself
- See which capabilities you can't annotate the 3 numbers for
- The ones you can't annotate — engineers will grill you on the spot
- Run a capability probe in advance

#### Action 3: Speak from the capability flow diagram in the review
- Don't say "click here, jump there"
- Say "we call capability X here, accuracy X%, the wrong ones go through fallback Y"

#### Action 4: Make the capability flow diagram a core chapter of the PRD
- Replaces the traditional "function flowchart" section
- Sits alongside the evals chapter, bad case tiering chapter, degradation strategy chapter, cost budget chapter

---

## Counter-Consensus Quotes

- **"In the world of function flow, the PM draws wireframes; in the world of capability flow, the PM draws model inference diagrams — these are not the same job in different skin, they are two different professions."**
- **"The side effects of traditional products are written in the bug list; the side effects of AI products are written in another capability's score dropping 17 points."**
- **"Every time you add a capability, first ask: will this capability 'fight with someone'? This is the first question of an AI PM's review meeting, not the last."**

---

## Closing Thoughts

This essay was about how to draw the diagram. The next essay covers model selection —

**Model selection isn't "pick the strongest." It's making explicit trade-offs across the four dimensions of cost / latency / effect / compliance.**

The next essay gives you the latest 2026 mainstream model comparison table (Claude Opus 4.7 / GPT-5.5 / Gemini 3 / DeepSeek V3.2 / Kimi K2.6, etc.), with precise data per model on all 4 dimensions.

More importantly — it tells you real selection cases like "**dropping from GPT-4 to Claude Haiku cuts cost 90% while losing only 3% effect**."

See you in the next essay.

---

> **Companion Resources for this essay**: Capability flow diagram template (editable Excalidraw + case gallery) (paid readers unlock)
> **Next up**: 08 · Model Selection Across 4 Dimensions — How to Weigh Cost / Latency / Effect / Compliance
> **Feedback / Reader Community**: WeChat Official Account 「蔡逸雯」

---

> **Reading the Chinese original?** See [07-capability-flow.md](./07-capability-flow.md)
> **Part of**: Season 1 · AI PM Workflow Reconstruction · 26 essays
> **Author**: Cai Yiwen (蔡逸雯) · 8 years in QE → AI PM
