# 04 · "Should AI-ify vs Shouldn't AI-ify" Judgment Framework—What 90% of Pseudo-AI Needs Look Like

> Season 1 · AI PM Workflow Reconstruction · Essay 4 · Part 1 Requirements

---

The third dismissive blind spot:

**90% of PMs, when a stakeholder drops an "AI-ification requirement" on them, immediately think "how do I build this," not "should this be built at all."**

The stakeholder says: "Can our workflow be done with AI?"—a sentence that hasn't stopped since the birth of AI products.

The dismissive PM catches it directly—starts ideating solutions, estimating timelines, scheduling engineer reviews.
The PM who sees the trap asks 3 questions first—**after these 3 questions, half the stakeholders walk away, but the requirements that remain can definitely be built.**

By the end of this essay you'll see—**90% of "AI-ification requirements" dumped on PMs' desks are false propositions.** This isn't hyperbole. The MIT 2025-08 report verified: **95% of enterprise GenAI projects show zero measurable return.**

---

## Part 1 · Workflow: The 3-Dimension Judgment Framework

### Dimension 1: Business Value (ROI Check)

First question to the stakeholder:

> "If we build this, what concrete, quantifiable return does it bring our company?"

Listen to how they answer.

**Real-need answers:**
- "Save X customer-service FTEs, ¥X/month in savings"
- "Conversion lifts from X% to Y%, +¥Z in annual revenue"
- "Contract review compresses from 3 days to 1 hour, signing speed up X times"

**Pseudo-need answers:**
- "Makes our company more intelligent"
- "Keep up with the AI era"
- "The boss said so"
- "Customers are asking if we have AI"

If you hear any pseudo-need answer—**dimension 1 fails**, send it back.

This isn't being hard on the stakeholder. **AI requirements without ROI numbers can't be built**—per the MIT NANDA report's core finding: failure is not technology, it's that "**systems don't capture feedback, don't adapt to context, don't continuously improve**"—fundamentally because stakeholders treat AI as one-time delivery, not ongoing investment.

### Dimension 2: Tolerance for Error (Negative-Feedback Cost)

Second question:

> "If the AI gets this wrong once, what happens?"

Listen.

**Real-need answers:**
- "User asks again, no big deal"
- "Our ops team backstops, workload manageable"
- "System auto-falls-back to rules"

**Pseudo-need answers:**
- "We have medical compliance, can't be wrong"
- "Finance scenario—one mistake could cost hundreds of thousands"
- "Legal advice—one wrong piece of guidance means a penalty"
- "One mistake and the customer files a complaint"

**The key call**: requirements where one-time error cost > 100 correct-answer benefits—**cannot be put on AI.**

Stanford RegLab + HAI 2024-2025 gave hard data: "AI legal research tool" hallucination rates—**Lexis+ AI 17%, Westlaw AI-Assisted Research 33%, GPT-4 43%.** All of these claim "hallucination-free / RAG-backed."

Imagine using a 17-43% hallucination tool to help draft contracts. The cost of one mistake is lawyer indemnification + customer churn. **The ROI is permanently negative.**

"AI legal advice," "AI medical diagnosis," "AI contract review"—the three categories stakeholders keep tossing at you—**90% are pseudo-needs.**

### Dimension 3: Data Availability (Ground Truth)

Third question:

> "How do we judge whether the AI's answer is right? Who labels? How many labels?"

Listen.

**Real-need answers:**
- "We have 1000+ historical reference answers, we can build evals"
- "Our ops label 50 per day, in 3 months we'll have 4500"
- "There's a public benchmark in the industry we can borrow"

**Pseudo-need answers:**
- "Our experts have a sense of it"
- "Labeling is too expensive, let's have GPT self-label first"
- "Right and wrong aren't that absolute, business understanding is enough"
- "Let's build first, set the standard as we go"

**The key call**: **no ground truth = can't do AI.**

A 2025 MIT MedRxiv paper on medical AI hallucination concluded: "LLM hallucinations, because they use 'professional vocabulary + coherent surface,' **are actually the hardest to detect.**" **Ground truth must be clinicians + real cases, not GPTs grading each other.**

Academically, Lebovitz / Levina / Lifshitz-Assaf's MISQ paper *Is AI Ground Truth Really True?* nails it: uncertainty in expert know-what labeling causes "high benchmark scores / production collapse."

If the stakeholder can't answer where ground truth comes from—**dimension 3 fails.** Send them back to think it through.

---

## How to Use This in a Review Meeting

3 questions, in order.

### After Q1 (business value)
- Clear answer → proceed to Q2
- Vague answer → "Please go back to the CFO and bring me an ROI number"

### After Q2 (tolerance for error)
- Low one-time error cost → proceed to Q3
- High one-time error cost → "Suggest 'AI-assist + human backstop'—AI can't decide independently"

### After Q3 (ground truth)
- Clear source → **build**, proceed to kickoff
- No ground truth → "Build the labeling pipeline first, re-review in 3 months"

After 3 questions, half the stakeholders walk. **But the requirements that remain can definitely be built.**

---

## Script for Declining a Stakeholder

A stakeholder who gets rejected will push back. That's normal.

Don't say "we can't do it." Say "**you'll regret doing it.**"

**Sample script:**

> "Director Zhang, we could absolutely build this, but I'd recommend not building it.
>
> First reason—the negative-feedback cost in this scenario is too high (cite the Air Canada case: the bot fabricated a non-existent bereavement-fare policy, the BC tribunal ruled the airline must pay CAD 650.88 (~USD 480), and the precedent now applies globally to airlines).
>
> Second reason—we have no ground truth. Once built, you have no way to judge right or wrong, and **this project will turn into 'AI team and business team blaming each other.'**
>
> Third reason—with the same resources, we could build [recommend a real need], which can show revenue inside 3 months.
>
> Whether to build is not a technical decision, it's a business decision. **If you get it wrong, you're burning your own budget.**"

70% of stakeholders accept this. The 30% who insist anyway—**that's a real need.** They have information you don't.

---

## Part 2 · Engineering Reality: The 3 Typical Shapes of 90% Pseudo-AI Needs

### Type 1: High-Determinism Needs Mis-classified

The most common.

Stakeholder sees a workflow: "**User submits order → system calculates shipping → returns result.**" Wonders, "Can this be done with AI?"

No.

This workflow is 100% deterministic—same input always yields same output. **Rules are more reliable, cheaper, more interpretable.**

Forcing AI here is hiring a GPU cluster to do addition. Triple loss: performance waste + cost waste + interpretability loss.

A piece in China's PM circles gave a localized 4-feature test: "**Fuzzy rules / dynamic evolution / massive variables / human-experience dependency.**" Requirements that touch none of the four shouldn't be force-AI-ified.

Memorize it. Next time a stakeholder drops a requirement at review, ask yourself 4 questions:
- Are the rules of this workflow fuzzy?
- Will the rules evolve dynamically?
- Are the input variables so massive they can't be enumerated?
- Does this workflow depend on human-experience judgment?

If not a single "yes"—**`if-else` beats AI 10 times over.**

### Type 2: Negative-Feedback Cost Too High

Medical, legal, financial—one wrong answer outweighs a thousand right ones.

Plus one more often overlooked—**heavy compliance scenarios.**

The NYC MyCity government chatbot is a textbook counter-example. The chatbot launched by the city government told small businesses:
- "You can take employees' tips" (violates federal labor law)
- "You can refuse Section 8 tenants" (violates NY anti-discrimination law)
- "You can refuse cash" (violates 2020 NYC law)

The Markup investigation exposed it; controversy continues.

**This kind of requirement should be cut at the PRD stage.** Not because AI capability is insufficient—because compliance risk is unbounded.

When the stakeholder says "our risk team can handle it"—reply: "Air Canada also thought they could argue 'the chatbot is an independent legal entity' and got slapped down in court. **What the bot says is what the company says.**"

### Type 3: Long-Tail Distribution Out of Control

The third pseudo-need type is the most insidious—80% of cases easy, 20% destroy the product.

McDonald's × IBM drive-thru AI order is the representative case. 100+ store pilot for 2 years; social media full of "wrong orders / cross-lane orders / can't be undone." **85% accuracy, 1 in 5 orders needs human backstop.**

But think it through—in fast food, 85% equals 100% rollover.

Why? Because the 15% of failure cases all happen in front of the user. Every wrong order gets filmed and posted to TikTok. **Long-tail-out-of-control AI products have no "small mistakes"—every mistake is a PR incident.**

In June 2024 McDonald's announced the termination of the IBM partnership and reverted entirely to human ordering.

How to judge this category—**ask the stakeholder "what's the long-tail failure rate?" + "will failure cases be visible to users?"**

If "long-tail failure rate > 5% + user-visible"—**don't build it.**

---

## QE Lens on the Common Thread Across 90% Pseudo-Needs

**8 years in QE—I've seen too many "looks reasonable, actually unbuildable" requirements.** AI products just amplify it 10x.

The **common root cause** across the 3 pseudo-AI types: stakeholders wrap a fundamentally **probabilistic system** in **deterministic thinking:**

- Type 1: wraps "AI can do this workflow" deterministic expectation over "this workflow doesn't need AI at all"
- Type 2: wraps "AI shouldn't make mistakes" deterministic expectation over "AI will always make mistakes"
- Type 3: wraps "85% accuracy is good enough" deterministic thinking over "long-tail failures will spread"

**The essence of the 3-dimension framework is to use the QE lens to strip away the 'deterministic wrapping'—exposing the stakeholder's pseudo-needs to the truth of probability distributions.**

---

## A Few Authoritative Citations

### MIT NANDA *State of AI in Business 2025*
- **95% of enterprise GenAI projects show zero measurable return**
- Core cause is not technology, not compliance, not talent
- It's "systems don't capture feedback, don't adapt to context, don't continuously improve"

### Gartner 2025 GenAI Hype Cycle
- GenAI has formally entered the **Trough of Disillusionment**
- Average enterprise 2024 GenAI spend: **$1.9M**
- **< 30% of CEOs satisfied with returns**

### a16z 2025 enterprise study
- Enterprise LLM budgets expected to grow another ~75% in a year
- **74% of CEOs list AI as top priority, only half believe spending will pay off**

The three data points together say one thing—**the false-proposition rate among AI-ification requirements is terrifyingly high**, and PMs must have the courage to decline in the review meeting.

---

## Your Action Checklist

#### Action 1: Print the 3 questions and pin them to your desk
- Business value: what's the quantifiable ROI?
- Tolerance for error: what's the cost of one mistake?
- Ground truth: how do we know if AI's answer is right?

#### Action 2: Run every new requirement through all 3
- No "skipping" allowed
- Stakeholder can't answer → go back and think

#### Action 3: Maintain a "rejected requirements" log
- Review monthly
- Six months later look back—the share rejected correctly should be > 70%

#### Action 4: Run a "3-dimension framework" training for your boss and stakeholders
- 30-minute deck
- Teach stakeholders to self-vet
- Review meeting efficiency triples

---

## Counter-Consensus Quotes

- **"The most expensive AI-era requirement isn't the one users ask for—it's the one executives raise in the boardroom."**
- **"If a requirement could be solved by `if-else` and you used a GPU cluster, that's not AI-ification, that's performance art."**
- **"In 2024 Klarna's CEO loudly announced AI had replaced 700 customer-service FTEs; in 2025 he publicly admitted 'AI lacks empathy' and started rehiring—the first headline made the news, the rollback made the news too."**

---

## Closing Thoughts

This essay covered "should we build it." The next covers "can we build it."

The stakeholder says a requirement "should" be built—you've cleared 3 dimensions. But some requirements **sound buildable and engineering-wise are not.**

Especially for Agent-type requirements—4 hard boundaries, cross any one, and the need shifts from "hard" to "unbuildable."

The next essay gives you fast-judgment standards for the 4 boundaries—**you'll be able to identify, in the requirements stage, whether an Agent's "thinking chain" will collapse.**

See you in the next one.

---

> **Companion Resources**: 3-dimension decision tree + script template for declining stakeholders (paid readers)
> **Next Up**: 05 · Agent Capability Boundaries—Requirements That "Look Buildable" But Aren't
> **Feedback / Reader Community**: WeChat Official Account 「蔡逸雯」

---

> **Reading the Chinese original?** See [04-pseudo-ai-needs.md](./04-pseudo-ai-needs.md)
> **Part of**: Season 1 · AI PM Workflow Reconstruction · 26 essays
> **Author**: Cai Yiwen (蔡逸雯) · 8 years in QE → AI PM
