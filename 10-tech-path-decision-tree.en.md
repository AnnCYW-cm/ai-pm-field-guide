# 10 · Tech Path Decision Tree — How to Choose Among RAG / Prompt / Agent / Fine-tune

> Season 1 · AI PM Workflow Reconstruction · Essay 10 · Part 2: Solutions
> Estimated length: 2,000 words

---

The ninth dismissive blind spot —

**90% of PMs jump straight to RAG / Agent / Fine-tune — skipping Prompt entirely.**

It's not that PMs love complexity. It's that most PMs **assume "advanced problems need advanced solutions"** — and 3 months later they discover the root cause of "RAG won't behave" was actually a prompt-design issue, **$40K and 3 months burned**.

After reading this essay you'll know — **RAG / Prompt / Agent / Fine-tune are not parallel options, they form a prioritized decision tree**. Choosing the wrong path costs far more than choosing the wrong model.

---

## Part 1 · Workflow

### The Essential Difference Between the 4 Paths

Each path solves a different problem:

| Path | Problem it solves | One-liner |
|------|------------|----------|
| **Prompt** | "Instruction understanding" | Tell the model what you want |
| **RAG** | "Missing knowledge" | Tell the model about your private data |
| **Agent** | "Process orchestration" | Let the model run multi-step tasks autonomously |
| **Fine-tune** | "Style / capability targeting" | Make the model output in your style |

**Confusing these 4 problems = wrong path = 3 months and ¥40K-100K of engineering wasted.**

### The Question Order of the Decision Tree

Apply the principle "the most complex option is the last resort":

```
Q1: Can Prompt solve it?
  → Try modifying system prompt + few-shot examples
  → Run 50 cases
  → Accuracy meets bar → Choose Prompt, done
  → Doesn't meet bar → Q2

Q2: Is it a knowledge gap?
  → Is the model wrong because "it doesn't know your private data"?
  → Yes → Choose RAG
  → No → Q3

Q3: Is it process orchestration?
  → Does the task require multi-step decisions + tool calls + non-enumerable branches?
  → Yes → Choose Agent
  → No → Q4

Q4: Is it style / capability targeting?
  → Need the model to output in a specific style? Or a dedicated capability?
  → Yes → Choose Fine-tune
  → No → Re-examine the requirement; it may itself be flawed
```

### Quick-Decision Rhyme

> **Prompt before Agent, RAG before Fine-tune**

These rhymes are grounded in cost + complexity:
- Prompt cost is lowest (rewriting text)
- RAG is medium (vector store + retrieval pipeline)
- Agent is high (multi-step calls + tool integration)
- Fine-tune is highest (data prep + training + maintenance)

**60% of problems you think need Fine-tune can actually be solved with Prompt.**

### Hybrid Path Design

Most production products combine **2-3 paths**:

```
Case: Enterprise smart customer service

Primary path: Prompt + RAG
  - Prompt defines persona, reply style, boundaries
  - RAG retrieves enterprise knowledge (product manuals, FAQs, order records)

Secondary path: Agent
  - User asks "process a refund" → Agent calls refund API
  - User asks "look up my order" → Agent calls order system

Avoided trap: No Fine-tune
  - Customer-service scripts change too frequently for fine-tuning to keep up
  - Solve style via Prompt + few-shot instead
```

---

## Part 2 · Engineering Reality

### Cost Analysis of Misapplication

#### Misuse 1: Forcing Agent when Prompt would do

Cost: **5× development overhead + 10× debugging overhead**.

Why? An Agent is a multi-step chain — every step can crash. A Prompt is single-step — one call.

Debugging a 5-step Agent is 50× harder than debugging a prompt. For every step you must:
- Read the trace
- Identify which step failed
- Decide if it's a prompt issue or tool issue
- Rerun the whole 5-step flow after each fix
- And it may still be wrong after the fix

If your requirement is just "have the model answer in a format" — **rewriting the system prompt is enough; don't build an Agent.**

#### Misuse 2: Forcing RAG when RAG can't solve it

3 problem classes that will crash if forced into RAG:
- **Style problems**: "Make answers more professional" — that's a prompt issue, not a knowledge issue
- **Instruction problems**: "Output in JSON format" — that's a structured-output issue
- **Logical problems**: "Reason through multiple steps" — that's a chain-of-thought issue

RAG only solves "missing knowledge." **Stuffing 10,000 documents into it cannot conjure instruction-following ability.**

#### Misuse 3: Fine-tune to "cure hallucinations" (the most expensive misconception)

**Fine-tune does not fix hallucinations.**

This is the counter-consensus IBM / Google Cloud / Anthropic docs repeat over and over.

Fine-tune changes "style / format / output tendency" — it **cannot teach the model new facts**. If the model doesn't know a fact, it still won't know after fine-tuning.

The only ways to teach the model "new facts" are RAG (dynamic knowledge injection) or online learning (live parameter updates, not supported by mainstream models today).

#### Misuse 4: "RAG = dump documents in a vector store and wire it to the model"

This implementation **fails 90% of the time**.

Causes:
- Bad chunk design (fixed-character splits destroy semantics)
- Bad retrieval quality (embedding model mismatched to domain)
- Generation paragraph mismatch (retrieved fragments don't answer the question)

**Doing RAG is not building a vector store, it's building a complete "chunk + retrieve + rerank + generate" pipeline.** Each stage requires its own eval.

### Real Misapplication Cases

#### Case 1: $40K fine-tune just to "cure hallucinations"

A team spent **$40K fine-tuning a model to cure hallucinations**, only to discover after the fact that the RAG layer would have solved it in **$800 and 2 weeks**.

**Lesson**: Rule out Fine-tune first (most expensive), then judge Agent (most complex), then Prompt vs RAG.

#### Case 2: 3 months on RAG, turns out to be a Prompt issue

A recurring industry pattern — team adopts RAG → tunes vector store → tunes reranker → tunes chunk size → tunes embedding model → 3 months later, still doesn't work.

Looking back at the system prompt, they hadn't actually said "answer must be grounded in provided context."

**Fixed the system prompt in 1 hour, hit the target instantly.**

#### Case 3: 5× the cost from forcing Agent

A "customer-intent classification" requirement that could have been done with Prompt was implemented as an Agent — split into "read input → call classifier API → call confidence API → decide → output" 5-step flow.

Development time went from 3 days to 3 weeks. Debug cost went from 5 cases to 50 cases. **Post-launch p99 latency went from 500ms to 3s.**

Eventually rolled back to a single-step Prompt classifier. **5× cost + 10× latency for identical results.**

---

## Reverse-Applicability of the 4 Paths

| Path | Use when | Don't use when |
|------|------|-------|
| **Prompt** | 60% of problems you think need fine-tune | You truly need new knowledge |
| **RAG** | Knowledge base changes / need provenance / internal data | The problem is "wrong style" not "wrong knowledge" |
| **Agent** | Genuine multi-step decisions + tool calls + non-enumerable branches | The flow can be written as if-else |
| **Fine-tune** | Style / format / domain-specific tone | You want the model to remember facts or cure hallucinations |

### Anthropic Prompt Caching Changed the Game

After Anthropic introduced prompt caching in 2024 — **the applicability of the Prompt path expanded dramatically**.

Previously, you needed fine-tune to make the model "remember" complex instructions — because system prompts got too long and every call was expensive.

Now you can put a super-long system prompt (5K-50K tokens) into the cache — cache-read price is only 1/10 of normal input.

**Implication**: Many scenarios that previously required fine-tune now work with Prompt + caching.

Example: Make the model reply to emails in your company's style → stuff 100 sample emails into the system prompt + cache → 10× cheaper than fine-tune + far more flexible to adjust.

---

## The 4-Path Decision Table

All dimensions in a single table:

| Dimension | Prompt | RAG | Agent | Fine-tune |
|------|--------|-----|-------|-----------|
| Problem solved | Instruction understanding | Missing knowledge | Process orchestration | Style targeting |
| Implementation cost | Low (1-3 days) | Medium (2-4 weeks) | High (1-3 months) | Very high (3-6 months) |
| Maintenance cost | Low | Medium | High | Very high (retrain on every model upgrade) |
| Debug difficulty | Low | Medium | High | Very high |
| Suitable stage | Any stage | Post-launch extension | Mature stage | Large scale + proprietary data |
| Failure rate | Low | Medium (complex pipeline) | High | Very high |
| Solo-author recommendation | ★★★★★ | ★★★★ | ★★ | ★ |

**Advice for solo / small teams**: 90% of scenarios use Prompt, 10% use RAG, **Agent and Fine-tune should almost never be touched**.

---

## QE Lens on the 4-Path Decision

**8 years in QE has taught me this** —

Any engineering problem should start by **validating the simplest solution first**. That's Occam's Razor applied to software engineering — **"do not multiply entities beyond necessity."**

Applied to the 4-path decision —
- Simplest is Prompt (rewrite text)
- Most complex is Fine-tune (retrain)

**Validate whether Prompt can solve it first** —
- Yes = save $40K + 3 months
- No = then consider the complex options

This isn't "cutting corners." It's a fundamental engineering action — **avoiding premature, unnecessary complexity.**

The industry counter-consensus: **60% of problems PMs think need Fine-tune can actually be solved with Prompt.** The underlying reason isn't that Prompt is magical — it's that the PM jumped to Fine-tune without honestly trying Prompt.

---

## Action Checklist

#### Action 1: Run every new requirement through the decision tree
- Q1 Prompt? → Q2 RAG? → Q3 Agent? → Q4 Fine-tune?
- Reverse order, not forward

#### Action 2: Stick "Prompt before Agent, RAG before Fine-tune" on your desk
- Reference in every review meeting
- When engineering says "we need Fine-tune" → counter-ask "have you tried Prompt + caching?"

#### Action 3: Check for 3 common misuses immediately
- "Fine-tune to cure hallucinations" → switch to RAG
- "RAG to change style" → switch to Prompt
- "Agent for an if-else flow" → switch to Prompt

#### Action 4: Evaluate prompt-caching applicability
- Is your system prompt > 1024 tokens?
- Reuse rate > 2 calls?
- Yes → adopt caching immediately (highest ROI path optimization)

---

## Counter-Consensus

- **"Forcing Agent when Prompt would do is like hiring a chauffeur to deliver takeout — not impossible, just won't survive your burn rate to PMF."**
- **"Fine-tune doesn't cure hallucinations — it just makes hallucinations sound more like internal jargon. That's the most dangerous engineering misconception of 2026."**
- **"Before deciding between RAG and Fine-tune, answer one question: 'Is your problem wrong knowledge or wrong style?' — get this wrong and you start at $40K."**

---

## Closing

This essay closes Part 2 (Essays 7-10) on Solutions.

You should now have a complete solution-design toolkit:
- Essay 7 — Draw the capability flow (not the feature flow)
- Essay 8 — Choose the model (good enough; don't default to "the strongest")
- Essay 9 — Calculate the token ledger (reverse-engineer the business model)
- Essay 10 — Choose the tech path (Prompt before Agent, RAG before Fine-tune)

Next we enter Part 3 — **PRD**.

The 5 essays in Part 3 are the hard-currency section of the column. The single biggest anxiety for working PMs is "how exactly do I write a PRD for an AI product?" — these 5 essays answer that head-on.

Essay 11 starts with the PRD skeleton — **what 4 sections to add and what 2 sections to cut from the traditional template**.

See you next essay.

---

## Next Up

**11 · PRD: 4 Adds, 2 Cuts — What to Add and What to Cut from the Traditional PRD Template**

## Companion Resources

Tech-path decision tree (interactive version) + 4-path misuse case collection (unlocked for paid readers).

## Feedback / Reader Community

WeChat Official Account 「蔡逸雯」

---

> **Reading the Chinese original?** See [10-tech-path-decision-tree.md](./10-tech-path-decision-tree.md)
> **Part of**: Season 1 · AI PM Workflow Reconstruction · 26 essays
> **Author**: Cai Yiwen (蔡逸雯) · 8 years in QE → AI PM
