# 19 · Pre-launch Eval Checklist — The One Pass Every PM Must Run Before Ship

> Season 1 *PM Workflow Reconstruction in the AI Era* · Article 19 · Part IV Delivery
> Estimated word count: 5000

---

The 18th "dismissive blind spot"—

**90% of PMs only run core-case eval before launch.**

It's not that PMs are lazy. It's that most PMs **assume "if the core cases pass, ship should be fine"**—then on day 3 you get a DPD-style faceplant. **Core eval passing ≠ production stable. Missing one eval category is enough to crash the product.**

By the end of this article you'll know—**before launch, the PM must personally run the full pre-launch eval. All 5 categories, no skipping.**

---

## Part 1 · Workflow

### The 5 Pre-launch Eval Categories

#### Category 1: Core Case Coverage (most important)

**What to test**: Your core capabilities' pass rate on 50-200 real tasks.

**Minimum bar**:
- ≥ 50 cases per core capability
- Pass rate ≥ business-defined launch threshold (e.g. 90%)
- Coverage: 60% normal + 30% edge + 10% adversarial

**How to run**:
- L1 unit tests (run in CI)
- L2 full eval set (manual + LLM judge)
- See the Eval chapter template in Article 12

#### Category 2: Performance (Latency + Concurrency)

**What to test**: Model latency and concurrency behavior under real load.

**Minimum bar**:
- P50 latency ≤ business commitment (e.g. 2s)
- **Watch the P99/P50 ratio** (industry typically 2-4×; > 5× warrants investigation)—don't only look at P50
- Concurrency can hold 2× expected peak

**How to run**:
- Use Locust / k6 or similar load tools
- Simulate real traffic distribution (not uniform)
- Test spike scenarios (sudden 10× traffic)

#### Category 3: Cost

**What to test**: Per-call cost + monthly budget estimate + top 1% user spend.

**Minimum bar**:
- Per-call cost ≤ what you wrote in the PRD
- Monthly budget estimate ≤ ARR × 30%
- Top 1% user spend ≤ 5× the average (else hard cap required)

**How to run**:
- Run 1,000 calls to profile token-usage distribution
- Compute monthly cost estimate
- Configure a monthly budget hard cap

#### Category 4: Adversarial (Malicious Input)

**What to test**: Resistance to prompt injection / jailbreaks / coercion / edge cases.

**Minimum bar**:
- 50+ adversarial cases
- Prompt-injection defense rate ≥ 95%
- Jailbreak resistance rate ≥ 90%
- Catastrophic outputs (violence / sexual / illegal) must be blocked 100%

**How to run**:
- Use red-team tools like PromptArmor / Lakera
- Write 20 of the most common adversarial patterns yourself
- Have 1-2 security engineers review

#### Category 5: Regression (Historical Cases)

**What to test**: This release didn't break historical cases.

**Minimum bar**:
- Pass rate on the historical case set doesn't drop
- No matter how sexy the new feature is, **old cases cannot regress**
- Regressed cases > 5% → block the release

**How to run**:
- Run regression eval automatically every release
- Integrate into CI
- Auto-block PRs that exceed the threshold

### The Full Pre-launch Eval Checklist

```markdown
## Pre-launch Eval Checklist

### Day -7: Core eval
[ ] All L1 unit tests pass
[ ] L2 full eval pass rate ≥ X%
[ ] Every core capability hits its bar

### Day -5: Performance eval
[ ] P50 latency ≤ X ms
[ ] P99 latency ≤ X ms
[ ] Concurrency peak passes

### Day -3: Cost eval
[ ] Per-call cost ≤ ¥X
[ ] Monthly budget estimate ≤ ¥X
[ ] Hard cap configured

### Day -2: Adversarial eval
[ ] 50+ adversarial cases, pass rate ≥ 95%
[ ] Catastrophic outputs 100% blocked
[ ] Security engineer review complete

### Day -1: Regression eval
[ ] Pass rate on historical cases doesn't drop
[ ] No case regressed > 5%

### Day 0: Launch
[ ] Canary 5% → 24h monitoring
[ ] Canary 20% → 24h monitoring
[ ] Canary 50% → 24h monitoring
[ ] Full rollout

### Day +7: Post-launch review
[ ] Real traffic vs. forecast
[ ] Actual cost vs. budget
[ ] Add newly discovered bad cases to the eval set
```

Walk this checklist and—you sleep at night.

### PM Runs It vs. Engineer Runs It—Division of Labor

**The PM must personally run**:
- Category 1 core cases (the PM understands the business bar best)
- The business-specific portion of Category 4 adversarial eval (the PM understands the scenarios best)

**The engineer runs**:
- Category 2 performance (load testing)
- Category 3 cost (token accounting)
- Category 5 regression (CI automated)

**Reviewed jointly**:
- The technical portion of Category 4 adversarial eval (prompt injection)
- The final ship decision

### What If It Doesn't Pass — Delay or Degrade?

**Case 1: Core case pass rate below bar**
→ Delay launch, go back and fix prompt / swap model

**Case 2: Performance below bar**
→ Degrade launch (cheaper model + simplified prompt) or delay

**Case 3: Cost over budget**
→ Add hard cap + degradation path. **Launch is OK.**

**Case 4: Adversarial eval below bar**
→ **Must delay**—this is the compliance and PR risk floor.

**Case 5: Regression eval shows > 5% degradation**
→ Must fix before launching.

---

## Part 2 · Engineering Reality

### The Boundary Between Automated and Manual Eval

What must be manual? What can be automated?

#### Must be manual
- Subjective judgment (tone / style / creativity)
- High-stakes domains (medical / legal / financial)
- Newly-emerged failure modes (label, then train the LLM judge)

#### Can be automated
- Format validation (JSON schema / field types)
- Factual validation (against gold answers)
- State validation (was the task completed?)
- Safety filtering (toxicity / bias)

### Hamel Husain's Cost-Structure Advice

```
- CI on each commit: run cheap code-based graders (cost ~ zero)
- Preview / production evaluation: use LLM-as-judge (expensive but strong)
- Manual eval: reserved for "judge alignment" and "contested edge cases"
```

**Workflow taught in the Maven course**:
- Label 100-200 examples manually first
- Train the LLM judge to align with human
- Then scale up

### The Chasm: "Eval Passed ≠ Production Stable"

The single most counter-intuitive thing—**passing eval ≠ stable in production.**

3 real-world gap cases:

#### Case 1: DPD Chatbot (2024-01)

UK courier company chatbot—pre-launch eval passed, **but no regression eval after the update**.

UK musician Ashley Beauchamp coaxed it into swearing and writing poetry about "DPD is the world's worst courier", **a single tweet hit millions of impressions on X**.

**Lesson**: Pre-launch eval passing ≠ still stable post-update. **Every update must rerun regression eval.**

#### Case 2: NYC MyCity Bot (2024)

New York City government's small-business chatbot gave illegal operating advice (telling users to take employee tips, to discriminate against certain groups).

**Eval did not cover "regulatory correctness"**—pre-launch eval passed, but the eval dimensions simply didn't include compliance.

**Lesson**: **Eval dimensions must cover every business-critical dimension.** Missing one dimension = a launch crash.

#### Case 3: Air Canada Moffatt Case (2024-02)

The bot wrongly promised bereavement discount could be claimed retroactively. The Civil Resolution Tribunal ruled the airline must pay **CAD 650.88**.

It explicitly held **a company cannot defend itself by claiming "the chatbot is an independent legal entity"**.

**Eval did not cover "policy consistency"**—the bot invented a policy that didn't exist.

**Lesson**: **RAG / knowledge-base products must have a "factual provenance" eval dimension.**

---

## Post-Launch Must-Do: Add New Bad Cases Back into the Eval Set

The first week post-launch you will discover new bad cases—this is the AI product norm.

What the PM must do:
1. Review the day's bad cases daily
2. Add them to the eval set immediately (within 24h)
3. Auto-run them in regression next release
4. Label "added to eval" or "pending add"

**The eval set is alive, not a one-shot pre-launch artifact.**

See Article 13 on EDD's core idea—**eval evolves alongside the product**.

---

## QE Lens: Pre-launch Eval = 5 Insurance Lines Before Launch

**Eight years in software QE talking—**

Any mature industrial system has **5 lines of insurance** before going live—functional verification + performance verification + safety verification + fault-tolerance verification + regression verification.

The 5 Pre-launch Eval categories are exactly the AI-era version of these 5 insurance lines—
- Core case coverage = functional verification
- Performance (latency + concurrency) = performance verification
- Adversarial (malicious input) = safety verification
- Cost = fault-tolerance verification (avoiding runaway bills)
- Regression = regression verification

Skip any one of these 5 lines = launch faceplant. **This is a basic principle of 60 years of industrial reliability engineering.**

The LLM crowd threw these insurance lines away—just because "AI looks flexible" people assume they can skip. **The result: DPD's millions-of-views tweet + NYC MyCity teaching people to break the law + the Air Canada legal precedent.**

---

## Action Checklist

#### Action 1: Print the 5-category checklist and stick it on your desk
- Run each release through all 5 categories item by item
- Any category below bar → pause release

#### Action 2: PM personally runs Categories 1 + 4
- Don't dump everything on the engineer
- The engineer runs the cases you weren't present for; the PM runs the cases you were

#### Action 3: Build a "post-launch bad case → eval" pipeline
- Must be added within 24h
- Auto-run in next release's regression
- Monthly review of new additions

#### Action 4: Print the 3 gap cases (DPD / NYC MyCity / Air Canada) on the wall
- Self-check before every release
- "Have our eval dimensions been fully covered?"

---

## Counter-Consensus Lines

- **"Eval passing ≠ production stable. The DPD update wiped out the guardrails—the lesson of millions of impressions in one tweet is free."**
- **"Skip the eval before launch and the post-launch payout will buy you 10 years of LLM judge."**
- **"Air Canada wanted to defend with 'the chatbot is an independent legal entity'—the court slapped it down on the spot: what your bot says is what you say."**

---

## Closing

This article closes the Delivery section (Articles 16-19).

By now you should have a complete AI-product delivery capability:
- Article 16—72h MVP (closing the demo-capability loop)
- Article 17—PM using Claude Code (the killer app)
- Article 18—Multi-axis canary strategy
- Article 19—Pre-launch Eval 5-category checklist

The next article enters Part V—**Operations**.

Operating AI products is **completely different** from traditional products—monitoring metrics change, bad case management changes, and the courage to degrade is a PM core skill.

Article 20 first covers AI-product monitoring metrics—**beyond the traditional funnel, you must watch 4 AI-specific metric categories.**

See you in the next one.

---

## Next Up

> **Next**: 20 · AI-Product Monitoring Metrics—Beyond the Traditional Funnel, What Else to Watch

## Companion Resources

> **Article companion assets**: Pre-launch Eval 5-category checklist + minimum bars per category + 3 gap cases self-check (paid subscriber unlock)
> **Feedback / Reader Community**: WeChat Official Account 「蔡逸雯」

---

> **Reading the Chinese original?** See [19-pre-launch-eval.md](./19-pre-launch-eval.md)
> **Part of**: Season 1 · AI PM Workflow Reconstruction · 26 essays
> **Author**: Cai Yiwen (蔡逸雯) · 8 years in QE → AI PM
