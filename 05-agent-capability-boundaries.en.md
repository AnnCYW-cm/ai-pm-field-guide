# 05 · Agent Capability Boundaries—Requirements That "Look Buildable" But Aren't

> Season 1 · AI PM Workflow Reconstruction · Essay 5 · Part 1 Requirements

---

The fourth dismissive blind spot:

**90% of PMs think "what Agents can do is the engineer's problem, the PM doesn't need to understand it."**

It's not that PMs don't want to understand. It's that most PMs **think "kick off first, then let the engineer assess feasibility" is enough**—and 2 months after kickoff, the engineer tells you "can't be built," with the quarter's budget already burned.

By the end of this essay you'll see—Agents have **4 hard boundaries**. Cross any one of them, and the requirement shifts from "hard" to "unbuildable." **PMs must identify these 4 boundaries during the requirements stage**, or you'll be rolling back in launch week one.

---

## Part 1 · Workflow: The 4 Categories of Agent Capability Boundaries

### Boundary 1: Reasoning Depth

**Standard**: When single-step reasoning exceeds 3-4 logical hops, accuracy drops off a cliff.

What counts as a "hop"? Example:

- "Analyze this company's financials" = 1 hop
- "Compare this company's financials with competitors'" = 2 hops
- "Based on the comparison, judge which is better to invest in" = 3 hops
- "Based on the investment judgment, give a specific position sizing and exit strategy" = 4 hops

Each additional hop doubles the "working memory" required. After hop 3, the model starts **hallucinatory fusion**—it doesn't tell you it hasn't thought it through; it fabricates a plausible-sounding answer.

If your requirement "contains 4+ verbs in one sentence"—**you've basically crossed the reasoning depth boundary.**

**Response**: Split the requirement into multiple steps. Each step asks the model to reason 1-2 hops only. **Make the "chain" explicit.**

### Boundary 2: Tool-Call Complexity

**Standard**: More than 5 tool calls in sequence—basically don't do it.

This isn't pulled from the air. **Anthropic's own engineering data:**

- **58 tools consume ~55k tokens**
- As the tool pool grows, the model's probability of picking the right tool drops significantly
- **Official recommendation**: at 30+ tools you need Tool Search, or it collapses

A more precise estimate: per-step accuracy of picking the right tool is around 80%; **5-step end-to-end success probability is only 32.8%** (80%^5).

If your requirement "needs 5+ tools coordinating"—accuracy drops below 1/3. **That's not a product, it's gambling.**

**Response**: Either reduce the number of tools (merge / cut), or use Tool Search (let the model select a smaller pool before deciding), or split the multi-step flow into multiple independent Agents.

### Boundary 3: Long-Chain Planning

**Standard**: When task duration exceeds 30 minutes (human baseline), Agent failure probability rises exponentially.

METR's (an independent AI evaluation org) "horizon length" research series: the task duration frontier models can stably complete **doubles every 7 months.** Sounds optimistic, right?

But flip it—any long-chain task multiplies single-step error rates. Success rate at step N = p^N.

p = 95% (already high):
- N=10: 60%
- N=20: 36%
- N=50: 8%

That's why OSWorld (computer-use benchmark) numbers are so awkward:

- **OpenAI Operator (CUA) 38.1%**
- **Anthropic Computer Use 22.0%**
- **Human baseline 72.4%**

It's not that the model is weak—**it's that long-chain tasks demand per-step precision that current models can't deliver.**

**Response**: Don't build "fully automated" requirements. Build "AI completes 70% + human confirmation at critical nodes" hybrid flows.

### Boundary 4: Cross-System Coordination

**Standard**: When you need to coordinate data + operations across 3+ independent systems, it's near-certain to collapse.

Why? Because:
- Each system has a different data schema (need an adapter layer)
- Each system has different latency (need wait + retry)
- Each system has different failure modes (need separate handling)
- Data state isn't guaranteed consistent across systems (race conditions)

The PM sees "AI auto-executes tasks cross-system"; the engineer sees N unreliable components chained together—**any one collapses, the whole flow collapses.**

**Response**: Split cross-system requirements into "AI recommends + human executes." AI gives the plan, human clicks execute, every step has an audit log.

---

## Boundary Identification Workflow

Stringing the 4 boundaries together, here's how to judge at the requirements stage:

```
Step 1: Sketch the requirement as an Agent thinking chain
  → List every step from input to output
  → For each step annotate: reasoning hops / tool count / cross-system?

Step 2: Check the 4 boundaries one by one
  → Boundary 1: single-step reasoning ≤ 3 hops?
  → Boundary 2: total tool count < 5?
  → Boundary 3: human completion time < 30 minutes?
  → Boundary 4: cross-system count < 3?

Step 3: Any boundary crossed → design degradation
  → Reasoning depth crossed → split into multiple steps
  → Tool complexity crossed → use Tool Search or split Agents
  → Long chain crossed → add human confirmation nodes
  → Cross-system crossed → switch to "AI recommends + human executes"

Step 4: Re-evaluate after degradation
  → Does it still close the loop?
  → Does the economics still pencil?
  → If can't close loop → cut the requirement
```

**15 minutes through this saves 3 months of post-launch rollback.**

---

## Alternative: "Agent + Rules" Combined Degradation

When a requirement crosses a boundary, you have 3 alternatives.

### Option 1: Split into multiple independent Agents

Break "fully automated office Agent" into "auto-organize-email Agent" + "auto-schedule Agent" + "auto-write-weekly-report Agent"—3 independent Agents each handling a single task, **accuracy returns to a usable range.**

### Option 2: AI decides + rules execute

Use AI for the "judgment," use rules for the "execution."

Example: contract review—AI flags 20 common risk points (judgment), rules route by risk tier to different approval levels (execution). **If AI errs, nothing bad happens directly—rules backstop.**

### Option 3: Human in the loop

The Agent runs to a critical decision node, stops, waits for human confirmation, then continues.

Example: auto customer-service Agent handling refunds—AI judges "should refund," but the actual refund action requires human-click confirmation. **If AI mis-judges, no actual money moves.**

The common thread: **changing "AI autonomous" to "AI assisted."** This isn't a step back—it's responsibility.

---

### How the 4 Boundaries Will Shift in the Next 24 Months

The 4 boundaries above are a **2026-Q2 model snapshot**—not constants. A "boundary-shift cheat sheet" for the reader:

- **Reasoning depth 3 hops**: Anthropic's 2026 Outcomes (an independent grader judges whether each intermediate result meets bar; if not, auto-revise) is breaking the "single forward-pass working-memory ceiling"—**the 3-hop boundary may shift to 5-6 hops within 12 months.**
- **Tool calls 5 steps**: Tool Search has moved from paper to product. The 58-tools-consuming-55k-tokens pain is being bypassed in the Skills form factor—**Skills are small bundles loaded on-demand, the 5-step boundary will be replaced by "on-demand skill invocation" within 6 months.**
- **Long chain 30 minutes**: METR Time Horizon 1.1 (2026-01) shows doubling time has compressed from 7 months to 4.3 months. Claude Opus 4.6's single-task 50% horizon hit 14.5 hours; 2026-05 Claude Mythos reached 16 hours—**the "30 minutes" boundary will be outdated within the 12 months of this book's publication.**
- **Cross-system 3 systems**: Sub-agent + Memory + shared filesystem are turning "cross-system coordination" into "internal coordination among sub-agents"—it stops being a distributed-consistency problem.

What the reader takes away isn't "4 numbers"—it's **"re-test the boundaries every 6 months" as discipline.** A PM who doesn't re-test will train themselves on 2026-Q2 data and still be using it in 2028.

---

## Part 2 · Engineering Reality: Why These 4 Boundaries Exist

### Why a Reasoning-Depth Boundary Exists

LLM "thinking" is a one-shot forward pass—it can't iterate the way humans do. Chain-of-thought simulates a "thinking process," but it's still a token-generation pass.

Each additional reasoning hop linearly increases the intermediate token count. When token count exceeds the model's "working memory" (typically a 4K-8K effective reasoning window), **the model starts forgetting earlier steps.**

It won't tell you "I forgot," **it will fabricate a plausible bridge.** That's "hallucinatory fusion."

### Why a Tool-Call Complexity Boundary Exists

Anthropic's 2025-2026 engineering blogs spell it out: **58 tools consume ~55k tokens.** Meaning the model must "read through the tool list" before deciding on each call.

The more tools, the more interference. Anthropic's measurements: on Claude Opus 4.5, Tool Search raised accuracy from 79.5% → 88.1%—meaning without Tool Search, **the model's probability of choosing wrong in a big tool pool is close to 20%.**

5-step 80%-correct probability = 80%^5 = 32.8%. That's why "don't do 5+ steps."

### Why a Long-Chain Planning Boundary Exists

Partnership on AI's 2025 paper *Prioritizing Real-Time Failure Detection in AI Agents* lists "real-time failure detection" as the core proposition for long-Agent deployment—**the industry default is that Agents will fail.**

The paper's essential question: how do you know, when the Agent has run to step 30, that it has already gone off the rails? Answer—**you don't.** The Agent won't proactively tell you it got lost at step 12; it will keep fabricating until step 30 and hand you a plausible-looking but entirely wrong result.

That's why "the engineering aesthetic of long Agents isn't making them run further—it's having them obediently stop and ask for help at step 3."

### Why a Cross-System Coordination Boundary Exists

Cross-system coordination is fundamentally a distributed consistency problem—a problem computer science hasn't solved in decades. Asking the LLM to "solve" it is like asking a high schooler who routinely fumbles math problems to be your CTO.

Each additional system raises the state-inconsistency probability by an order of magnitude. Coordinating 3 systems = 8 possible state combinations = 8 corner cases. **LLMs cannot enumerate-handle these.**

---

## QE Lens on Agent Boundaries

**8 years in QE—I've seen the same pattern repeatedly:**

Any "looks fully automated" system has **one or more latent failure points.** An engineer's job is to find them, quantify them, monitor them.

The 4 Agent boundaries are essentially 4 classes of latent failure points:
- Reasoning depth boundary = working-memory failure point
- Tool-call complexity boundary = decision failure point
- Long-chain planning boundary = cumulative error failure point
- Cross-system coordination boundary = state consistency failure point

When a PM sketches an "Agent thinking chain" during requirements—it's essentially running one **FMEA (Failure Mode and Effects Analysis).** This is a baseline QE move that **the LLM world dropped—only because Agents "look like they can do anything," misleading people into thinking they can skip failure mode analysis.**

If your Agent-type PRD doesn't have the "4-boundary self-check" + "degradation path" sections—**you're not building an AI product, you're gambling.**

---

## Will Model Upgrades Eliminate These Boundaries?

Many PMs comfort themselves—"can't be done now, when the model upgrades it can."

**Partially right, partially wrong.**

**The right part**: each model generation upgrade improves single-step precision. METR data shows frontier models doubling task duration every 7 months.

**The wrong part**: the boundary is fundamentally an "exponential vs linear" race. **Model upgrades linearly improve single-step precision, but task complexity is exponentially compounded.**

Concrete numbers:
- Single-step precision from 80% → 90% only takes 5-step success from 32.8% → 59%
- Single-step precision from 90% → 95% only takes 5-step success from 59% → 77%

**What truly solves the problem is not model upgrades, it's product design degradation.**

What the PM needs isn't "wait for the model to get stronger," it's "**identify the boundary now and design degradation now.**"

---

## Manus AI's Real and Fake Moat

A final case study.

Manus (from Butterfly Effect) initially claimed GAIA benchmark SOTA, with valuation rumors in the multi-billion-USD range.

Early-2025 hands-on reviews from several technical media outlets converged on—
- Beautiful benchmarks
- But real issues with reliability, context window, paywall, and CAPTCHA blockers
- Frequent crashes

**Beautiful benchmarks, real tasks blocked by CAPTCHA.**

This is the composite expression of the 4 boundaries—long-chain planning collapse, cross-system coordination collapse, tool-complexity collapse.

**The key call**: Manus's "real moat" doesn't actually exist in the face of the 4 boundaries—benchmark SOTA ≠ production-usable, a common ailment of all Agent-type products.

---

## Your Action Checklist

#### Action 1: Sketch a thinking chain for every Agent-type requirement
- List every step from input to output
- For each step annotate: reasoning hops / tool count / cross-system?

#### Action 2: Run the 4-boundary checklist
- Reasoning depth ≤ 3 hops
- Tool count < 5
- Human completion time < 30 minutes
- Cross-system count < 3

#### Action 3: Any boundary crossed → design degradation
- Split Agents / AI-decide + rules-execute / human in the loop—pick one

#### Action 4: Write it into the PRD
- 4-boundary self-check results
- Degradation plan
- Backstop mechanism on failure

---

## Counter-Consensus Quotes

- **"Anthropic itself says you need Tool Search past 30 tools—if your Agent stuffs 50 tools into a single prompt, that's not an Agent, that's a mascot."**
- **"Operator scores 38 on OSWorld, humans 72—it's not that AI replaced humans, it's that AI got a failing grade and is still charging subscription fees."**
- **"The engineering aesthetic of long Agents isn't running further—it's stopping obediently at step 3 to ask for help."**

---

## Closing Thoughts

This essay covered "can we build it." The next essay is the last in the requirements section:

A stakeholder drops a requirement on you—**miss any one of 5 signals, and the requirement should be rejected.**

The next essay gives you the specific phrasing of the 5 signals + how to confirm each in the review meeting + how to handle missing signals.

After all 5 signals, the stakeholder either walks or has thought the requirement through.

See you in the next one.

---

> **Companion Resources**: Agent boundary self-check + long-chain degradation plan template (paid readers)
> **Next Up**: 06 · Identifying True vs False AI Requirements—5 Signals
> **Feedback / Reader Community**: WeChat Official Account 「蔡逸雯」

---

> **Reading the Chinese original?** See [05-agent-capability-boundaries.md](./05-agent-capability-boundaries.md)
> **Part of**: Season 1 · AI PM Workflow Reconstruction · 26 essays
> **Author**: Cai Yiwen (蔡逸雯) · 8 years in QE → AI PM
