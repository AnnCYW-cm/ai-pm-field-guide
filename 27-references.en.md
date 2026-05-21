# References Index · The Complete Citation List for Season 1's 26 Essays

> Season 1 *AI-Era PM Workflow Reconstruction* · Companion asset · References index
> Author: Cai Yiwen (WeChat Official Account 「蔡逸雯」)
> **Version: v1.1** (initial public release 2026-05-21 · 9 highest-frequency URLs verified) · Remaining URLs being filled in

---

## About this index

This document lists every external citation used across Season 1 — version-hardening + a pointer set for readers who want to dig.

**Overview**: ~35 KOL public statements + 15 third-party reports + 24 industry incidents + 21 open-source / public standards + several sets of model vendor data.

### ⚠️ Current status (v1.1 launch)

**Done**:
- ✅ Source-type classification of all 95 citations (5 categories)
- ✅ Essay number + line range for every appearance in the season
- ✅ Source domain / platform / report name tagged
- ✅ **The 9 highest-frequency citations — verified, official URLs filled** (the cross-essay highest-exposure citations: Air Canada / GPT-4o sycophancy / Cursor billing / Hamel Field Guide / OpenAI Model Spec / Microsoft RAI v2 / Cat Wu Lenny Podcast / Klarna 2024 + 2025 reversal)
- ✅ Critical sources cross-validated (official + authoritative third-party)

**Ongoing**:
- ⏳ Concrete URLs for the remaining 80+ citations (v1.2 — top 50 within 1 month / v2.0 — all 95 within 3 months)
- ⏳ Citations whose URL is dead → marked at the end of the table with "URL dead, search by domain + keywords"

**Commitment**:
- Paid readers automatically receive v1.1 / v2.0 updates
- Every citation can be located by "appearance + source domain" — Google should find it within 5 seconds

### Reader covenant

- Every citation comes from a public source (public talks / blogs / podcasts / academic papers / earnings calls / regulatory filings / news reports)
- Each citation can be located by essay number + line range in this index, so you can dig deeper
- Citations qualify as fair use — commentary citation + author attribution + does not substitute for the original

---

## Category 1: KOL Public Statements (~35)

### 1.1 Hamel Husain (independent AI evals consultant, Maven course co-instructor)

**Quote A**: "Writing good evals is becoming the defining skill for AI PMs."
- Appears: 01 L236-244 / 12 L16
- Suggested source: Lenny Newsletter 2025 / Maven course "AI Evals For Engineers & PMs"
- [URL: pending]

**Quote B**: "EDD was always front and center pre-generative AI. Ex: nobody cares about your fraud/churn/forecasting model if it's not accurate."
- Appears: 12 L290 / 13 L216-224 / 13 L285
- Suggested source: hamel.dev / Twitter @HamelHusain (2024-10)
- [URL: pending]

**Quote C**: "Field Guide to Rapidly Improving AI Products" SOP — hand-look at 20-50 traces per fix iteration / write a custom data viewer / cluster errors → define failure modes / write an eval per failure mode / make the eval set a CI gate / "until you stop finding new failure modes"
- Appears: 12 L130 / 13 L173-176 / 18 L140-148 / 21 L99-112 / 21 L268
- Source: https://hamel.dev/blog/posts/field-guide/ (Hamel official blog)

**Quote D**: 3-layer Eval framework — L1 (Unit Tests) / L2 (Human & Model Eval) / L3 (A/B Testing); 60-80% of dev time spent on error analysis and evaluation; binary scoring not 5-point
- Appears: 12 L108-141
- Suggested source: Hamel × Shreya Shankar Maven course material
- [URL: pending]

### 1.2 Cat Wu (Anthropic Claude Code Head of Product)

**Quote A**: "Prototypes over PRDs"
- Appears: 01 L122-128 / 11 L160 / 25 L194
- Source: https://www.lennysnewsletter.com/p/how-anthropics-product-team-moves (Lenny's Podcast, Cat Wu episode, 2026-04-23)

**Quote B**: Anthropic's product team — "why faster than everyone else" — PM/Designer/Eng all use Claude Code to ship working prototypes into review, not Figma + docs
- Appears: 17 L242-244
- Source: same as above

**Quote C**: Product Note 3-pointer — "Prototypes over PRDs" / "Spec-first" / "Daily user sentiment loop"
- Appears: 24 L192-199 / 25 L190-204
- Source: same as above

### 1.3 Mike Krieger (Anthropic CPO, former Instagram co-founder)

**Quote**: PM no longer writes a 10-page PRD — writes a 3-4 paragraph Product Note (user intent + expected result + concrete metrics), backed by two context files `product_area_context.md` + `code_context.md`; an orchestrator composes the Functional Spec, the PM becomes "Editor-in-Chief" reviewing PRs
- Appears: 01 L118-128 / 11 L150-158
- Suggested source: Lenny's Podcast Mike Krieger episode
- [URL: pending]

### 1.4 Boris Cherny (Anthropic Claude Code lead)

**Quote**: Since 2025-11, 100% of code written by Claude Code; he no longer hand-codes; Anthropic's internal workflow prototypes first then dogfoods
- Appears: 01 L134 / 17 L238-241
- Suggested source: Lenny's Podcast Boris Cherny episode
- [URL: pending]

### 1.5 Sachin Rekhi (formerly LinkedIn / Reforge instructor)

**Quote**: In a large PM-facing webinar, demonstrated 10+ self-built skills — customer interview synthesis / NPS autonomy / no-SQL EDA / product strategy critique / release notes automation; produced an "AI Prototyping Mastery Ladder" (Apprentice / Journeyman / Master)
- Appears: 01 L134-138 / 17 L233-237
- Suggested source: Sachin Rekhi public webinar recordings + Reforge course pages + sachinrekhi.com
- [URL: pending]

### 1.6 Aparna Chennapragada (Microsoft CPO)

**Quote**: "Prompt sets are the new PRDs." + "a prompt set is a living artifact, half-spec, half-training-data"; traditional PRDs are "written for programmers, lock requirements up-front then deliver", but AI products are intrinsically non-deterministic
- Appears: 01 L202-208 / 11 L194-199
- Suggested source: Lenny's Podcast Aparna Chennapragada episode
- [URL: pending]

### 1.7 Marty Cagan (SVPG)

**Quote**: "Product discovery is judgement — AI can automate delivery, but discovering unmet needs and validating value can't be automated."
- Appears: 01 L176-180 / 03 L170-174
- Suggested source: svpg.com 2025 articles
- [URL: pending]

### 1.8 Teresa Torres (Product Talk)

**Quote**: "Customer interviews themselves have to change. In an AI product, outcomes are not deterministic — the interview can no longer ask 'what do you want', it has to log traces / human-review / tag error types / write evals / A/B test fixes."
- Appears: 03 L175-180
- Suggested source: Teresa Torres 2025 webinar / Product Talk blog
- [URL: pending]

### 1.9 Kevin Weil (OpenAI CPO)

**Quote**: Quarterly roadmaps and annual strategy no longer reflect the real shipping cadence — roadmap redefined as "rolling bets"
- Appears: 03 L181-184
- Suggested source: Lenny Newsletter citation set / Kevin Weil interviews
- [URL: pending]

### 1.10 Anton Osika (Lovable founder)

**Quote**: "Our number of PMs is 0 — the engineers are doing the PM work"
- Appears: 25 L76
- Suggested source: Lovable founder interviews / Twitter @antonosika
- [URL: pending]

### 1.11 Satya Nadella (Microsoft CEO)

**Quote**: "as much as 30% of our code is now written by AI"
- Appears: 25 L80 / L246
- Suggested source: Microsoft 2025-04 earnings call transcript
- [URL: pending]

### 1.12 Sundar Pichai (Google CEO)

**Quote A**: "We were able to lower Gemini serving unit costs by 78% over 2025 through model optimisations, efficiency and utilisation improvements."
- Appears: 08 L207-211
- Suggested source: Alphabet Q4 2025 earnings call
- [URL: pending]

**Quote B**: After the Gemini image-generation over-tune incident, publicly said "unacceptable"
- Appears: 18 L196-199 / 21 L207
- Suggested source: Google official blog 2024-02 statement
- [URL: pending]

### 1.13 Liang Wenfeng (DeepSeek founder)

**Quote**: "We did not intend to be a catfish — we became a catfish by accident… our principle is not to subsidize, and not to extract excessive margin. This price is a small profit on top of cost."
- Appears: 08 L213-217
- Suggested source: Waves (暗涌) interview
- [URL: pending]

### 1.14 Sebastian Siemiatkowski (Klarna CEO)

**Quote A**: 2024 announced AI replacing the equivalent of 700 customer service workloads
**Quote B**: 2025-05 publicly admitted "AI lacks empathy," reopened hiring and shifted to a hybrid model
- Appears: 04 L263 / 22 L221-223 / 25 L160-164
- Source A (2024-02 Klarna announcement): https://www.klarna.com/international/press/klarna-ai-assistant-handles-two-thirds-of-customer-service-chats-in-its-first-month/
- Source B (2025-05 Bloomberg reversal coverage): https://www.bloomberg.com/news/articles/2025-05-08/klarna-turns-from-ai-to-real-person-customer-service

### 1.15 Dario Amodei (Anthropic CEO)

**Quote**: Research team accounts for ~1/3 or more
- Appears: 24 L52-60 / 25 L34-36
- Suggested source: Anthropic CEO interviews (Lex Fridman et al.)
- [URL: pending]

### 1.16 Lenny Rachitsky (Lenny's Newsletter)

**Quote**: "Everyone should be using Claude Code more" / "forget that it's called Claude Code — treat it as Claude Local / Claude Agent" / collected 50 non-technical user cases of Claude Code
- Appears: 17 L228-232 / L355
- Suggested source: Lenny Newsletter 2026-02 piece
- [URL: pending]

### 1.17 Dennis Yang (Chime PM)

**Quote**: PRD in markdown → open `claude` in terminal → 20 minutes for a clickable prototype → share via Slack screen recording
- Appears: 17 L222-224
- Suggested source: Dennis Yang public talks / Lenny Newsletter citation
- [URL: pending]

### 1.18 Anna Arteeva (vibe-coding reviewer)

**Quote**: "Lovable wins for non-technical PMs, Bolt wins for speed, v0 wins for UI, Replit wins full-stack, Cursor / Claude Code win for engineering depth"
- Appears: 17 L202-206
- Suggested source: Anna Arteeva Medium / public reviews
- [URL: pending]

### 1.19 Miqdad Jaffer (OpenAI Product Lead)

**Quote**: productcompass.pm's public "AI PRD Template" — capability boundary / input-output schema / eval set / failure modes / cost ceiling
- Appears: 02 L36
- Suggested source: productcompass.pm
- [URL: pending]

### 1.20 David Haberlah (Medium data analysis)

**Quote**: Unpacked 638 PMs' actual outputs — AI-related content went from 4% in early 2023 to 67% in 2026 Q1; mocking & prototyping dropped from 60-70% to 30-40%
- Appears: 01 L46-52 / 02 L96
- Suggested source: David Haberlah Medium piece
- [URL: pending]

### 1.21 Shreya Shankar (Hamel's Maven co-instructor)

**Quote**: Co-launched Maven course with Hamel; have taught 2000+ PMs and engineers
- Appears: 01 L236-244
- Suggested source: Maven course "AI Evals For Engineers & PMs"
- [URL: pending]

### 1.22 OpenAI's own GPT-4o sycophancy postmortem

**Quote**: "Sycophancy was not included as a blocking item in the release evaluation"; several testers "felt something was off" but had no mechanism to halt the release; post-fix policy: "behavior issues must be able to block release"
- Appears: 01 L302 / 14 L242-248 / 18 L188-194 / 21 L195-201 / 23 L88
- Source A (initial announcement 2025-04-29): https://openai.com/index/sycophancy-in-gpt-4o/
- Source B (detailed postmortem 2025-05-01): https://openai.com/index/expanding-on-sycophancy/

---

## Category 2: Third-Party Reports / Survey Data (~15)

### 2.1 MIT NANDA *State of AI in Business 2025*
- 95% of enterprise GenAI projects had zero measurable return; partner-built model has 67% success rate vs. 1/3 for pure internal build
- Appears: 04 L17 / L42-44 / L219-223 / 06 L86-87 / L197
- Source: MIT Sloan / NANDA Initiative, 2025-08 [URL: pending]

### 2.2 a16z 2025 Enterprise LLM — 100 CIOs survey
- Enterprise LLM annual spend $4.5M → $7M; 37% run 5+ models in parallel; 74% of CEOs put AI as top priority; budget expected up ~75% next year
- Appears: 04 L229-232 / 14 L213 / 20 L89-91 / 22 L131-134 / 24 L63-73
- Source: a16z.com 2025 Enterprise AI Survey [URL: pending]

### 2.3 Gartner 2025 GenAI Hype Cycle
- GenAI in Trough of Disillusionment; <30% of CEOs satisfied with returns
- Appears: 04 L224-228
- Source: Gartner official report [URL: pending]

### 2.4 ICONIQ 2025 AI Product Survey
- AI product gross margin: 2024 = 41% / 2025 = 45% / 2026 = 52%
- Appears: 03 L65-66 / 09 L122 / L242-243 / 15 L207-209
- Source: iconiqcapital.com 2025 report [URL: pending]

### 2.5 Stanford RegLab + HAI Legal AI Hallucination Study (2024-2025)
- Lexis+ AI 17% / Westlaw AI-Assisted Research 33% / GPT-4 43% hallucination rates
- Appears: 04 L67-68
- Source: Stanford RegLab paper / hai.stanford.edu [URL: pending]

### 2.6 The Information / Reuters on Anthropic / OpenAI financials
- Anthropic inference cost briefly exceeded period revenue; OpenAI 2025 revenue ~$13B
- Appears: 09 L233-243 / 15 L196-205
- Source: theinformation.com / reuters.com 2025 reporting [URL: pending]

### 2.7 Springer Nature User Research review
- "Systematic gap between pre-experience expectations and post-experience evaluation"
- Appears: 01 L170 / 03 L34 / L119
- Source: Springer Nature journal [URL: pending]

### 2.8 TechXplore sycophantic study (2025-07)
- ChatBots remain confident even when wrong
- Appears: 03 L126
- Source: TechXplore 2025-07 [URL: pending]

### 2.9 EMNLP 2024 RLHF Alignment Tax paper
- OpenLLaMA-3B preference-alignment reward from 0.16 to 0.35 — SQuAD F1 drops 16, DROP F1 drops 17, WMT BLEU drops 5.7
- Appears: 02 L128 / 07 L168
- Source: EMNLP 2024 proceedings (aclanthology.org) [URL: pending]

### 2.10 MIT MedRxiv 2025 medical AI hallucination paper
- LLM hallucinations hardest to detect because they "use specialized terminology + look coherent"
- Appears: 04 L94
- Source: medrxiv.org 2025 paper [URL: pending]

### 2.11 MISQ Lebovitz / Levina / Lifshitz-Assaf *Is AI Ground Truth Really True?*
- Expert know-what labeling uncertainty drives "benchmark high score / production blowup"
- Appears: 04 L96
- Source: MIS Quarterly [URL: pending]

### 2.12 METR "horizon length" research series
- Task duration that frontier models can reliably complete doubles every 7 months
- Appears: 05 L58 / L205
- Source: metr.org [URL: pending]

### 2.13 Partnership on AI *Prioritizing Real-Time Failure Detection in AI Agents* (2025)
- Lists "real-time failure detection" as a core problem of long-Agent deployment
- Appears: 05 L167-171
- Source: partnershiponai.org [URL: pending]

### 2.14 Retool — vibe-coded app survey
- Connecting vibe-coded apps to real databases turns SQL injection into a "data breach waiting to happen"
- Appears: 17 L260
- Source: Retool State of AI report [URL: pending]

### 2.15 Jevons paradox data
- Token prices down 99.7%; enterprise AI total spend up to $37B
- Appears: 09 L245-247 / 15 L211
- Source: Bloomberg / a16z / ICONIQ composite [URL: pending]

---

## Category 3: Industry Incidents (~24)

### 3.1 Air Canada Moffatt case (2024-02 ruling)
- Bot fabricated "bereavement-fare 90-day retroactive refund" policy; BC Civil Resolution Tribunal awarded CAD 650.88 (~USD 480); ruled "chatbot is not an independent legal entity"
- Appears: 04 L132 / 11 L252-262 / 14 L218-223 / 19 L222-228 / L294 / 22 L226-230 / 24 L83-87
- Source: https://www.canlii.org/en/bc/bccrt/doc/2024/2024bccrt149/2024bccrt149.html (official CanLII judgment text, 2024 BCCRT 149)

### 3.2 Klarna AI replacing 700 CS (2024 → 2025 reversal)
- Appears: 04 L263 / 22 L221-223 / 25 L160-164
- Source A (2024-02 Klarna PR): https://www.klarna.com/international/press/klarna-ai-assistant-handles-two-thirds-of-customer-service-chats-in-its-first-month/
- Source B (OpenAI customer case): https://openai.com/index/klarna/
- Source C (2025-05 Bloomberg reversal): https://www.bloomberg.com/news/articles/2025-05-08/klarna-turns-from-ai-to-real-person-customer-service
- Source D (2025-05 Fortune analysis): https://fortune.com/2025/05/09/klarna-ai-humans-return-on-investment/

### 3.3 DPD chatbot — Ashley Beauchamp (2024-01)
- Post-update no regression eval — coaxed into writing a poem "DPD is the world's worst courier"; single tweet → millions of impressions on X
- Appears: 12 L219-223 / 19 L206-212 / 20 L196-200
- Source: BBC / The Guardian 2024-01 coverage + Ashley Beauchamp's X tweet [URL: pending]

### 3.4 NYC MyCity government chatbot (2024-03)
- Appears: 04 L173-184 / 11 L264-272 / 12 L224-226 / 19 L214-220
- Source: The Markup investigation (themarkup.org) [URL: pending]

### 3.5 Chevy dealer chatbot — prompt injection sold $1 Tahoe (2023-11)
- Appears: 11 L275-284
- Source: original X tweet + Business Insider / The Verge 2023-11 [URL: pending]

### 3.6 McDonald's × IBM drive-thru AI ordering (2021 → 2024-07)
- Appears: 04 L189-196 / 12 L63 / 22 L105-107 / L233-238
- Source: CNBC / Bloomberg / Restaurant Business Online 2024-06 [URL: pending]

### 3.7 Knight Capital $440M loss (2012)
- 8 servers but 1 missed the update; $440M lost in 45 minutes
- Appears: 18 L287
- Source: SEC investigation report / Wikipedia "Knight Capital Group" [URL: pending]

### 3.8 OpenAI GPT-4o sycophancy (2025-04-25 → 2025-04-29 full rollback)
- Appears: 01 L302-304 / 14 L228-248 / 18 L188-194 / 21 L194-201 / 23 L88 / 24 L100-105
- Source A (OpenAI initial announcement 2025-04-29): https://openai.com/index/sycophancy-in-gpt-4o/
- Source B (OpenAI detailed postmortem 2025-05-01): https://openai.com/index/expanding-on-sycophancy/
- Source C (TechCrunch): https://techcrunch.com/2025/04/29/openai-explains-why-chatgpt-became-too-sycophantic/

### 3.9 Cursor 2025-06 billing blowup
- Appears: 01 L268 / 02 L163 / 08 L246 / 09 L218-224 / 15 L156-165
- Source A (Cursor official apology blog 2025-07-04): https://cursor.com/blog/june-2025-pricing
- Source B (TechCrunch 2025-07-07): https://techcrunch.com/2025/07/07/cursor-apologizes-for-unclear-pricing-changes-that-upset-users/

### 3.10 DoorDash chatbot simulator
- Appears: 18 L113-118
- Source: DoorDash Engineering Blog [URL: pending]

### 3.11 Anthropic 2025 Postmortem (perf optimization hurting output quality)
- Appears: 20 L162-167
- Source: Anthropic Engineering Blog 2025 postmortem [URL: pending]

### 3.12 Cursor "engine vs car" + Claude 3.7 post-train
- Appears: 02 L132-134 / L182 / 07 L172-174 / L208
- Source: Cursor team public blog / engineering interviews [URL: pending]

### 3.13 Humane AI Pin failure (2025-02 sold to HP)
- Raised $230M; 2025-02 sold to HP for $116M
- Appears: 01 L174
- Source: Bloomberg / The Verge 2025-02 [URL: pending]

### 3.14 ChatGPT "gibberish incident" (2024-02-20)
- ~5h online rollback
- Appears: 18 L203-209
- Source: OpenAI status page report [URL: pending]

### 3.15 Gemini image generation over-tune (2024-02)
- Appears: 18 L196-199 / 21 L203-209
- Source: Google official statement + The Verge / Wired [URL: pending]

### 3.16 Google AI Overviews glue-on-pizza (2024-05)
- Appears: 20 L190-195
- Source: The Verge / BBC 2024-05 [URL: pending]

### 3.17 Manus AI (Butterfly Effect)
- Claimed GAIA SOTA; in real testing reliability / context window / paywall / CAPTCHA all jammed
- Appears: 05 L222-234
- Source: multiple tech-media test reports early 2025 [URL: pending]

### 3.18 Khan Academy Khanmigo (education AI)
- Appears: 06 bullet list (not deeply elaborated in body)
- Source: Khan Academy public statements [URL: pending]
- ⚠️ Note: little elaboration in body — author may expand or remove from index

### 3.19 Nabla medical AI scribe
- Appears: 06 bullet list (not deeply elaborated)
- Source: Nabla official site / public coverage [URL: pending]
- ⚠️ Note: same as above

### 3.20 5 real token-bill blowups
- #1: Claude Code recursive loop, 5h, 1.67B tokens
- #2: subagent entered 809-step infinite loop, 3.5h, $350
- #3: retry loop overnight burned $72,000 OpenAI credit
- #4: a software company — single billing period $150,000 shadow-AI crisis
- #5: Cursor June 2025 billing (see 3.9)
- Appears: 09 L200-224 / 15 L133-137
- Source: Hacker News / X / Reddit consolidated [URL: pending]

### 3.21 Cursor (ARR-per-employee)
- 2025-Q3 engineering team ~100, supporting ~$1B-scale ARR
- Appears: 01 L32 / 25 L57-60 / L260-262
- Source: Cursor official / Forbes / Bloomberg [URL: pending]

### 3.22 Lovable (ARR-per-employee)
- 2025-Q3 snapshot — 18 people, ~$17M ARR
- Appears: 01 L30 / 16 L109-110 / 25 L72-77 / L252-254
- Source: Lovable founder public statements [URL: pending]

### 3.23 Anthropic sales-to-headcount ratio
- ~2000 people; only dozens of quota-carrying salespeople
- Appears: 01 L34
- Source: Anthropic public statements [URL: pending]

### 3.24 Notion × Braintrust case
- Dual-track eval (regression + frontier); certain workflows sped up ~10x
- Appears: 12 L100-104 / 18 L103-110 / 25 L51-53 / L248-250
- Source: Braintrust customer-case blog [URL: pending]

### 3.25 thoughtbot engineer weekend MVP
- Appears: 16 L112-114
- Source: thoughtbot blog [URL: pending]

### 3.26 Anna Arteeva — AI Agents Benchmark vibeCrm case
- Appears: 16 L115-117 / L119-127
- Source: Anna Arteeva Medium [URL: pending]

### 3.27 Anthropic prompt caching — 3 cases
- DEV.to author: RCA task — 90% cost cut
- Du'An Lightfoot: monthly bill $720 → $72
- ProjectDiscovery: cache hit rate 7% → 74%
- Appears: 08 L99-114 / 09 L186
- Source: DEV.to / Du'An Lightfoot blog / ProjectDiscovery [URL: pending]

---

## Category 4: Open-Source Frameworks / Public Standards (~21)

### 4.1 BMAD-METHOD (Breakthrough Method of Agile AI-Driven Development)
- Appears: 01 L100-104 / 11 L174-182 / 13 L231-241
- Source: github.com/bmad-code-org/BMAD-METHOD [URL: pending]

### 4.2 GitHub Spec Kit (Spec-Driven Development)
- Maintainer: GitHub; open-sourced 2025-09; flow: `/specify` → `/plan` → `/tasks` → `/analyze`
- Appears: 01 L106-116 / 11 L164-172 / 13 L243-255
- Source: github.com/github/spec-kit [URL: pending]

### 4.3 OpenAI Model Spec
- Maintainer: OpenAI; 3-layer structure Objectives / Rules / Defaults; version 2025-12-18 (latest, includes U18 Principles)
- Appears: 11 L139-147 / 14 L172-180 / 24 L167-175
- Source A (latest): https://model-spec.openai.com/
- Source B (2025-12-18 permalink): https://model-spec.openai.com/2025-12-18.html

### 4.4 Anthropic ASL (AI Safety Levels) / Responsible Scaling Policy
- 4-tier capability classification ASL-1 → ASL-4
- Appears: 14 L165-170 / 24 L176-184
- Source: anthropic.com/responsible-scaling-policy [URL: pending]

### 4.5 Anthropic Constitutional AI (2022 training-phase method)
- Appears: 21 L117-122
- Source: anthropic.com/research/constitutional-ai-harmlessness-from-ai-feedback [URL: pending]

### 4.6 Anthropic Constitutional Classifiers (2025 inference-phase method)
- Appears: 21 L123-128
- Source: Anthropic 2025 Research announcement [URL: pending]

### 4.7 Microsoft Responsible AI Standard v2
- Core: frequency × severity 2-D matrix
- Appears: 11 L48-49 / 14 L115-122 / 24 L78-93 / L185-191
- Source A (Microsoft CDN official PDF): https://cdn-dynmedia-1.microsoft.com/is/content/microsoftcorp/microsoft/final/en-us/microsoft-brand/documents/Microsoft-Responsible-AI-Standard-General-Requirements.pdf
- Source B (Microsoft Blog archive PDF): https://blogs.microsoft.com/wp-content/uploads/prod/sites/5/2022/06/Microsoft-Responsible-AI-Standard-v2-General-Requirements-3.pdf

### 4.8 Microsoft Azure AI Content Safety
- Core: 4 harm classes × 4 severity levels
- Appears: 14 L160-164
- Source: learn.microsoft.com/en-us/azure/ai-services/content-safety/ [URL: pending]

### 4.9 Anthropic Acceptable Use Policy
- Appears: bullet list (not deeply elaborated in body)
- Source: anthropic.com/legal/aup [URL: pending]
- ⚠️ Note: same — author may elaborate or remove

### 4.10 SWE-bench Verified
- Maintainer: OpenAI (based on the SWE-bench team); 500 hand-curated Python samples
- Appears: 12 L53-58 / L321 / 08 (table)
- Source: openai.com/index/introducing-swe-bench-verified/ [URL: pending]

### 4.11 OpenAI Evals Repo
- YAML + JSONL data format; oaieval / oaievalset CLI
- Appears: 12 L254-263
- Source: github.com/openai/evals [URL: pending]

### 4.12 Inspect AI (UK AISI)
- Maintainer: UK AI Safety Institute; 4-layer abstraction Dataset → Task → Solver → Scorer
- Appears: 12 L264-271
- Source: inspect.aisi.org.uk [URL: pending]

### 4.13 Anthropic — statistical methodology paper
- Eval results must come with confidence intervals
- Appears: 02 L110 / 08 L143 / 12 L273-279
- Source: anthropic.com/research/statistical-approach-to-model-evals [URL: pending]

### 4.14 Scrum.org *Definition of Done for AI Agents*
- Appears: 01 L70-74 / 02 L46-48 / 11 L206-209
- Source: scrum.org blog [URL: pending]

### 4.15 Google Model Card (2018) + Cambridge AI Product Card (2024)
- Appears: 02 L35
- Source: cambridge.org/core/journals/data-and-policy [URL: pending]

### 4.16 Anthropic Engineering Manager / Evals hiring
- Evals EM base reaches $300K+; Netflix hiring "Software Engineer L4/L5, LLM Evaluation"
- Appears: 02 L69-71 / 13 L84
- Source: anthropic.com/careers / netflix careers public JDs [URL: pending]

### 4.17 Anthropic 58-tool token data + Tool Search
- 58 tools cost ~55K token; on Claude Opus 4.5 Tool Search bumps accuracy 79.5% → 88.1%
- Appears: 05 L40-52 / L158-162
- Source: Anthropic Engineering Blog (2025-2026) [URL: pending]

### 4.18 OSWorld benchmark
- 2024-Q4 snapshot: Operator (CUA) 38.1% / Anthropic Computer Use 22.0% / human baseline 72.4%
- Appears: 02 L154 / 05 L66-71 / L263
- Source: os-world.github.io / paper [URL: pending]

### 4.19 PromptArmor / Lakera red-team tools
- Appears: 19 L75
- Source: promptarmor.com / lakera.ai [URL: pending]

### 4.20 Vellum / Traceloop best practices
- N-consecutive-error circuit breaker + spike detection + per-user hard cap
- Appears: 15 L108-117
- Source: vellum.ai / traceloop.com blogs [URL: pending]

### 4.21 Illinois state law + Texas TRAIGA
- Illinois (2025): "Wellness and Oversight for Psychological Resources Act" — prohibits AI from creating mental-health treatment plans
- Texas TRAIGA (partial effective 2026-01): physicians must disclose AI use in diagnosis in writing
- Appears: 22 L62-65 / L156-158 / L240-243
- Source: Illinois official legislative PDF + Texas TRAIGA official documents [URL: pending]

---

## Category 5: Model Vendor Public Data / Pricing / Benchmarks

### 5.1 2026-Q2 Mainstream Models Comparison (Essay 08 L31-49)

| Model | Input | Output | Cache read | SWE-bench Verified | First token | Compliance |
|---|---|---|---|---|---|---|
| Claude Opus 4.7 | $5/M | $25/M | $0.50/M | 87.6% | ~2s | SOC2 II / HIPAA BAA / ZDR |
| Claude Sonnet 4.6 | $3/M | $15/M | $0.30/M | ~82% | 2s | same |
| Claude Haiku 4.5 | $1/M | $5/M | $0.10/M | ~73% | <1s | same |
| GPT-5.5 | $5/M | $30/M | 10% auto | 88.7% | 0.55s | SOC2 II / HIPAA |
| GPT-5.1 | $1.25/M | $10/M | auto | ~80% | <1s | same |
| GPT-5 | $0.625/M | $5/M | auto | ~75% | <1s | same |
| Gemini 3 Flash | $0.50/M | $3/M | - | 80.6% | sub-second | Vertex VPC SC / HIPAA BAA |
| DeepSeek V3.2 | $0.28/M | $0.42/M | built-in cache hit $0.028 | ~70% | medium | China-domestic, no BAA |
| Kimi K2.6 | $0.60/M | $2.50/M | - | ~75% | medium | China-domestic, no BAA |

- Suggested sources by vendor:
  - Anthropic: anthropic.com/pricing + model cards
  - OpenAI: openai.com/pricing + model cards
  - Google: ai.google.dev/pricing + Gemini model cards
  - DeepSeek: api-docs.deepseek.com
  - Kimi (Moonshot): platform.moonshot.cn
  - 3rd-party leaderboards: artificialanalysis.ai / SEAL
- [URL: pending × each vendor]

### 5.2 Anthropic Opus 4.7 — new tokenizer's 35% bump
- Source: Finout post
- Appears: 08 L176-186
- Source: finout.io [URL: pending]

### 5.3 Anthropic prompt caching decision line
- system prompt > 1024 tokens + reuse rate > 2
- Appears: 08 L157-172
- Source: Anthropic official docs (prompt caching) [URL: pending]

### 5.4 OpenAI / Azure monthly budget hard cap
- Appears: 15 L98-106
- Source: platform.openai.com / learn.microsoft.com Azure docs [URL: pending]

### 5.5 AI Observability SaaS tools
- Datadog LLM Observability (factuality / toxicity / relevance)
- Braintrust (eval-driven development + CI/CD gates)
- Arize (enterprise-grade AI observability)
- Helicone (one-line proxy)
- Traceloop (OpenTelemetry user_id injected into trace)
- LangSmith (LangChain official)
- Appears: 20 L42 / L48 / L52 / L79 / L91 / L205-228 / 23 L143-147
- Source: datadoghq.com / braintrust.dev / arize.com / helicone.ai / traceloop.com / smith.langchain.com [URL: pending × each]

---

## Pre-Publish Checklist

- [ ] Every citation has a concrete URL filled in
- [ ] Dead URLs → re-phrase to "as reported by X" in body
- [ ] Highly sensitive citations (KOL famous quotes) → double-verify original was a public talk / article
- [ ] Model pricing / benchmark data (Category 5) → re-verify against vendor model card within 7 days of publish
- [ ] Air Canada / NYC MyCity / Chevy Tahoe and similar case-law citations → verify original judgment / investigative reporting links
- [ ] Citations like Khan Academy Khanmigo / Nabla / Anthropic AUP that are listed but not elaborated → decide whether to expand in body or remove from index
- [ ] OpenAI / Anthropic financial data → official disclosure or top-tier media (The Information / Reuters) only
- [ ] Anthropic Postmortem / OpenAI sycophancy postmortem → link to official incident report
- [ ] Companion-asset list: this References Index will be one of the paid-reader unlocked assets

---

## High-Exposure Citations (URL Priority)

By appearance frequency — the citations most likely to be "URL-checked by peers":

| Citation | # of essays | Risk |
|---|---|---|
| Air Canada Moffatt case | 7 | ⭐⭐⭐ Highest |
| OpenAI GPT-4o sycophancy postmortem | 5 | ⭐⭐⭐ Highest |
| Cursor 2025-06 billing blowup | 5 | ⭐⭐⭐ Highest |
| Hamel "EDD" series | 4 | ⭐⭐ High |
| OpenAI Model Spec | 3 | ⭐⭐ High |
| Microsoft RAI Standard v2 | 3 | ⭐⭐ High |
| Anthropic Cat Wu Product Note | 3 | ⭐⭐ High |
| Cat Wu "prototypes over PRDs" | 3 | ⭐⭐ High |
| Klarna 700 CS | 3 | ⭐⭐ High |

**Author's top-priority before publish**: fill the URLs for the 9 above; everything else can batch later.

---

> Companion asset · Season 1 *AI-Era PM Workflow Reconstruction*
> Author: Cai Yiwen (WeChat Official Account 「蔡逸雯」)

---

> **Reading the Chinese original?** See [27-references.md](./27-references.md)
> **Part of**: Season 1 · AI PM Workflow Reconstruction · 26 essays
> **Author**: Cai Yiwen (蔡逸雯) · 8 years in QE → AI PM
