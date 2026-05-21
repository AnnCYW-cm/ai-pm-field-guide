# 21 · Bad Case Management — The Mindset Shift from "Fixing Bugs" to "Tuning a System"

> Season 1 *PM Workflow Reconstruction in the AI Era* · Article 21 · Part V Operations
> Estimated word count: 5000

---

The 20th "dismissive blind spot"—

**90% of PMs' first reaction to fixing a bad case is "tweak the prompt".**

It's not that PMs want to slack. It's that most PMs **assume "AI bad cases are like traditional bugs — fix and you're done"**—then they fix 10 bad cases and introduce 20 new ones, **because a traditional bug is "fix and you're done", but an AI bad case is "fix and you might make it worse".**

By the end of this article you'll know—**traditional PMs fix bugs like fixing plumbing; AI PMs fix bad cases like tuning a piano—pluck one string and every other string sings back.**

---

## Part 1 · Workflow

### The 5-Step Bad Case Management

#### Step 1: Discover

Sources:
- Monitoring alerts (Article 20's 4 AI-specific categories)
- User-initiated feedback
- Customer service / operations tagging
- Automated eval failures

**Key**: build a bad case collection pipeline—route every channel into a single pool.

#### Step 2: Reproduce

Every bad case must be **reproducible locally** before it can be fixed.

Cases that can't be reproduced:
- Incomplete screenshots / screen recordings / traces
- Lost context
- Inaccurate user description

**Response**: build a standardized bad case submission template:
```markdown
## Bad Case Report
- Time:
- User ID (anonymized):
- Full input:
- AI output:
- Expected output:
- Severity (Tier 1-4):
- Trace ID (for local reproduction):
```

#### Step 3: Classify (the critical step)

**Classification determines the fix path.**

The 5 classes + their corresponding fix strategies:

| Bad Case Type | Typical Symptom | Fix Strategy |
|--------------|----------------|--------------|
| Hallucination | Fabricates facts that don't exist | Add RAG / add grounding / change prompt to emphasize "if unsure say I don't know" |
| Refusal | Refuses to answer what should be answered | Change prompt / adjust safety filter |
| Format Error | JSON parsing fails | Use structured output / add retry with format hint |
| Off-topic | Answer doesn't match question | Adjust system prompt boundary / add intent recognition |
| Safety Violation | Outputs prohibited content | Add content filter / change system prompt red lines |

**The same bad case may belong to multiple classes**—classification determines the fix path.

#### Step 4: Fix

Choose 1 of 4 fix strategies:
1. **Tweak the prompt**: cheapest, fastest
2. **Add an eval case**: ensure this case can't recur
3. **Change the product design**: avoid at the root (e.g. add disclaimer / hand off to human)
4. **Degrade to a rule**: AI never does this in this scenario

**Counter-consensus**: 90% of PMs reflexively reach for "tweak the prompt"—most of the time it should actually be "**change the product design**" or "**degrade to a rule**".

Example: a user asks "can you write me a prescription?"—
- Tweak prompt (try to make AI answer more safely) → no, the boundary will always be at risk
- Add eval cases → no, the case space is infinite
- Change product design → ✅ Explicitly state "AI does not provide medical advice, please consult a doctor"
- Degrade to a rule → ✅ Detect medical keywords, hand off directly to human

#### Step 5: Regression (mandatory)

After a fix, what you must do—**prevent "fix A, break B"**.

Concretely:
- Run the full historical case set
- Compare pre-fix vs. post-fix
- Any case regressed > 5% → the fix doesn't count as successful
- Regressed cases must be root-cause-analyzed ("why did fixing A cause B to regress")

---

## Industry Bad Case Management SOP

### Hamel Husain "Field Guide to Rapidly Improving AI Products"

Industry-grade SOP, 5 steps:

> 1. **Hand-look at 20-50 traces per fix iteration**
> 2. **Write a custom data viewer (don't use a dashboard)**
> 3. Cluster errors → define failure modes
> 4. Write an eval per failure mode
> 5. Make the eval set a CI gate

**Hamel's principle**: "**until you stop finding new failure modes**"—you stop when no new failure mode appears, not after some fixed number of traces.

Meaning—looking at traces isn't "look at 5 that seem similar", it's looking **until no new failure types keep emerging**. Only then is the review done.

### Anthropic's Two-Layer Approach: Constitutional AI + Constitutional Classifiers

These are two different methods—you need to unpack them separately:

**Constitutional AI (2022, training-phase method)**:
- Give the model a set of "constitutional principles"
- Have the model self-critique / rewrite based on the principles
- Use RL to optimize alignment

**Constitutional Classifiers (2025, inference-phase method)**:
- Add a classifier at inference time
- Red-team challenges + discover fringe cases + iterate the classifier
- The new version refuses less + is more robust + runs cheaper

**What the PM learns**: bad case fixing **is not changing one prompt, it's changing the "evaluation criteria"**—change the constitution at training, change the classifier at inference, **let the system itself learn to rewrite**.

### The Notion Prioritization Framework

The practice: score cases by "**users impacted × frequency × severity**".

Each feature defines its own judge—avoiding the situation where one broad indicator masks the regression of a single sub-capability.

---

## Part 2 · Engineering Reality

### Why It's No Longer "Fixing a Bug"

Traditional bugs:
- Causality is clear
- Fix impact is bounded
- Fix doesn't introduce new bugs (if reviewed carefully)

AI bad cases:
- **Causality is murky** (one prompt line can affect 100 scenarios)
- **Fix impact is global** (changing system prompt affects all calls)
- **Fixing one likely introduces new bad cases** (this is "fix A, break B")

Example. A customer-service AI gets dinged in refund scenarios as "too rigid".

The PM changes the system prompt: "**respond with more empathy**".

Week 2, new problems appear—
- In "system-failure apology" scenarios the AI over-blames itself, promising compensation it can't deliver
- In "rule reminder" scenarios it's too gentle and the user misses the rule
- In "refund refusal" scenarios the empathetic tone gives users the illusion that "it's negotiable"

**Change one prompt → affect every scenario.**

### The "Contagion" of Bad Cases

Bad cases of the same kind tend to **appear in waves**—not as isolated incidents.

Why? Because AI models handle similar inputs similarly. One case going wrong means all similar inputs could go wrong.

**Response**:
- Find 1 bad case → actively hunt for siblings
- E.g. discover "AI oversteps in medical consultation" → actively find all "health-related" cases
- Fix one whole class together; don't single-point fix

### Priority of Fix Strategies

Not every bad case is worth fixing. Score with the Notion framework:

```
Priority score = users impacted × frequency × severity
```

Example:
- Case A: 5% of users × high frequency × medium severity = **high priority**
- Case B: 0.1% of users × low frequency × high severity = medium priority (but severity demands a fix)
- Case C: 30% of users × high frequency × low severity = **high priority** (large volume)
- Case D: 0.01% of users × extremely low frequency × low severity = **don't fix**

**Counter-consensus**: many PMs treat every bad case as equally urgent—result: **resources scattered across low-ROI work**.

---

## "Fix A, Break B" Textbook Cases

### OpenAI GPT-4o sycophancy (2025-04) ⭐

**Event**: in pursuit of "friendlier" conversation, the model was trained into pleasing users and agreeing with harmful decisions (even agreeing with stopping medication, even agreeing with terror plans).

**Key**: OpenAI itself admitted—"**sycophancy was not included as a blocking item in the release evaluation**." Several testers "felt something was off" but had no mechanism to stop the release on that feedback.

**Post-fix**: officially written in—"**behavior issues must be able to block release**".

**Takeaway for PMs**: any change "to optimize a specific metric" must check "will it cause other metrics to regress".

### Gemini Image Generation Over-tune (2024-02)

**Event**: to fix "insufficiently diverse output", over-tuning led to forcing 1800s US senators and Nazi soldiers into diverse depictions, and the model became excessively refusal-prone.

CEO Pichai publicly wrote that it was "unacceptable".

**Takeaway for PMs**: **fixing bias** easily becomes **reverse bias**—fixing a bad case must include considering the risk of "over-fixing".

### Academic Record

An arxiv paper explicitly states "**generalized prompt improvements cause format drift on extraction tasks and reduce citation-compliance rates in RAG**"—it's a pattern industry sees repeatedly.

---

## A Bad Case Management Failure Mode

A pattern industry sees repeatedly—

PM fixes 5 bad cases in week 1 → 10 new ones surface in week 2 → fixes 10 in week 3 → 20 new ones surface in week 4.

**Root cause**: every fix only changed the prompt. No looking at traces, no classification, no regression. The "fix A, break B" loop intensifies.

The right approach is Hamel's 5-step SOP—**look at traces first, classify, choose the fix strategy with the smallest blast radius, then run regression.**

---

## QE Lens: Bad Case Management = Tuning a System, Not Fixing a Bug

**Eight years in software QE talking—**

Bug fixing in any complex system follows one principle: "**root-cause analyze first, then make the minimal change**".

Traditional software bug causal chains are short—"minimal change" usually means "edit this one line of code".

AI product bad case causal chains are long (prompt → model → context → user input → output)—"minimal change" usually isn't "tweak the prompt"—it's "**change the evaluation criteria**" (change eval) or "**change the product design**" (change flow).

**The 90% PM reflex to tweak prompt is essentially mistaking "complex-system tuning" for "code bug fixing".**

The right mindset: **tuning a system is not fixing a bug**. Look at traces, classify, judge root cause, choose the fix with the smallest blast radius—this is the basic move of quality engineering.

---

## Action Checklist

#### Action 1: Build a bad case collection + classification pipeline
- 5 classes (hallucination / refusal / format / off-topic / safety)
- Each class maps to a different fix strategy

#### Action 2: Hand-look at 20-50 traces per fix iteration
- Hamel's industry baseline
- Don't "look at 5 that seem similar"

#### Action 3: After a fix, you must run full regression eval
- Regressed > 5% → fix failed
- Don't "fix and ship"

#### Action 4: Order with the Notion prioritization framework
- Users impacted × frequency × severity
- High priority first; low priority can wait a quarter

---

## Counter-Consensus Lines

- **"Traditional PMs fix bugs like fixing plumbing; AI PMs fix bad cases like tuning a piano—pluck one string and every other string sings back."**
- **"Hamel Husain's principle: every prompt change requires re-looking at traces; only when no new failure modes keep appearing do you earn the right to stop error analysis—this is industry baseline, not academic ideal."**
- **"OpenAI itself admitted the root cause of the GPT-4o crash: sycophancy was not a blocking gate at release. So if your product doesn't have a 'behavior-risk veto', sooner or later you're due an April-29-style full rollback."**

---

## Closing

This article covered Bad case management. The next covers—**The PM's Courage Checklist: When You Must Degrade to a Rule**.

Degrading isn't failure—it's **being responsible**.

The next article covers 4 scenarios where you must degrade + 4 real degradation cases (Klarna / Air Canada / McDonald's / Illinois state law) + 3 sentences to explain degradation to your boss.

See you in the next one.

---

## Next Up

> **Next**: 22 · When You Must Degrade to a Rule — The PM's Courage Checklist

## Companion Resources

> **Article companion assets**: Bad Case Management 5-step workflow + classification checklist + Notion prioritization template (paid subscriber unlock)
> **Feedback / Reader Community**: WeChat Official Account 「蔡逸雯」

---

> **Reading the Chinese original?** See [21-bad-case-management.md](./21-bad-case-management.md)
> **Part of**: Season 1 · AI PM Workflow Reconstruction · 26 essays
> **Author**: Cai Yiwen (蔡逸雯) · 8 years in QE → AI PM
