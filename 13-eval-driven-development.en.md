# 13 · Eval-Driven Development — Letting the Eval Set Drive the Entire Dev Process

> Season 1 《Rebuilding the PM Workflow for the AI Era》· Chapter 13 · Part Three: PRD (the Hard Goods of this Column)
> Target length: ~5,000 words

---

The twelfth "dismissive blind spot" —

**90% of teams are still "writing code first, adding evals later."**

It's not that engineers are lazy. It's that most teams **believe "evals are an acceptance step before launch"** — and end up halfway through coding without anyone able to articulate "what does done look like," with PMs and engineers shoving blame at each other for three weeks.

By the end of this chapter you will know — **EDD (Eval-Driven Development) is not a change of testing method, it's a change of development philosophy.**

Chapter 12 covered the "operational layer" — how to write an Eval section.
**This chapter covers the "philosophical layer" — how to drive the entire dev process with evals.**

---

## Part 1 · Workflow

### EDD in Three Steps

#### Step 1: Define the eval first (not the code)

Traditional flow: write PRD → write code → test → ship.
EDD flow: **write PRD → write eval → write code → run eval → ship.**

**Eval comes before code.**

**Anthropic's official guidance** (codified in their documentation):

> "We recommend practicing eval-driven development: **build evals to define planned capabilities before agents can fulfill them**, then iterate until the agent performs well."

Translation: write the eval first to define "what does done look like" — then let the agent / model iterate until it meets the bar.

The counter-consensus in this ordering — **eval is a design tool, not a verification tool.**

#### Step 2: Use evals to define "done"

The core of EDD is using evals to force the PM to think clearly about the requirement.

**If the PM can't write an eval — the PM hasn't thought clearly about what "good" means.**

Example:
- Fuzzy ask: "make the AI agent smarter"
- EDD challenge: "what are the eval dimensions? what's the pass bar?"
- PM is forced to clarify: "ticket-resolution rate ≥ 90% / average turns ≤ 5 / user satisfaction ≥ 4.2"
- **Now it's an executable requirement.**

EDD turns a "fuzzy product idea" into "measurable engineering targets."

#### Step 3: Use evals to drive iteration

Code written → run eval → didn't meet bar → modify prompt / architecture / model → run eval → met bar → ship.

**Key difference**: traditional is "implement to spec," EDD is "**converge to eval**."

Engineers don't need the PM to constantly interrupt with "this case is wrong" — they run the eval themselves and find out.
The PM doesn't need the engineer to keep asking "does this count as good now?" — the eval pass bar settles it.

The entire dev process becomes **asynchronous** — PM writes evals, engineer iterates implementation, CI runs evals for feedback.

### Landing EDD in a Team

```
PM ─────► writes PRD + eval set ("what does done look like")
   │
   ├─► AI Engineer ─► picks model / writes prompt / wires tools
   │      │
   │      └─► runs eval (auto in CI)
   │            │
   │            ├─► passes → next stage
   │            └─► fails → modify implementation → re-run eval
   │
   └─► Eval Engineer ─► maintains eval set / writes LLM-as-judge / trains graders
          │
          └─► continuously extends evals (new bad case → new eval case)
```

**Triangular collaboration**: PM-AI Engineer-Eval Engineer replaces the traditional PM-RD-QA triangle.

See Chapter 25 on AI-Native team-building for the details — but remember the core insight here: **Eval Engineer is becoming a standalone role**. Anthropic / OpenAI are publicly hiring Eval-related EMs with base bands reaching $300K+. Netflix is hiring "Software Engineer L4/L5, LLM Evaluation & Infrastructure." **In China, the role is still hidden behind the title "AI Test Engineer," but the essence is the same.**

### Where EDD Doesn't Apply

EDD is not a silver bullet. Three classes of scenarios don't fit:

#### Doesn't apply 1: Very early exploration
Capability boundaries are unknown. At this point you don't know what to evaluate — because you don't even know what the model can do.

**Response**: spend a week on a "capability probe" (see Chapter 3) to map the model's limits. Write evals once you know.

#### Doesn't apply 2: Pure-creative scenarios
"Write a poem that moves the reader" — the eval criterion is intrinsically subjective.

**Response**: replace automated evals with A/B tests + user feedback. But **hard constraints** (no porn, no violence, correct rhyme) still need evals.

#### Doesn't apply 3: Last-minute pre-launch patching
"We're about to ship, let's tack on some evals" — this isn't EDD, it's an eval after-the-fact patch.

**True EDD has evals before code.** After-the-fact patching is "evals as documentation," not "evals as development."

---

## EDD Three-Step Flow

```
       PM wants to ship an AI feature
              │
              ▼
   ┌─── Step 1: Write Eval ───┐
   │  - 3-5 eval dimensions    │
   │  - 20-50 starter cases    │
   │  - Pass bar defined       │
   └──────────┬─────────────────┘
              │
              ▼
       PM can't write the eval?
       ├─ Yes → requirement unclear, go back and think
       └─ No  → continue
              │
              ▼
   ┌─── Step 2: Design Capability ───┐
   │  - Engineer picks model/path     │
   │  - Writes v1 prompt              │
   └──────────┬─────────────────────────┘
              │
              ▼
   ┌─── Step 3: Run Eval ───┐
   │  - CI runs automatically │
   │  - Passes → ship         │
   │  - Fails → iterate impl  │
   └─────────────────────────┘
```

---

## EDD vs TDD Comparison

| Dimension | TDD | EDD |
|---|---|---|
| What is tested | Code function (deterministic) | Model capability (probabilistic) |
| Pass criterion | All pass / fail | Pass rate ≥ X% (distribution) |
| Eval form | Unit-test code | YAML / JSONL + grader |
| Failure causes | Code bug | Prompt wrong / model weak / data biased |
| Fix method | Modify code | Modify prompt / swap model / add data |
| Iteration rhythm | Write code → write test → run | Write eval → write impl → run |
| Validates the unknown? | TDD verifies known logic | EDD defines unknown capability |

**Most critical difference**: **TDD verifies the known, evals define the unknown.**

TDD assumes "I know what the code should do, I write tests to verify it did so."
EDD assumes "I don't know how well the model can perform, I write evals to define how well I want it to perform."

---

## Part 2 · Engineering Reality

### The Engineering Reality of EDD: Evals Are "Alive"

Many teams treat evals as a one-time deliverable on their first EDD pass — finish before launch, ignore after.

**That's turning EDD into "pre-launch eval-patching" — which isn't EDD, it's an after-the-fact patch.**

True EDD: evals evolve with the product, continuously maintained.

Every new bad case appears → add to the eval set → run regression on the next release.
Every model upgrade → run evals to verify no regression → decide whether to switch.
Every prompt change → CI runs evals → automatically decides merge-ability.

The industrial-grade SOP Hamel Husain gives in *"Field Guide to Rapidly Improving AI Products"*:

> "Hand-review at least 20-50 traces per change; write a custom data viewer (don't use dashboards); cluster errors → define failure modes; write one eval per failure mode; turn the eval set into a CI gate."

### QE Inversion: The Fundamental Difference between EDD and Traditional QA

**From 8 years in software quality engineering** —

EDD is actually an **inverted version of QA thinking.**

| Dimension | Traditional QA | EDD (QE inverted) |
|---|---|---|
| What is tested | Known logic (verify code is correct) | Unknown capability (define model performance) |
| When written | After code | **Before code** |
| Written for | QA themselves | **PM + Engineer + Eval Engineer**, shared |
| Goal | Find bugs | **Force the requirement to be clarified** |
| Feedback target | Engineer | **The PM themselves** |

Traditional QA: "you wrote this wrong" — pointing at the engineer.
EDD: "did you think this through?" — pointing at the PM.

**EDD turns QA from "nitpicker" into "requirement-converger."**

This is why Anthropic positions its Eval team as the "**bridge between model capability and product experience**" — a bridge between product and research teams, not after-the-fact reviewers.

### The Common Anti-Pattern: Turning EDD into After-the-Fact Patching

A recurring failure mode in the industry —

The team accepts the concept of EDD, but the landing is distorted:
- Week 1: PM writes requirements → engineer develops
- Week 4: launch pressure mounts, evals start being written
- Week 5: run evals, find 60% of cases failing
- Week 6: emergency prompt fixes → case fixes → re-run → re-fix

**This isn't EDD — it's "eval as documentation"** — evals are just pre-launch documents tacked on, not a driver of development.

Correct EDD: in Week 1 the PM writes the eval, in Week 2 the engineer develops against it, **in Week 3 if eval pass rate isn't met → the engineer modifies, not the PM.**

---

## Hamel's "EDD Isn't New" Counter-Consensus

The origin of the term EDD —

**Hamel Husain (Oct 2024)**:

> "**EDD was always front and center pre-generative AI. Ex: nobody cares about your fraud/churn/forecasting model if it's not accurate. This is missing with most LLM products. But the best practices and playbooks are there.**"

Translation: **EDD has been core ML common sense long before generative AI.** Nobody cares about an inaccurate fraud/churn model. The LLM product world dropped this discipline, but the best practices were always there.

**Key framing**: EDD isn't a new term. It's an old practice transplanted from traditional ML engineering into LLM products. The "newness" is only that the LLM crowd forgot it.

---

## The Essence of BMAD / Spec-Driven Development

EDD isn't the only AI dev methodology. Two more are worth knowing:

### BMAD-METHOD

⚠️ Important correction: BMAD stands for "**Breakthrough Method of Agile AI-Driven Development**" (per the bmad-code-org/BMAD-METHOD GitHub repo's official README).

Core practices:
- Split the LLM into multiple specialized Agent roles (Architect / PM / Developer)
- Each role has bounded context
- The Developer Agent is defined as an "obedient craftsman" — when a requirement conflicts with the architecture, it **must halt and report**

**Relation to EDD**: BMAD leans toward "multi-agent collaboration flow," EDD leans toward "quality assurance." They compose — BMAD splits roles → each role converges with EDD.

### Spec-Driven Development (GitHub Spec Kit)

Open-sourced in Sep 2025:

> "Specifications become executable, directly generating working implementations rather than just guiding them."

Flow: `/specify` → `/plan` → `/tasks` → `/analyze` → executed by Claude Code / Copilot / Gemini CLI.

**Relation to EDD**: Spec-Driven leans toward "code generation," EDD leans toward "quality evaluation." **Combined**:
- BMAD splits roles
- Spec Kit writes specs
- EDD validates quality

This is the most advanced AI dev methodology stack as of 2026.

---

## Action Checklist

#### Action 1: Run your next project in EDD three-step order
- Step 1 — write eval first (not PRD)
- Step 2 — engineer designs implementation against the eval
- Step 3 — CI runs eval, driving iteration

#### Action 2: Every new bad case goes straight into the eval set
- Don't "do it later"
- Add same day, run on next release

#### Action 3: Turn the eval set into a CI gate
- PRs auto-run evals
- Score below baseline → block merge
- This is engineering-grade EDD

#### Action 4: Use EDD to force "fuzzy requirements" out
- Stakeholder says "make the AI smarter" → reply "what are the eval dimensions?"
- Stakeholder says "improve user satisfaction" → reply "what's the pass bar?"
- Can't write an eval = requirement isn't clear

---

## Counter-Consensus Punchlines

- **"Hamel Husain cuts to the truth: 'EDD is not a new invention. It's the old ML rule the LLM crowd forgot. Nobody cares about an inaccurate fraud model — but the LLM product world somehow tolerates it.'"**
- **"The fundamental difference between EDD and TDD: TDD tests determinism (pass/fail), EDD tests probability distribution. Testing an LLM as if it were a function — that's the root cause of crashing on day one."**
- **"QA thinking didn't disappear. It got inverted — traditional QA points at the engineer and says 'you're wrong,' EDD points at the PM and says 'did you think this through?'"**

---

## Closing

This chapter covered the EDD philosophy. The next chapter returns to the operational layer with PRD Chapter 6 — **Bad Case Grading and Degradation Strategy**.

Bad Cases are not "handled after launch" — they must be graded and have degradation strategies written in the PRD. **Microsoft Responsible AI Standard v2 + Anthropic ASL four levels + OpenAI Model Spec three layers — all three industry standards unpacked.**

See you next chapter.

---

## Next Up
**14 · Writing Bad Case Grading and Degradation Strategy into the PRD.**

## Companion Resources
**EDD three-step flowchart + EDD vs TDD comparison + BMAD/Spec-Driven composition guide** (paid subscribers unlock).

## Feedback / Reader Community
WeChat Official Account 「蔡逸雯」.

---

> **Reading the Chinese original?** See [13-eval-driven-development.md](./13-eval-driven-development.md)
> **Part of**: Season 1 · AI PM Workflow Reconstruction · 26 essays
> **Author**: Cai Yiwen (蔡逸雯) · 8 years in QE → AI PM
