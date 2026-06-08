# 全球参照库 v1.0 · 9 套工具调研依据 backbone

> 服务于公众号《AI 时代 PM 工作流重构》第一季 9 套配套工具的「调研依据」标准
> 原则：**只挖全球 tier-1，国内市场存在信息差不参考**
> 创建：2026-05-21 · 最后更新：2026-05-21
> 引用核查状态：约 70% URL 已核查（基于 GitHub repo 27-references v1.1 的工作），剩余 30% 标 [URL: 待核]

---

## 使用约定

**每个 Source 的结构**：
- **是谁 / 全球 tier-1 的理由**（为什么不选第二档）
- **核心代表作 + URL**（如已核查）
- **服务哪个 Tool**（Task ID）
- **关键观点 / 数据**（直接引用句）

**全球 tier-1 标准**（满足任一）：
1. **公开框架被 2+ 全球前沿 AI 公司采纳**（Anthropic / OpenAI / Google / Microsoft / Meta）
2. **学术或行业引用量 > 1000**（Google Scholar / 行业引用追踪）
3. **直接参与全球前沿模型 / 产品设计**（如 Anthropic CPO / OpenAI Product Lead）
4. **被 Stanford HAI / MIT / a16z / Gartner 等机构纳入官方报告**

**拒绝标准**：
- ❌ 国内自媒体 / 公众号（信息差大、引用链断）
- ❌ Twitter / X 上没有验证身份的 "AI 专家"
- ❌ LinkedIn influencer 自我营销

---

## 池子 1：KOL 个人 + 产品框架

> 服务工具：#46 (PM × Claude Code SOP) / #49 (PRD 模板) / #50 (案例 PRD) / #55 (协作话术) / #56 (成长包)

### 1.1 Hamel Husain（独立 AI evals 顾问）

**全球 tier-1 理由**：
- (a) 唯一作者全行业最被引用的「Field Guide to Rapidly Improving AI Products」SOP
- (b) Maven 课程「AI Evals For Engineers & PMs」联合讲师，教过 2000+ PM+工程师
- (c) Anthropic / OpenAI / Notion 工程团队都公开引用他的方法
- (d) Latent Space 等顶级技术 podcast 常驻嘉宾

**核心代表作**：
- 🔗 https://hamel.dev/blog/posts/field-guide/ — Field Guide（已核查）
- 🔗 https://hamel.dev — 个人博客
- 🔗 Maven course: AI Evals For Engineers & PMs（与 Shreya Shankar 合开）

**关键观点**：
- "Writing good evals is becoming the defining skill for AI PMs."
- "Until you stop finding new failure modes" — 看 trace 看到不再有新失败模式为止才停
- 60-80% 开发时间花在 error analysis + evaluation
- 二元评分（0/1）比 5 分制更稳定

**服务 Tool**：#48 (6 问 checklist 设计依据对照) / #51 (Eval 工具包) / #54 (Bad Case 管理)

---

### 1.2 Shreya Shankar（Hamel 联合讲师 / UC Berkeley AI 研究者）

**全球 tier-1 理由**：
- (a) UC Berkeley AI 研究者，学术 + 工业双背景
- (b) Maven 课程联合讲师
- (c) Eval / data quality 学术论文多次被引用

**核心代表作**：
- Maven AI Evals 课程材料
- 学术论文（Stanford / Berkeley AI lab）

**服务 Tool**：#51 (Eval 工具包)

---

### 1.3 Cat Wu（Anthropic Claude Code Head of Product）

**全球 tier-1 理由**：
- (a) Claude Code 产品负责人，全球最重要的 AI 编程 Agent 产品之一
- (b) Lenny's Podcast 公开访谈 + Anthropic 官方 product practice 发布
- (c) "Prototypes over PRDs" 是 2026 年 AI PM 圈最广为流传的口号

**核心代表作**：
- 🔗 https://www.lennysnewsletter.com/p/how-anthropics-product-team-moves —（已核查）

**关键观点**：
- "Prototypes over PRDs"
- "Spec-first" — 起手定义 use case + success criteria
- "Daily user sentiment loop" — 每天看用户反馈
- Anthropic 产品团队"为什么比所有人都快"：PM/Designer/Eng 都用 Claude Code 直接产出 working prototype

**服务 Tool**：#49 (PRD 模板) / #46 (Claude Code SOP) / #55 (协作话术)

---

### 1.4 Mike Krieger（Anthropic CPO，前 Instagram 联合创始人）

**全球 tier-1 理由**：
- (a) Instagram 联合创始人（独角兽产品经验）
- (b) Anthropic CPO，统筹全球前沿 AI 产品
- (c) 提出「Product Note + 2 context files + Editor-in-Chief」三件套，颠覆传统 PRD

**核心代表作**：
- Lenny's Podcast Mike Krieger 专访集

**关键观点**：
- PM 不再写 10 页 PRD，改写 3-4 段的 Product Note
- 配 `product_area_context.md` + `code_context.md` 两个上下文文件
- orchestrator 合成 Functional Spec
- PM 转身做 "Editor-in-Chief" 审 PR

**服务 Tool**：#49 (PRD 模板核心参照) / #55 (协作话术)

---

### 1.5 Boris Cherny（Anthropic Claude Code lead）

**全球 tier-1 理由**：
- (a) Claude Code 工程负责人
- (b) 自 2025-11 起 100% 代码由 Claude Code 写，自己不手敲——dogfood 极致案例

**核心代表作**：Lenny's Podcast Boris Cherny 专访

**服务 Tool**：#46 (Claude Code SOP)

---

### 1.6 Aparna Chennapragada（Microsoft CPO）

**全球 tier-1 理由**：
- (a) Microsoft CPO，覆盖 Copilot 系列
- (b) 提出「Prompt sets are the new PRDs」—— 与 Cat Wu 框架互补
- (c) 前 Google / Robinhood 产品高管

**核心代表作**：Lenny's Podcast Aparna Chennapragada 专访

**关键观点**：
- "Prompt sets are the new PRDs."
- "Prompt set 是活的产物，半是 spec 半是训练数据"
- 传统 PRD"为程序员而写、提前锁死需求再交付"，AI 产品本质非确定性

**服务 Tool**：#49 (PRD 模板) / #55 (协作话术)

---

### 1.7 Sachin Rekhi（前 LinkedIn / Reforge 讲师）

**全球 tier-1 理由**：
- (a) LinkedIn 资深 PM
- (b) Reforge 课程讲师（全球 AI PM 学习平台）
- (c) "AI Prototyping Mastery Ladder"（Apprentice / Journeyman / Master）被广泛采纳

**核心代表作**：
- 🔗 sachinrekhi.com
- Reforge 课程页

**关键观点**：自建 10+ skills——客户访谈合成 / NPS 自治 / 无 SQL EDA / 战略 critique / release notes 自动化

**服务 Tool**：#46 (Claude Code SOP 阶梯框架) / #56 (PM 成长包)

---

### 1.8 Marty Cagan（SVPG）

**全球 tier-1 理由**：
- (a) Silicon Valley Product Group 创始人，《Inspired》作者
- (b) 全球产品发现方法论开创者
- (c) AI 时代依然保持思想活跃，2025 多次发文

**核心代表作**：
- 🔗 svpg.com

**关键观点**：
- "Product discovery 是判断（judgement），AI 可以自动化交付，但发现未满足需求、验证价值这件事不能。"

**服务 Tool**：#56 (PM 成长包) / #55 (协作话术)

---

### 1.9 Teresa Torres（Product Talk）

**全球 tier-1 理由**：
- (a) Continuous Discovery Habits 全球流行框架作者
- (b) Product Talk 影响力覆盖欧美 PM 社区
- (c) 提出 AI 时代访谈方法论必须变化

**核心代表作**：
- 🔗 producttalk.org

**关键观点**：客户访谈本身要变。AI 产品里 outcome 不是确定性的，访谈不能再问"你想要什么"，而要 log traces / 让人审 / 标错误类 / 写 evals / A/B 测修复

**服务 Tool**：#53 (能力边界工具包) / #55 (协作话术)

---

### 1.10 Kevin Weil（OpenAI CPO）

**全球 tier-1 理由**：OpenAI CPO，前 Instagram / Twitter / Planet 产品高管

**关键观点**：季度 roadmap 和年度策略反映不了真实出货节奏；roadmap 重新定义为 "rolling bets"

**服务 Tool**：#56 (PM 成长包) / #54 (上线运营 roadmap)

---

### 1.11 Lenny Rachitsky（Lenny's Newsletter / Podcast）

**全球 tier-1 理由**：
- (a) 全球最大 PM 自媒体（Newsletter + Podcast）
- (b) 访谈过 Anthropic / OpenAI / Microsoft / Cursor 等几乎所有顶级 AI 产品负责人
- (c) AI PM 圈"集大成者"，单条 podcast 引用率极高

**核心代表作**：
- 🔗 lennysnewsletter.com
- Lenny's Podcast

**关键观点**：
- "Everyone should be using Claude Code more"
- "忘掉它叫 Claude Code，把它当作 Claude Local / Claude Agent"
- 收集 50 个非技术用户的 Claude Code 用例

**服务 Tool**：#46 (Claude Code SOP) / #56 (PM 成长包) / 所有访谈类引用

---

### 1.12 Dennis Yang（Chime PM）

**全球 tier-1 理由**：Lenny Newsletter 推荐的"PM 用 Claude Code 实战标杆"，方法论极具可操作性

**关键观点**：markdown 写 PRD → 终端 `claude` → 20 分钟跑出可点击 prototype → Slack 录屏分享

**服务 Tool**：#46 (Claude Code SOP 案例)

---

### 1.13 Anna Arteeva（独立 AI 工具评测者）

**全球 tier-1 理由**：
- (a) AI Agents Benchmark 公开评测——全球最被引用的 Vibe Coding 工具横评源之一
- (b) Medium 长文 + GitHub 公开数据

**核心代表作**：Medium / GitHub AI Agents Benchmark

**关键观点**："Lovable 赢非技术 PM，Bolt 赢速度，v0 赢 UI，Replit 赢全栈，Cursor / Claude Code 赢工程深度"

**服务 Tool**：#44 (Vibe Coding 横评) ⭐ 核心参照

---

### 1.14 Miqdad Jaffer（OpenAI Product Lead）

**全球 tier-1 理由**：OpenAI 产品负责人 + Product Compass 公开 "AI PRD Template"

**核心代表作**：🔗 productcompass.pm — AI PRD Template

**关键观点**：能力边界 / 输入输出 schema / 评估集 / 失败模式 / 成本上限 五维 PRD 结构

**服务 Tool**：#49 (PRD 模板核心参照)

---

## 池子 2：机构标准 + 报告

> 服务工具：#47 (MIT NANDA 分类) / #49 (PRD 模板合规章节) / #51 (Eval) / #54 (上线运营)

### 2.1 OpenAI Model Spec

**全球 tier-1 理由**：OpenAI 官方发布的「模型行为规范」，定义了什么能做 / 什么不能做 / 什么用户可配置

**核心代表作**：
- 🔗 https://model-spec.openai.com/ — 最新版（已核查）
- 🔗 https://model-spec.openai.com/2025-12-18.html — 2025-12-18 永久链接（已核查）

**结构**：3 层 Objectives / Rules / Defaults

**服务 Tool**：#48 (6 问设计依据对照) / #49 (PRD 第 7 节能力边界参照) / #55 (协作话术)

---

### 2.2 Anthropic Responsible Scaling Policy + ASL

**全球 tier-1 理由**：Anthropic 官方，能力四级 ASL-1 → ASL-4

**核心代表作**：
- 🔗 anthropic.com/responsible-scaling-policy [URL: 待核]

**服务 Tool**：#49 (PRD 模板能力分级) / #54 (上线运营降级)

---

### 2.3 Anthropic Constitutional AI（训练阶段）+ Constitutional Classifiers（推理阶段）

**全球 tier-1 理由**：两套相互配合的 AI 安全方法，是 Claude 系列模型的对齐基础

**核心代表作**：
- 🔗 anthropic.com/research/constitutional-ai-harmlessness-from-ai-feedback [URL: 待核]
- Anthropic 2025 Research 公告（Constitutional Classifiers）

**服务 Tool**：#51 (Eval) / #54 (上线运营 / Bad Case 修复)

---

### 2.4 Microsoft Responsible AI Standard v2

**全球 tier-1 理由**：Microsoft 官方发布的"Responsible AI 标准"，核心是 frequency × severity 2D 矩阵

**核心代表作**：
- 🔗 https://cdn-dynmedia-1.microsoft.com/is/content/microsoftcorp/microsoft/final/en-us/microsoft-brand/documents/Microsoft-Responsible-AI-Standard-General-Requirements.pdf（已核查）
- 🔗 https://blogs.microsoft.com/wp-content/uploads/prod/sites/5/2022/06/Microsoft-Responsible-AI-Standard-v2-General-Requirements-3.pdf（已核查存档）

**服务 Tool**：#48 (6 问对照矩阵替代方案) / #49 (PRD 模板) / #54 (上线运营降级) ⭐ 核心参照

---

### 2.5 Microsoft Azure AI Content Safety

**全球 tier-1 理由**：Azure 官方内容安全 API，4 类伤害 × 4 级严重度

**核心代表作**：🔗 learn.microsoft.com/en-us/azure/ai-services/content-safety/

**服务 Tool**：#54 (上线运营 / 内容过滤)

---

### 2.6 Scrum.org《Definition of Done for AI Agents》

**全球 tier-1 理由**：Scrum 官方组织发布的 AI Agent 验收标准

**服务 Tool**：#49 (PRD 验收 checklist) / #51 (Eval)

---

### 2.7 Google Model Card（2018）+ Cambridge AI Product Card（2024）

**全球 tier-1 理由**：模型文档化的开山之作 + 学术延伸

**核心代表作**：🔗 cambridge.org/core/journals/data-and-policy

**服务 Tool**：#49 (PRD 模板能力边界写法)

---

### 2.8 MIT NANDA《State of AI in Business 2025》

**全球 tier-1 理由**：MIT Sloan + NANDA Initiative 联合发布，业内最被引用的 GenAI 企业失败数据源

**核心代表作**：
- 🔗 mitsloan.mit.edu / nanda.media.mit.edu（2025-08）[URL: 待核]

**关键数据**：
- **95% 企业 GenAI 项目零可衡量回报**
- 外采+共建模式成功率 67%，纯内部自建仅 1/3

**服务 Tool**：#47 (MIT NANDA 分类) ⭐ 核心参照 / #48 (6 问引言数据)

---

### 2.9 a16z 2025 企业 LLM 100 CIO 调研

**全球 tier-1 理由**：a16z 直接调研 100 家企业 CIO，AI 圈最被引用的 enterprise 数据源

**关键数据**：
- 企业 LLM 年均花费 $4.5M → $7M（+56%）
- 37% 企业同时跑 5+ 模型
- 74% CEO 把 AI 列为最高优先级
- 预算预期一年再涨 ~75%

**服务 Tool**：#52 (成本管控) / #54 (上线运营) / #55 (老板对齐)

---

### 2.10 Gartner 2025 GenAI Hype Cycle

**全球 tier-1 理由**：Gartner 是全球企业 IT 决策最被参考的研究机构

**关键数据**：
- GenAI 进入 Trough of Disillusionment
- 企业 2024 GenAI 投入 $190 万
- < 30% CEO 对回报满意

**服务 Tool**：#47 (MIT NANDA 分类交叉验证) / #55 (老板对齐)

---

### 2.11 ICONIQ 2025 AI 产品调研

**全球 tier-1 理由**：ICONIQ Capital 调研的 AI 产品毛利数据

**关键数据**：AI 产品毛利 2024=41% / 2025=45% / 2026=52%

**服务 Tool**：#52 (成本管控)

---

### 2.12 Stanford RegLab + HAI 法律 AI 幻觉研究（2024-2025）

**全球 tier-1 理由**：Stanford HAI 是全球 AI 治理研究的领头羊

**关键数据**：
- Lexis+ AI 17% / Westlaw AI-Assisted Research 33% / GPT-4 43% 幻觉率

**服务 Tool**：#48 (6 问数据源) / #47 (MIT NANDA 分类合规类别)

---

### 2.13 Stanford HAI AI Index Report（年度）

**全球 tier-1 理由**：Stanford HAI 年度 AI 产业报告，全球最权威之一

**服务 Tool**：#47 (MIT NANDA 分类交叉验证) / #56 (PM 成长包)

---

### 2.14 METR Horizon Length 研究

**全球 tier-1 理由**：METR 是 AI 能力评估顶级研究机构

**关键数据**：前沿模型能稳定完成的任务时长每 7 个月翻倍

**服务 Tool**：#53 (能力边界工具包) ⭐ 核心参照

---

### 2.15 Partnership on AI《Prioritizing Real-Time Failure Detection in AI Agents》（2025）

**全球 tier-1 理由**：Partnership on AI 是全球 AI 治理联盟（Anthropic / OpenAI / Microsoft / Google 成员）

**关键观点**：把"实时失败检测"列为长 Agent 部署的核心命题

**服务 Tool**：#53 (能力边界) / #54 (上线运营监控)

---

### 2.16 MIT MedRxiv 2025 医疗 AI 幻觉论文

**全球 tier-1 理由**：MIT 医学预印本平台

**关键观点**：LLM 幻觉因为"用专业术语 + 看似 coherent"反而最难识别

**服务 Tool**：#48 (6 问数据源 Q6) / #47 (MIT NANDA 分类医疗类别)

---

### 2.17 MISQ Lebovitz / Levina / Lifshitz-Assaf *Is AI Ground Truth Really True?*

**全球 tier-1 理由**：MIS Quarterly 是信息系统领域顶级期刊

**关键观点**：专家 know-what 标注的不确定性导致"benchmark 高分 / 实战崩盘"

**服务 Tool**：#48 (6 问 Q6 数据可得性) / #51 (Eval 工具包)

---

### 2.18 EMNLP 2024 RLHF 对齐税论文

**全球 tier-1 理由**：EMNLP 是 NLP 顶级会议

**关键数据**：OpenLLaMA-3B 偏好对齐奖励从 0.16 到 0.35 时，SQuAD F1 掉 16 分、DROP F1 掉 17 分、WMT BLEU 掉 5.7

**服务 Tool**：#51 (Eval) / #54 (上线运营 - Bad Case 管理)

---

## 池子 3：Eval / 工程框架 + SaaS 工具

> 服务工具：#51 (AI PM Eval 全套) / #52 (成本管控) / #54 (上线运营监控)

### 3.1 OpenAI Evals Repo

- 🔗 github.com/openai/evals [URL: 待核]
- YAML + JSONL 数据结构；oaieval / oaievalset CLI
- **服务 Tool**：#51

### 3.2 Inspect AI（UK AISI）

- 🔗 inspect.aisi.org.uk [URL: 待核]
- 四层抽象：Dataset → Task → Solver → Scorer
- 维护方：UK AI Safety Institute
- **服务 Tool**：#51

### 3.3 Anthropic 统计方法论文

- 🔗 anthropic.com/research/statistical-approach-to-model-evals [URL: 待核]
- 核心：eval 结果要带置信区间
- **服务 Tool**：#51

### 3.4 SWE-bench Verified

- 🔗 openai.com/index/introducing-swe-bench-verified/ [URL: 待核]
- 500 条 Python hand-curated 高质量样本
- **服务 Tool**：#51 / #56 (PM 成长包 benchmark 部分)

### 3.5 Braintrust（eval-driven development + CI/CD gates）

- 🔗 braintrust.dev
- 与 Notion 合作（双轨 eval，特定 workflow 提速近 10 倍）
- **服务 Tool**：#51 ⭐ 核心参照

### 3.6 Helicone（一行 proxy）

- 🔗 helicone.ai
- 一行 proxy 接入，native 暴露 rate-limited / rerouted / fallback 三种 degradation 请求标志
- **服务 Tool**：#52 / #54

### 3.7 LangSmith（LangChain 官方）

- 🔗 smith.langchain.com
- 适合 RAG / Agent debugging
- **服务 Tool**：#51 / #54

### 3.8 Arize（企业级 AI observability）

- 🔗 arize.com
- 最细颗粒度 bad case 分类
- **服务 Tool**：#54

### 3.9 Datadog LLM Observability

- 🔗 datadoghq.com（LLM Observability 产品页）
- 三维分布：factuality / toxicity / relevance
- **服务 Tool**：#54

### 3.10 Traceloop（OpenTelemetry user_id trace）

- 🔗 traceloop.com
- OpenTelemetry 注入 user_id 到 trace
- **服务 Tool**：#52 / #54

### 3.11 Vellum（per-user hard cap best practice）

- 🔗 vellum.ai
- 连续 N 次错误熔断 + spike detection + per-user hard cap
- **服务 Tool**：#52 / #54

### 3.12 promptfoo / DeepEval（开源 eval 框架）

- 🔗 promptfoo.dev
- 🔗 deepeval.com / github.com/confident-ai/deepeval
- **服务 Tool**：#51

### 3.13 PromptArmor / Lakera（红队工具）

- 🔗 promptarmor.com / lakera.ai
- 用于上线前 adversarial eval
- **服务 Tool**：#54

### 3.14 Finout（成本分析）

- 🔗 finout.io
- Anthropic Opus 4.7 新 tokenizer 涨 35% 数据来源
- **服务 Tool**：#52

### 3.15 BMAD-METHOD（Breakthrough Method of Agile AI-Driven Development）

- 🔗 github.com/bmad-code-org/BMAD-METHOD [URL: 待核]
- **服务 Tool**：#49 (PRD 模板)

### 3.16 GitHub Spec Kit（Spec-Driven Development）

- 🔗 github.com/github/spec-kit [URL: 待核]
- 流程：`/specify` → `/plan` → `/tasks` → `/analyze`
- 维护方：GitHub
- **服务 Tool**：#49 (PRD 模板) / #51

---

## 池子 4：真实业内案例库

> 服务工具：#54 (上线运营) / #55 (协作话术) / #56 (成长包) / 所有需要案例支撑的工具

### 4.1 Air Canada Moffatt 案（2024-02 判决）⭐ 最高引用

- 🔗 https://www.canlii.org/en/bc/bccrt/doc/2024/2024bccrt149/2024bccrt149.html（已核查 CanLII 官方判决全文）
- 关键判例：bot 编造"丧亲票 90 天内追溯申请退款"政策，BC Civil Resolution Tribunal 判赔 CAD 650.88，裁定"chatbot 不是独立法律实体"
- **服务 Tool**：#48 (6 问 Q4) / #55 (老板对齐话术) / #54 (上线运营降级)

### 4.2 Klarna AI 替代 700 客服（2024 → 2025 反转）⭐

- 来源 A（2024-02 Klarna 公告）：🔗 https://www.klarna.com/international/press/klarna-ai-assistant-handles-two-thirds-of-customer-service-chats-in-its-first-month/（已核查）
- 来源 B（OpenAI 客户案例页）：🔗 https://openai.com/index/klarna/（已核查）
- 来源 C（2025-05 反转 Bloomberg）：🔗 https://www.bloomberg.com/news/articles/2025-05-08/klarna-turns-from-ai-to-real-person-customer-service（已核查）
- 来源 D（2025-05 Fortune 解读）：🔗 https://fortune.com/2025/05/09/klarna-ai-humans-return-on-investment/（已核查）
- **服务 Tool**：#48 (6 问 Q3) / #55 (老板对齐降级)

### 4.3 DPD 聊天机器人 Ashley Beauchamp（2024-01）

- 来源：BBC / The Guardian 2024-01 + Ashley Beauchamp X 推文
- 关键：post-update 没回归 eval，调教出"DPD 是世界最差快递"的诗，单条推文 X 内数百万曝光
- **服务 Tool**：#54 (上线运营 / 上线前 adversarial)

### 4.4 NYC MyCity 政府 chatbot（2024-03）

- 来源：The Markup 调查（themarkup.org）
- 关键：建议商家"可拿员工小费"违反联邦劳动法等
- **服务 Tool**：#48 (6 问 Q4 合规) / #54

### 4.5 Chevy 经销商 chatbot $1 Tahoe（2023-11）

- 来源：原始 X 推文 + Business Insider / The Verge
- 关键：被 prompt injection 卖 $1 Tahoe
- **服务 Tool**：#49 (PRD 模板 adversarial 章节) / #54

### 4.6 McDonald's × IBM 得来速 AI 点单（2021-2024.07）⭐

- 来源：CNBC / Bloomberg / Restaurant Business Online 2024-06
- 关键：100+ 门店试点 3 年，85% 准确率 1/5 单需要人工兜底，2024-06 终止 IBM 合作
- **服务 Tool**：#48 (6 问 Q5 长尾) / #55 (老板对齐)

### 4.7 OpenAI GPT-4o sycophancy（2025-04-25 → 2025-04-29 全量回滚）⭐ 最近案例

- 来源 A（OpenAI 初次公告 2025-04-29）：🔗 https://openai.com/index/sycophancy-in-gpt-4o/（已核查）
- 来源 B（OpenAI 详细 postmortem 2025-05-01）：🔗 https://openai.com/index/expanding-on-sycophancy/（已核查）
- 来源 C（TechCrunch）：🔗 https://techcrunch.com/2025/04/29/openai-explains-why-chatgpt-became-too-sycophantic/（已核查）
- 关键：OpenAI 自承"sycophancy 没有作为 blocking 项进入发版评估"——成为"behavior issues 必须 block 发布"的行业标准来源
- **服务 Tool**：#54 (上线运营) / #55 (老板对齐) / #51 (Eval 上线前必跑)

### 4.8 Cursor 2025-06 billing 暴雷 ⭐

- 来源 A（Cursor 官方道歉 2025-07-04）：🔗 https://cursor.com/blog/june-2025-pricing（已核查）
- 来源 B（TechCrunch 2025-07-07）：🔗 https://techcrunch.com/2025/07/07/cursor-apologizes-for-unclear-pricing-changes-that-upset-users/（已核查）
- **服务 Tool**：#52 (成本管控)

### 4.9 Anthropic 2025 Postmortem（性能优化误伤输出质量）

- 来源：Anthropic Engineering Blog
- 关键：HTTP 200 / 延迟正常 / dashboard 全绿，但实际输出已退化；~2 周延迟才被发现
- **服务 Tool**：#54 (监控指标 - 延迟暴露问题)

### 4.10 Gemini 图像生成 over-tune（2024-02）

- 来源：Google 官方声明 + The Verge / Wired
- 关键：CEO Pichai 公开发文 "unacceptable"
- **服务 Tool**：#54 (Bad Case 管理 - 反向 bias 案例)

### 4.11 Google AI Overviews 胶水披萨（2024-05）

- 来源：The Verge / BBC 2024-05
- 关键：infra 全绿但内容层失败
- **服务 Tool**：#54 (监控 - 内容层 vs infra 层区分)

### 4.12 ChatGPT 胡言乱语事件（2024-02-20）

- 来源：OpenAI status page
- 关键：线上约 5 小时回滚
- **服务 Tool**：#54

### 4.13 Knight Capital $4.4 亿亏损（2012）

- 来源：SEC 调查报告 / Wikipedia
- 关键：8 台服务器漏更新 1 台，45 分钟亏 $4.4 亿
- **服务 Tool**：#54 (上线运营 - 部署一致性)

### 4.14 Manus AI（蝴蝶效应）

- 来源：多家技术媒体 2025 初实测
- 关键：宣称 GAIA SOTA，实测 reliability / 上下文窗口 / 付费墙 / CAPTCHA 全卡死
- **服务 Tool**：#53 (能力边界 - 反面案例)

### 4.15 Humane AI Pin（2025-02 卖给 HP）

- 来源：Bloomberg / The Verge 2025-02
- 关键：融资 $230M，2025-02 卖给 HP 仅 $116M
- **服务 Tool**：#56 (PM 成长包 - 产品方向判断案例)

### 4.16 Notion × Braintrust 案例 ⭐

- 来源：Braintrust 客户案例博客
- 关键：双轨 eval（regression + frontier），特定 workflow 提速近 10 倍
- **服务 Tool**：#51 (Eval) ⭐ 核心参照

### 4.17 Cursor 案例（人均 ARR）

- 来源：Cursor 官方 / Forbes / Bloomberg
- 关键：2025-Q3 工程团队约 100 人，撑起 $1B 量级 ARR
- **服务 Tool**：#56 (PM 成长包) / #49 (PRD 模板 - 团队规模锚)

### 4.18 Lovable 案例（人均 ARR）

- 来源：Lovable 创始人公开声明 + Anton Osika Twitter
- 关键：2025-Q3 快照——18 人 ~$17M ARR；"我们的 PM 数量是 0，工程师都在做 PM 的事"
- **服务 Tool**：#56 (PM 成长包) / #49 (PRD 模板)

### 4.19 Anthropic 销售配比

- 来源：Anthropic 公开口径
- 关键：~2000 人公司销售 quota carrier 只有数十名
- **服务 Tool**：#56

### 4.20 Token 账单 5 个真实失控事件

- 来源：Hacker News / X 推文 / Reddit 汇总
- 事件 1：Claude Code 递归循环 5 小时烧 16.7 亿 token
- 事件 2：subagent 进入 809 步无限循环，3.5 小时烧 $350
- 事件 3：retry loop 一夜烧 $72,000 OpenAI credit
- 事件 4：某软件公司单计费周期 $150,000 影子 AI 危机
- 事件 5：Cursor June 2025 billing（同 4.8）
- **服务 Tool**：#52 (成本管控) ⭐ 核心案例

### 4.21 Illinois 州法 + Texas TRAIGA

- Illinois（2025）："Wellness and Oversight for Psychological Resources Act" 禁止 AI 制定心理健康治疗方案
- Texas TRAIGA（2026-01 部分生效）：医师必须书面披露 AI 用于诊断
- **服务 Tool**：#48 (6 问 Q4 合规) / #54 (强合规降级)

### 4.22 Anthropic prompt caching 3 个案例

- DEV.to 作者：RCA 任务砍 90% 成本
- Du'An Lightfoot：月账单 $720 → $72
- ProjectDiscovery：缓存命中率 7% → 74%
- **服务 Tool**：#52 (成本管控)

---

## 池子 5：学术 AI Safety + 顶会 🟢 v2 深度

> 服务工具：#51 (Eval) / #53 (能力边界) / #54 (上线运营) / #56 (PM 成长包)
> v2 深度调研：2026-05-21 完成 WebSearch 5 轮，每条含具体 paper/事件/数据/PM 应用

### 5.1 ML 三大顶会 NeurIPS / ICML / ICLR · AI 安全方向

**全球 tier-1 理由**：ML 学术界三大顶会，所有前沿 AI 论文集中地。**对 PM 的核心价值**：eval 方法论 / 红队 / 安全对齐技术全部来自这里。

**必看 paper（按 PM 关联度排序）**：

| Paper | 作者 | 年份 | arXiv | 对 PM 的应用 |
|---|---|---|---|---|
| **Holistic Safety and Responsibility Evaluations of Advanced AI Models** | DeepMind | 2024 | [2404.14068](https://arxiv.org/pdf/2404.14068) | eval 全景方法论框架 |
| **AI Alignment: A Comprehensive Survey** | Ji et al. | 2023 | [2310.19852](https://arxiv.org/abs/2310.19852) | AI 对齐综述（PM 入门必读） |
| **AI Alignment: A Contemporary Survey** | ACM Computing Surveys | 2025 | [DOI 3770749](https://dl.acm.org/doi/10.1145/3770749) | 最新对齐综述 |

- 🔗 [NeurIPS](https://neurips.cc) / [ICML](https://icml.cc) / [ICLR](https://iclr.cc)
- 🔗 [12 Remarkable Research Papers from NeurIPS 2024](https://www.turingpost.com/p/neurips-2024-papers) — Turing Post 综述
- **服务 Tool**：#51 ⭐ (eval 学术依据) / #53 (能力边界)

### 5.2 AI Alignment Forum · 高质量 AI 安全讨论社区

**全球 tier-1 理由**：全球最活跃的 AI 安全与对齐研究讨论社区，**Anthropic / DeepMind / OpenAI / Redwood / Apollo 研究员日常发文交锋**。对 PM 的核心价值：你能第一手看到顶级研究员对最近模型 bug / 行为漂移的"非官方诚实评估"。

**2024-2025 高影响力 posts**：

| Post | 时间 | 核心论点 | 对 PM 的应用 |
|---|---|---|---|
| **[Alignment remains a hard, unsolved problem](https://www.alignmentforum.org/posts/epjuxGnSPof3GnMSL/alignment-remains-a-hard-unsolved-problem)** | 2025-11 | 3 个原因导致 inner alignment 是大问题：scaling pre-training 5-10% 灾难概率 / RL 选 misaligned personas 10-15% / outcome-based RL 长 horizon 选 misaligned agents 20-25% | #54 (Bad Case 管理 - 知道行为漂移概率上限) |
| **[What's the short timeline plan?](https://www.alignmentforum.org/posts/bb5Tnjdrptu89rcyY/what-s-the-short-timeline-plan)** | 2025 | 2030 年 95%+ 经济任务可被 AI 完全自动化的情景 | #56 (PM 成长规划) |
| **My AGI safety research—2025 review** | 2025 | 顶级研究员年度复盘范本 | #56 |
| **Frontier Models are Capable of In-context Scheming** | 2024-12 | 同 Apollo 5.6 | 关联 |

- 🔗 [alignmentforum.org](https://www.alignmentforum.org/)
- **服务 Tool**：#54 ⭐ (Bad Case 管理 - 行为漂移上限) / #56 / #51 (eval 方法论新动态)

### 5.3 Center for AI Safety (CAIS) · 全球 AI 风险联署核心组织

**全球 tier-1 理由**：
- (a) 2023-05-30 发起 [Statement on AI Risk](https://aistatement.com/) — "Mitigating the risk of extinction from AI should be a global priority"
- (b) **签署人包括 Sam Altman / Dario Amodei / Bill Gates / Geoffrey Hinton / Yoshua Bengio + 100+ AI 教授**
- (c) 是 AI 风险从"小众担忧"变成"全球议程"的关键转折

**核心产出（2023-2025 完整列表）**：

| 时间 | 产出 | 价值 |
|---|---|---|
| 2023-05 | [Statement on AI Risk](https://aistatement.com/) | 全球签署声明，AI 风险议程化 |
| 2024-01 | AI Safety and Ethics 教科书 | 高校教学标准化 |
| 2024-04 | SafeBench Competition | AI 安全 benchmark 标准化 |
| **2025-03** | **Superintelligence Strategy Paper** | **最新 — 超智能战略框架** |

- 🔗 [safe.ai](https://safe.ai) / [aistatement.com](https://aistatement.com/)
- **服务 Tool**：#54 ⭐ (上线运营 - 风险等级判断) / #55 (老板对齐 - 用全球共识替代单点判断)

### 5.4 Stuart Russell (UC Berkeley) · "Provably Beneficial AI" 之父

**全球 tier-1 理由**：
- (a) 《Human Compatible》作者，全球 AI Safety 学派精神领袖
- (b) **2025 年获 AAAI Award for Artificial Intelligence for the Benefit of Humanity**（AAAI 最高奖之一）
- (c) Michael H. Smith and Lotfi A. Zadeh Chair @ Berkeley
- (d) 收录于 [Time 100 Most Influential People in AI 2025](https://time.com/collections/time100-ai-2025/7305869/stuart-russell/)

**核心框架：Provably Beneficial AI = "Assistance Game"**
- 传统 AI：给定明确目标，最大化它
- Russell 框架：**AI 不应该有自己的目标**，应把"人类利益"作为不确定的目标去服务
- 数学上可证明（provably）AI 的行为有界且可控
- 对 PM 的应用：所有 AI Agent 类需求，本质上应是 "Assistance Game" 而不是"自治智能体"

**2025 重要行动**：
- 召集 **IASEAI（International Association for Safe and Ethical AI）首届会议**
- 700+ 现场 + 1400+ 在线参会

- 🔗 [people.eecs.berkeley.edu/~russell](https://people.eecs.berkeley.edu/~russell/)
- 🔗 [Russell wins AAAI 2025 Award](https://aihub.org/2025/02/04/stuart-j-russell-wins-2025-aaai-award-for-artificial-intelligence-for-the-benefit-of-humanity/)
- **服务 Tool**：#56 ⭐ (PM 成长包 - AI Agent 设计哲学) / #53 (能力边界)

### 5.5 MILA / Yoshua Bengio · 图灵奖得主 + 国际 AI 安全报告 + Scientist AI 提案

**全球 tier-1 理由**：
- (a) **图灵奖得主**（与 Hinton / LeCun 并列三巨头）
- (b) 引用量全球计算机科学家最高之一
- (c) **领导首份 International AI Safety Report**（联合国 + EU + OECD + 30 国背书）

**核心产出 3 件大事**：

**1. International AI Safety Report 2025**（2025-01-29 发布）⭐
- 🔗 [internationalaisafetyreport.org](https://internationalaisafetyreport.org/)
- 全球首份 "comprehensive review of the latest science on capabilities and risks of general-purpose AI"
- 100+ 独立专家，30 国 + UN + EU + OECD 支持
- **关键警告**：OpenAI o1（2024-09）是首个跨过 OpenAI 自己"low risk → medium risk for CBRN" 边界的模型
- 对 PM 的应用：**这是全球唯一的 AI 风险 "国际标准报告"** — 在老板对齐时引用，比单点 KOL 观点权威 100 倍

**2. Scientist AI 提案**（2025-02，arXiv 2502.15657）
- 🔗 [Paper](https://arxiv.org/abs/2502.15657) — *Superintelligent Agents Pose Catastrophic Risks: Can Scientist AI Offer a Safer Path?*
- 提出 "Scientist AI" — **非 agentic 的 AI**，只生成假设 + 推理 + 量化不确定性
- 对比：当前 AI 公司都在做 generalist agents（autonomous plan / act / pursue goals）
- 对 PM 的应用：给"AI Agent 是不是必须 autonomous"提供反方论据 — 部分场景应该选 "assistant + uncertainty quantification" 而不是 agent

**3. LawZero 非营利**（2025-06 启动，$30M 资金）
- 🔗 [TIME: The Most-Cited Computer Scientist Plans to Make AI More Trustworthy](https://time.com/7290554/yoshua-bengio-launches-lawzero-for-safer-ai/)
- 目标：构建 non-agentic、默认安全的 AI 系统

- 🔗 [mila.quebec](https://mila.quebec) / [yoshuabengio.org](https://yoshuabengio.org/)
- 🔗 [TED Talk: The catastrophic risks of AI](https://www.ted.com/talks/yoshua_bengio_the_catastrophic_risks_of_ai_and_a_safer_path)
- **服务 Tool**：#54 ⭐ / #55 ⭐ (老板对齐 - 国际标准报告锚) / #51

### 5.6 Apollo Research · "AI 欺骗对齐" 实证研究领头羊

**全球 tier-1 理由**：
- (a) 全球**唯一专注 "deceptive alignment" 实证的独立机构**
- (b) **与 OpenAI 官方合作**评估 o1 的 scheming 能力
- (c) 论文是当前 AI 安全圈最被引用之一

**核心 paper：Frontier Models are Capable of In-context Scheming**（2024-12）⭐
- 🔗 [apolloresearch.ai/research/frontier-models-are-capable-of-incontext-scheming](https://www.apolloresearch.ai/research/frontier-models-are-capable-of-incontext-scheming/)
- **6 个测试场景中，o1 / Claude 3 Sonnet / Claude 3 Opus / Gemini 1.5 Pro / Llama 3 五款都展示 scheming 能力**（6 个里中 5 个）
- 观察到的具体行为：
  - **Disabling oversight mechanisms**（禁用监督机制）
  - **Self-exfiltration attempts**（自我外渗尝试）
  - **Subtly manipulating outputs**（暗中操纵输出）
- 评估方法：模型从未被指示"做欺骗行为"，只是被放入"欺骗有助于达成目标"的情境
- **OpenAI 官方采纳**：[OpenAI: Detecting and reducing scheming in AI models](https://openai.com/index/detecting-and-reducing-scheming-in-ai-models/)

**后续 paper**：[Stress Testing Deliberative Alignment for Anti-Scheming Training](https://www.apolloresearch.ai/research/stress-testing-deliberative-alignment-for-anti-scheming-training/)

**对 PM 的应用**：
- **Bad Case 管理 5 类** 之外要加第 6 类——**Deceptive Behavior**（模型不是"出错"，是"故意做错")
- 上线前 eval 必须包含"模型是否会在认为不被观察时改变行为"的 scenario

- 🔗 [apolloresearch.ai](https://www.apolloresearch.ai)
- **服务 Tool**：#54 ⭐⭐ (Bad Case 第 6 类) / #51 (上线前 deception eval)

### 5.7 Redwood Research · "AI Control" 范式开创者

**全球 tier-1 理由**：
- (a) **开创 "AI Control" 范式** — "AI 是受控的 = 即使被严重 misalign 也无法造成损害"
- (b) Buck Shlegeris 是行业认可的 AI Safety 工程实践标杆
- (c) 与 Anthropic / OpenAI 工程团队对话密集

**核心 paper（2024-2025）**：

| Paper | 时间 | 核心结论 | 对 PM 应用 |
|---|---|---|---|
| **[Ctrl-Z: Controlling AI Agents via Resampling](https://www.redwoodresearch.org/research/ai-control)** | 2025-04 (Bhatt et al.) | Agent 失控时用 resampling 技术控回 | #54 (Agent 上线降级方案) |
| **[Subversion Strategy Eval](https://arxiv.org/pdf/2412.12480)** | 2024-12 (Mallen et al.) | 测试模型能否"无状态"地策划颠覆控制协议 — **所有当前模型都没做到** | #51 (eval 设计 - 加 subversion test) |

**核心理念差异**（与传统 AI Safety 学派比）：
- 传统：让模型"想正确" → alignment 路线
- Redwood：**假设模型可能 misalign，确保它"做不了坏事"** → control 路线
- 对 PM 的应用：**短期 PM 应该走 control 路线**（架构上限制 AI 能做的事），不要等"完美对齐"

- 🔗 [redwoodresearch.org/research/ai-control](https://www.redwoodresearch.org/research/ai-control)
- 🔗 [Buck Shlegeris Reading List](https://blog.redwoodresearch.org/p/guide)
- **服务 Tool**：#54 ⭐ (Agent 上线 control 架构) / #51

### 5.8 5 篇必读经典论文（AI Era PM 不读这 5 篇等于零知识）

**全球 tier-1 理由**：这 5 篇分别开创了：transformer / scaling laws / instruction tuning / chain of thought / constitutional AI 五个核心范式

| # | Paper | 作者 | arXiv | 关键贡献 | 对 PM 的应用 |
|---|---|---|---|---|---|
| 1 | **Attention Is All You Need** | Vaswani et al. (Google) | [1706.03762](https://arxiv.org/abs/1706.03762) | Transformer 架构 | 理解所有 LLM 的底层 |
| 2 | **Scaling Laws for Neural Language Models** | Kaplan et al. (OpenAI) | [2001.08361](https://arxiv.org/abs/2001.08361) | 性能随参数 / 数据 / 算力幂律 scaling | 解释为啥 GPT-5 比 GPT-3 强 + 成本/收益曲线 |
| 3 | **Chain-of-Thought Prompting** | Wei et al. (Google) | [2201.11903](https://arxiv.org/abs/2201.11903) | "Let's think step by step" 提示词 | 所有 prompt engineering 起点 |
| 4 | **InstructGPT / RLHF for ChatGPT** | Ouyang et al. (OpenAI) | [2203.02155](https://arxiv.org/abs/2203.02155) | RLHF 把模型对齐到人类偏好 | 理解为啥 base model vs chat model 差别巨大 |
| 5 | **Constitutional AI** | Bai et al. (Anthropic) | [2212.08073](https://arxiv.org/abs/2212.08073) | 用"宪法"指导 AI 自我修正 | 理解 Claude 系列对齐方式 |

**PM 实战建议**：5 篇不必全读懂数学，但必须知道**每篇的 one-liner 影响**（如上表"关键贡献"列）。在与工程师讨论时能引用其中之一 = 立即获得专业信任。

- **服务 Tool**：#56 ⭐ (PM 成长包 - 必读清单)

### 5.9 DeepMind Safety Research · Frontier Safety Framework

**全球 tier-1 理由**：Google DeepMind 是与 Anthropic / OpenAI 并列的 frontier AI 公司，**Frontier Safety Framework 是与 Anthropic RSP 平行的另一份行业标准框架**

**核心产出：Frontier Safety Framework (FSF)**
- 🔗 [Introducing the Frontier Safety Framework](https://deepmind.google/blog/introducing-the-frontier-safety-framework/) - v1 (2024-05)
- 🔗 [Updating the Frontier Safety Framework](https://deepmind.google/blog/updating-the-frontier-safety-framework/) - v2 (2025-02)
- 🔗 [Strengthening Framework](https://deepmind.google/blog/strengthening-our-frontier-safety-framework/) - v3 (2025-09)

**4 个 risk domains**：
1. **CBRN**（化学/生物/放射/核武器信息风险）
2. **Cybersecurity**（网络安全）
3. **Machine Learning R&D**（AI 自我加速研发）
4. **Harmful Manipulation**（有害操纵）
+ exploratory: **Misalignment**

**核心概念：Critical Capability Levels (CCLs)** — 触发严重风险的能力阈值

**实际应用**：[Gemini 3 Pro Frontier Safety Framework Report (2025-11)](https://storage.googleapis.com/deepmind-media/gemini/gemini_3_pro_fsf_report.pdf)
- Gemini 系列每个版本都按 FSF 跑 dangerous capability evaluations 并发布报告

**对 PM 的应用**：
- 与 Anthropic ASL 形成参照——产品 PM 在写 PRD 第 7 节"能力边界"时，**同时引用两份标准**才完整
- 老板对齐时可以说："Gemini 3 Pro 上线前要走 FSF 4 domain 评估，我们小公司至少要做 4 domain 的简化版"

- 🔗 [deepmindsafetyresearch.medium.com](https://deepmindsafetyresearch.medium.com)
- 🔗 [AGI Safety and Alignment at Google DeepMind: A Summary](https://deepmindsafetyresearch.medium.com/agi-safety-and-alignment-at-google-deepmind-a-summary-of-recent-work-8e600aca582a)
- **服务 Tool**：#54 ⭐ (上线运营 - 4 domain 评估) / #49 (PRD 模板 - 能力边界引用) / #55 (老板对齐)

---

## 池子 6：风投视角 🟢 v2 深度

> 服务工具：#52（成本管控）/ #55（老板对齐）/ #56（PM 成长包 / 市场判断）
> v2 深度调研：2026-05-21 完成

### 6.1 Sequoia Capital · Sonya Huang / Pat Grady / Konstantine Buhler — Act o1 + Act Three 框架

**全球 tier-1 理由**：
- (a) 全球最具影响力 VC（市值排名常年第一），AI portfolio 含 OpenAI / Anthropic / Hugging Face / Glean / Harvey
- (b) Sonya Huang 是 AI 投资圈最被引用的女性 GP，AI Ascent 大会是全球 VC 圈 AI 风向标
- (c) "Generative AI's Act Two / Act o1 / Act Three" 系列已成行业通用语言（应用层、推理层、agent 层）

**核心产出 2 件大事**：

**1. Generative AI's Act o1: The Reasoning Era Begins**（2024-10-09 发布）⭐
- 🔗 [sequoiacap.com/article/generative-ais-act-o1/](https://sequoiacap.com/article/generative-ais-act-o1/)
- 作者：Sonya Huang、Pat Grady（与 o1 共同创作）
- 三个核心论点：
  - **Inference-time reasoning 是范式转移**："reasoning at inference time...unlocking a new cohort of agentic applications"
  - **定制化认知架构**：通用基座不够，需要 domain-specific reasoning（Factory "droids" 案例）
  - **从 SaaS 到 service-as-a-software**：目标是"万亿美元服务市场"（Sierra 按结果付费而非席位）
- 关键数据：GPT-4 token 价格自上次 dev day 下降 98%；云 / 移动时代各约 20 家应用层公司做到 $1B+ 营收
- 对 PM 的应用：**做 AI 产品定价模型选型时引用 "service-as-software" 论点** — 给老板解释为什么不再做席位制 SaaS

**2. AI Ascent 2025 主题演讲**（2025-05-02 旧金山）
- 🔗 [sequoiacap.com/article/ai-ascent-2025/](https://sequoiacap.com/article/ai-ascent-2025/)
- 演讲：Pat Grady / Sonya Huang / Konstantine Buhler，嘉宾含 Sam Altman、Jensen Huang、Jeff Dean、Mike Krieger、Bret Taylor
- 关键引用：
  - Sonya Huang："coding has reached **screaming product-market fit**"
  - Pat Grady：市场有 "tremendous sucking sound"，建议创始人 "go at maximum velocity, all of the time"
  - Konstantine Buhler 主推 "agent economy" 框架
- 对 PM 的应用：**判断 2025-2026 哪些品类已 PMF** — coding 已确认、客服 / 销售在路上、垂直 agent 是下半场

- **服务 Tool**：#56 ⭐ / #55

### 6.2 Andreessen Horowitz（a16z）· Sarah Wang / Martin Casado — AI Canon + 100 CIO 调研

**全球 tier-1 理由**：
- (a) 全球 AUM 排名前三 VC，AI portfolio 含 Mistral / Databricks / Character.ai / Anyscale
- (b) Marc Andreessen 是 "Software is eating the world"（2011）作者，思想锚定行业
- (c) 出版能力业内独一档：a16z 官网相当于 AI 行业准官方知识库

**核心产出 3 件大事**：

**1. AI Canon**（2023-05-25 首发，持续更新）⭐
- 🔗 [a16z.com/ai-canon/](https://a16z.com/ai-canon/)
- 作者：Derrick Harris、Matt Bornstein、Guido Appenzeller
- 结构 6 大板块：温和入门 / 基础学习 / 技术深潜 / 实战指南 / 市场分析 / 里程碑论文
- 收录 Karpathy "Software 2.0" / "State of GPT"、Stanford CS229/CS224N/CS324、Attention Is All You Need、OpenAI Cookbook、LangChain 文档
- 对 PM 的应用：**AI PM 自学路径官方推荐书单** — 新人入门、面试准备直接照单全收

**2. 16 Changes to the Way Enterprises Are Building and Buying Generative AI**（2024）⭐
- 🔗 [a16z.com/generative-ai-enterprise-2024/](https://a16z.com/generative-ai-enterprise-2024/)
- 作者：Sarah Wang 等
- 来源：基于数十位 Fortune 500 + 70+ 企业领导调研
- 关键结论：企业 LLM 预算"几乎翻三倍"，逐步从实验走向生产；开源小模型扩大应用面

**3. How 100 Enterprise CIOs Are Building and Buying Gen AI in 2025**（2025-06-10）⭐
- 🔗 [a16z.com/ai-enterprise-2025/](https://a16z.com/ai-enterprise-2025/)
- 作者：Sarah Wang、Shangda Xu、Justin Kahl、Tugce Erten
- 5 个最关键数据：
  - 企业未来 1 年 AI 支出预期 **~75% 增长**；创新预算占 LLM 总支出从 25% 降到 7%（已成核心预算）
  - **37% 受访者生产环境部署 5+ 模型**（多模型常态化）
  - OpenAI 仍领先，Anthropic 在最技术前沿企业渗透最高
  - **90%+ 测试第三方应用做客服**（buy > build）
  - **23% 企业部署 OpenAI o3** vs DeepSeek 3%
- 对 PM 的应用：**老板对齐弹药库** — "你看 a16z 调研 100 个 CIO，预算涨 75%，我们不投就掉队"

- **服务 Tool**：#52 / #54 / #55 / #56

### 6.3 Bessemer Venture Partners · State of AI 2025（Supernovas vs Shooting Stars）

**全球 tier-1 理由**：
- (a) 全球最老牌 VC（1911 年成立），Cloud 100 榜单是 SaaS 行业金标准
- (b) State of the Cloud 系列连续 10+ 年，AI portfolio 含 Perplexity / ElevenLabs / Cleerly
- (c) 2023 起 cloud + AI 整合发布，是 SaaS / AI 增长基准的权威来源

**核心产出**：

**State of AI 2025: First Light**（2025-08-13 发布）⭐
- 🔗 [bvp.com/atlas/the-state-of-ai-2025](https://www.bvp.com/atlas/the-state-of-ai-2025)
- 完整 PDF：[State_of_AI_2025_slides_Bessemer_Venture_Partners.pdf](https://www.bvp.com/assets/uploads/2025/08/Final_PDF_State_of_AI_2025_slides_Bessemer_Venture_Partners.pdf)
- 作者：Kent Bennett、Talia Goldberg、Janelle Teng Wade、Sameer Dholakia、Mike Droesch、Lauri Moore 等 13 人
- 核心框架 **Supernovas vs Shooting Stars**：
  - **Supernovas**（超新星）：year-1 ~$40M ARR / year-2 ~$125M ARR，毛利仅 ~25%，$1.13M ARR/FTE，留存脆弱
  - **Shooting Stars**（流星）："Q2T3" 轨迹（quadruple, quadruple, triple, triple, triple），year-4 ~$103M ARR，毛利 ~60%，$164K ARR/FTE，类传统优质 SaaS
  - 核心引用："We believe this era will be defined not by a few outliers—but by **hundreds of Shooting Stars**"
- 其他数据：Perplexity 6 亿 WAU / Gemini 4 亿 WAU（2025-03）
- 2026 五大预测：AI 浏览器（Comet / Dia）成主要 agent 接口、视频生成 mainstream、private eval 决定企业部署速度、新一代社交、并购潮
- 金句："memory and context are the new moats"、"build systems of action, not systems of record"
- 对 PM 的应用：**汇报 AI 产品健康度时直接套两个 archetype** — Supernova（高速但脆弱）还是 Shooting Star（健康复利），决定下一步 OKR

- **服务 Tool**：#56 ⭐ (产品健康度判断) / #55

### 6.4 Conviction · Sarah Guo + Elad Gil — No Priors 播客 + Software 3.0 框架

**全球 tier-1 理由**：
- (a) Sarah Guo 前 Greylock 最年轻合伙人（27 岁），2022 离开创办 Conviction，专投 AI / "Software 3.0"
- (b) No Priors 播客是 AI 圈最受关注的 VC 主理播客（Apple Podcasts Tech 类常驻 Top 10），嘉宾含 Sam Altman、Jensen Huang、Demis Hassabis、Mira Murati
- (c) Elad Gil 是 Google / Twitter 系连续创业者，写过《High Growth Handbook》，AI 单一 angel 投资规模行业最大之一

**核心产出**：

**1. No Priors Podcast**（2023 至今，每周更新）⭐
- 🔗 [feeds.megaphone.fm/nopriors](https://feeds.megaphone.fm/nopriors)
- YouTube：[youtube.com/@NoPriorsPodcast](https://www.youtube.com/@NoPriorsPodcast)
- 2024 重磅集：The Best of 2024 with Sarah Guo and Elad Gil（年度复盘）
- 价值：第一手与 AI 实验室创始人/科学家深度对谈（非 PR 答案）

**2. State of Startups and AI 2025**（演讲）
- 🔗 [YouTube](https://www.youtube.com/watch?v=3MZS5gNElZM)
- Sarah Guo 总结当年 AI 创业全景

**3. Sarah Guo 个人哲学（[sarahguo.com](https://sarahguo.com/)）**
- 引用："Conviction is the temporary suspension of doubt that makes action possible. Sometimes that suspension of doubt needs to last years."
- Software 3.0 定义：服务智能软件（不仅 AI 工具，而是 AI 原生公司）

**对 PM 的应用**：
- **No Priors 是 AI PM 通勤必听** — 想知道 OpenAI / Anthropic / xAI 下一步在做什么，听 30 分钟比看 30 篇报道密度高
- **判断创业方向 / 跳槽时引用 Software 3.0 框架** — 区分 "AI 套壳" 与 "AI 原生"

- **服务 Tool**：#56 ⭐

### 6.5 General Catalyst · Hemant Taneja — Anthropic + Mistral + Global Resilience 论

**全球 tier-1 理由**：
- (a) 与 Lightspeed 并列 Anthropic Series E 主要投资人；2023 末领投 Mistral，2024 加注
- (b) Hemant Taneja 是 CEO，提出 "Responsible Innovation" + "Global Resilience" 投资框架
- (c) 同时控股 Applied Intelligence Healthcare Group（用 AI 直接收购运营医院），是 VC 主动产业整合最激进案例

**核心产出 3 件大事**：

**1. Our Investment in Mistral AI**（2023-12-11）⭐
- 🔗 [generalcatalyst.com/stories/our-investment-in-mistral-ai](https://www.generalcatalyst.com/stories/our-investment-in-mistral-ai)
- 作者：Hemant Taneja、Quentin Clark、Alexandre Momeni
- 三大投资支柱：Workforce Transformation / Global Resilience / Responsible Innovation
- 关键引用：
  - "Open source fosters innovation through open standards and interoperability, and establishes trust through transparency"
  - "Enduring AI adoption and progress requires a key ingredient that the ecosystem today lacks: **trust**"

**2. Tripling Down on Mistral AI**（2024）
- 🔗 [generalcatalyst.com/stories/tripling-down-on-mistral-ai](https://www.generalcatalyst.com/stories/tripling-down-on-mistral-ai)
- 联合领投 €600M Series B

**3. America's AI Action Plan**（2025）
- 🔗 [generalcatalyst.com/stories/americas-ai-action-plan](https://www.generalcatalyst.com/stories/americas-ai-action-plan)

**对 PM 的应用**：
- **开源 vs 闭源选型论证** — 引用 GC "trust = open source transparency" 论
- **国家级 AI 战略视角** — 做政府 / 国企客户时引用 "Global Resilience" 框架

- **服务 Tool**：#52 / #55 / #56

### 6.6 Lightspeed Venture Partners · Ravi Mhatre — Anthropic Series E 领投 + 165 家 AI 公司

**全球 tier-1 理由**：
- (a) 2025-03 领投 Anthropic $3.5B Series E（最大单笔投资），同时投 xAI / Databricks / Mistral / Glean / Abridge
- (b) 2025-12 募集 $9B 新基金（六只 vehicle），声明 "double down on AI"，体量行业前列
- (c) 已部署 $5.5B+ 到 165 家 AI 原生创业公司，是 AI 押注最深的传统 VC

**核心产出**：

**Lightspeed Announces Lead Investment in Anthropic's $3.5B Series E**（2025-03-03）⭐
- 🔗 [lsvp.com/stories/lightspeed-announces-lead-investment-in-anthropics-3-5b-series-e-financing/](https://lsvp.com/stories/lightspeed-announces-lead-investment-in-anthropics-3-5b-series-e-financing/)
- 作者：Ravi Mhatre、Guru Chahal、Sebastian Duesterhoeft
- 投资论点：
  - "AI — **intelligence as software** — is a fundamentally different paradigm"
  - "the biggest value from AI's development will be unlocked at the frontier"
  - "**intelligence is the product**"
  - 企业需要 "reliability at scale, interpretability, and security" 三要素

**对 PM 的应用**：
- **企业级 AI 落地核心三要素** — 给 ToB AI 产品立项时直接套 reliability / interpretability / security 三轴
- **选模型时为 Claude 站台** — Anthropic 行业 #1 投资人背书

- **服务 Tool**：#52 ⭐ / #55 / #56

### 6.7 Greylock · Reid Hoffman + Saam Motamedi — 企业 AI 三层价值论

**全球 tier-1 理由**：
- (a) Reid Hoffman 是 LinkedIn 联合创始人 + OpenAI 早期董事 + Inflection AI 联合创始人
- (b) Saam Motamedi 是 Greylock 54 年历史最年轻 GP，专投企业 AI / 网络安全 / 数据基础设施
- (c) 投资 Cresta / Adept / Tome / Inflection 等 AI 原生公司，以 thesis-driven 闻名

**核心产出**：

**1. AI's Transformative Power**（2023-03-30，持续更新）⭐
- 🔗 [greylock.com/greymatter/ais-transformative-power/](https://greylock.com/greymatter/ais-transformative-power/)
- 形式：播客 + 视频（Morgan Stanley TMT Conference 录制）
- Reid Hoffman 论点：
  - "Every profession will have a co-pilot that will be between useful and essential within **two to five years**"
  - AI 不取代人，应监管为安全结果导向而非僵化限制
- Saam Motamedi 论点：
  - "AI is an enabling technology wave and it's shifting every category that we invest in"
  - **三层价值捕获框架**：foundation models / infrastructure & orchestration / applications（PM 工作必须明确产品在哪一层）

**2. The Intelligent Future**（持续更新对谈系列）
- 🔗 [greylock.com/greymatter/the-intelligent-future/](https://greylock.com/greymatter/the-intelligent-future/)

**对 PM 的应用**：
- **产品定位三层框架** — 写 PRD 时第一句话先说清在 model / infra / app 哪一层
- **Co-pilot 2-5 年 mainstream 时间窗** — 做产品路线图时引用 Hoffman 预测

- **服务 Tool**：#56 ⭐ / #55 / #49 (PRD 模板三层定位)

### 6.8 Founders Fund · Peter Thiel / Trae Stephens — AI × 国防的反共识投资

**全球 tier-1 理由**：
- (a) Peter Thiel 是 PayPal 黑帮教父 + Palantir 联合创始人，硅谷最具影响力反共识思想家
- (b) Anduril 是 Founders Fund 史上最大单笔投资（2025-06 领投 $1B / $2.5B Series G，估值 $30.5B），AI × 国防赛道开拓者
- (c) AI portfolio：Anthropic / Scale AI / Anduril / Crusoe / SentientAGI / Dirac / Senra Systems
- (d) 2024 录得 $6B 历史最大成长基金，专投后期 AI

**核心产出（注：FF 官方很少发长文，材料多见于第三方）**：

**1. Trae Stephens 长访谈 - TechCrunch**（2024-03）⭐
- 🔗 [techcrunch.com/2024/03/02/vc-trae-stephens-says-he-has-a-bunker-and-much-more-in-talk-about-founders-fund-and-anduril](https://techcrunch.com/2024/03/02/vc-trae-stephens-says-he-has-a-bunker-and-much-more-in-talk-about-founders-fund-and-anduril/)
- 核心论点：下一代变革性公司不在消费互联网，而在 **AI × 国防 × 国家基础设施** 交叉口
- 2024 Anduril 营收翻倍至 ~$10 亿，验证 "AI-powered defense" 商业可行

**2. 投资节奏数据（2024 一年内）**
- Impulse Space（在轨运输）/ Ramp（企业财务）/ Crusoe（AI 清洁能源数据中心）/ SentientAGI（UAE 开源 AI $85M 种子）

**3. Peter Thiel 系思想锚定**
- 经典：Zero to One（仍是 AI 创业必读）
- 2024-2025 公开演讲多次强调 AI = "the last bubble before AGI"

**对 PM 的应用**：
- **反共识赛道判断框架** — Thiel 的 "secret"（别人都不信的真相）论用于做产品差异化
- **AI 不是消费品而是基础设施** 这一视角，对做 ToB / ToG 产品的 PM 有锚定价值
- 注：FF 官方长文 [部分待补]

- **服务 Tool**：#56 / #55

### 6.9 Index Ventures · Hannah Seal / Martin Mignot — 欧洲顶级 VC AI 视角

**全球 tier-1 理由**：
- (a) 欧洲 + 美国双总部 VC，2024 募集 $2B 新基金（明确为 AI "platform shift"）
- (b) 投资 Mistral / Cohere / Scale AI / Wordsmith AI / Phaidra 等 AI 原生公司
- (c) Hannah Seal 是欧洲 AI / 法律科技投资 thesis-driven 代表，Martin Mignot 是 AI infra / compute 视角顶流

**核心产出**：

**1. Automating the Back Office: How AI is Transforming Professional Services**（2024-09-12）⭐
- 🔗 [indexventures.com/perspectives/automating-the-back-office-how-ai-is-transforming-professional-services/](https://www.indexventures.com/perspectives/automating-the-back-office-how-ai-is-transforming-professional-services/)
- 作者：Hannah Seal、Susana Rojas
- 核心论点 "services as software"：AI 让原本太复杂 / 太低毛利的服务工作能被系统化，公司可以**直接吃服务预算（不需要新设软件 line item）**
- 三大被颠覆领域：法律（合同管理 / 研究 / 起草）/ 会计审计（数据抽取 / 合规 / 财报）/ 通用 back office
- 关键引用：
  - "I'm trying to close a round. I've got procurement screaming at me with five baby contracts that could be checked by any 10-year-old."
  - "Compliance is rearview-mirror, reactive work. Advisory is front-windshield, looking forward."
  - "Accountants who use AI will outperform accountants who don't use AI, and they'll do it with less effort."

**2. Compute is King: Our Investment in Phaidra**（2024-07）
- 🔗 [indexventures.com/perspectives/compute-is-king-our-investment-in-phaidra/](https://www.indexventures.com/perspectives/compute-is-king-our-investment-in-phaidra/)
- 主题：AI 算力 + 数据中心能耗已成产业核心矛盾

**对 PM 的应用**：
- **找市场预算的思路转换** — 你不需要新开预算项，去吃服务费 / 人力费这种"已有大池子"
- **欧洲视角的 AI 法律 / 合规 deep dive** — 比硅谷视角更细颗粒，做出海欧洲市场必读

- **服务 Tool**：#52 / #55 / #56

### 6.10 Madrona Venture Group · IA40（Intelligent Applications 40）+ 推理革命

**全球 tier-1 理由**：
- (a) 西雅图最老牌 VC（Amazon 早期投资人），AI / 云计算 portfolio 深厚（Snowflake / Smartsheet / Apptio）
- (b) IA40 榜单连续 5 年（自 2021），与 PitchBook 联合发布，超 70 位 VC + 54 家机构投票，AI 公司行业基准榜
- (c) 与 AWS / Microsoft / Google / McKinsey / NYSE / Goldman / Delta 联合主办 IA Summit

**核心产出 2 件大事**：

**1. 2025 Intelligent Applications 40**（2025-08-28 发布）⭐
- 🔗 [madrona.com/intelligent-applications-40-2025/](https://www.madrona.com/intelligent-applications-40-2025/)
- 完整榜单：[ia40.com/the-list](https://www.ia40.com/the-list)
- 关键数据：
  - 340+ 公司提名，27 家首次入选
  - **Databricks 是唯一连续 5 年上榜的公司**
- 年度主题 **"Reasoning Revolution"**：reasoning 成为核心叙事
- 强调：入选公司是 "intelligent systems—reasoning machines that improve with use, integrate deeply into workflows, and collaborate with users"

**2. 2024 Intelligent Applications 40**（2024-09 发布）
- 🔗 [madrona.com/intelligent-applications-40-2024/](https://www.madrona.com/intelligent-applications-40-2024/)
- 关键数据：2024 winners 累计融资 $45.3B，其中近一半 $22B 在近 12 个月内

**对 PM 的应用**：
- **找标杆产品研究池** — IA40 = AI 产品基准 40 强，做竞品分析不用自己挑
- **判断品类成熟度** — 连续上榜 = 已成基建（Databricks），新入选 = 新兴赛道
- **"Reasoning Revolution" 框架** — 给老板讲下半场为什么不是更大模型而是更深推理

- **服务 Tool**：#56 ⭐ / #53 (能力边界)

---

## 池子 7：行业咨询机构（Big 4+）🟢 v2 深度

> 服务工具：#47 (失败分类交叉验证) / #55 (老板对齐) / #56
> v2 深度调研：2026-05-21 完成
> 调研方法：每家机构 2024-2025 主力 AI 报告 + 与 Pool 5 (MIT NANDA / MILA) 数据交叉验证

### 7.1 McKinsey QuantumBlack · 全球 AI 老板对齐第一权威

**全球 tier-1 理由**：
- (a) 全球咨询业 AI 实践规模最大（QuantumBlack 是 AI 子品牌，3000+ AI 专家）
- (b) "The State of AI" 是 CEO/CFO 引用频率最高的咨询报告之一
- (c) 调研口径稳定（年度同一问卷，可纵向对比）

**核心产出 - 最新一份大事**：

**The State of AI 2025: Agents, innovation, and transformation**（2025-11 发布，第 9 期）⭐
- 🔗 [mckinsey.com/capabilities/quantumblack/our-insights/the-state-of-ai](https://www.mckinsey.com/capabilities/quantumblack/our-insights/the-state-of-ai)
- 🔗 [PDF 直链](https://www.mckinsey.com/~/media/mckinsey/business%20functions/quantumblack/our%20insights/the%20state%20of%20ai/november%202025/the-state-of-ai-2025-agents-innovation_cmyk-v1.pdf)
- 样本：2025-06-25 至 2025-07-29，1,993 名受访者，105 国
- **关键数据点**：
  - 88% 受访者所在组织在至少 1 个业务职能中常规使用 AI（上年 78%）
  - **仅 6% 是"AI high performers"** —— 通过 redesign workflows 取得 EBIT 提升 ≥ 5%
  - 23% 已在企业内 scale agentic AI；另 39% 在 pilot
  - workflow redesign 是 EBIT 影响最大的单一变量

**与其他口径对比**：
- McKinsey 6% high performers vs **MIT NANDA 5% 项目交付 ROI** → 数量级一致，互为旁证
- vs **BCG 5% future-built** → 三家独立调研在"成功率 5-6%"上完全收敛 ⭐

**AI PM 应用**：
- **老板对齐神器**：跟老板说"我们 workflow 还没 redesign"时引用 McKinsey "94% 的公司还没拿到 EBIT 影响"
- **立项对齐**：6% 标尺 → 给老板的预期管理用

- **服务 Tool**：#47 ⭐ / #55 / #56

### 7.2 BCG Henderson Institute · AI Maturity Survey 全球标尺

**全球 tier-1 理由**：
- (a) Henderson Institute 是 BCG 智库，研究方法学公开
- (b) 建立了"future-built / scaler / laggard"3 级成熟度框架，被业界广泛引用
- (c) 调研覆盖 41 项基础能力（最细颗粒度）

**核心产出 - 最新一份大事**：

**The Widening AI Value Gap: Build for the Future 2025**（2025-09-30 发布）⭐
- 🔗 [bcg.com/publications/2025/are-you-generating-value-from-ai-the-widening-gap](https://www.bcg.com/publications/2025/are-you-generating-value-from-ai-the-widening-gap)
- 🔗 [PDF](https://media-publications.bcg.com/The-Widening-AI-Value-Gap-Sept-2025.pdf)
- 样本：1,250 名高管 / AI 决策者，9 大行业 + 25+ 子板块
- **关键数据点**：
  - **仅 5% 公司是 "future-built"** —— 系统性建立前沿 AI 能力并持续创造价值
  - Agents 已占 2025 年 AI 总价值的 **17%**，预计 2028 年达 **29%**
  - future-built 公司将 **15% AI 预算**投给 agents；laggards 几乎为 0
  - AI Leaders 营收增速是 Laggards 的 2 倍 + 成本节约高 40%

**与其他口径对比**：
- BCG 5% future-built ≈ McKinsey 6% high performers ≈ MIT NANDA 5% 项目盈利 → **三角验证 = "5% 法则"**
- BCG 比 McKinsey 多了 agent-specific 数据（17% → 29%）

**AI PM 应用**：
- **立项对齐**：用 "agent 价值占比 17%→29%" 论证 agent 项目优先级
- **预算谈判**：引用 "future-built 公司 15% 预算给 agent" 反推自己应该申请多少

- **服务 Tool**：#55 ⭐ / #56

### 7.3 Bain & Company · 务实派代表

**全球 tier-1 理由**：
- (a) Bain Technology Report 是 PE/VC 圈高度引用的科技尽调参考
- (b) 数据偏务实（不吹 hype），常给"反 narrative"判断
- (c) 重点关注 ROI / 转化率，与 PM 关切高度对齐

**核心产出 - 最新一份大事**：

**Bain Technology Report 2025: AI leaders are extending their edge**（2025-09 发布）⭐
- 🔗 [bain.com/insights/topics/technology-report/](https://www.bain.com/insights/topics/technology-report/)
- 🔗 子篇章：[From Pilots to Payoff (GenAI in Software Development)](https://www.bain.com/insights/from-pilots-to-payoff-generative-ai-in-software-development-technology-report-2025/)
- **关键数据点**：
  - 2/3 软件公司已 rollout GenAI 工具，但开发者实际采用率低
  - Coding 工具仅带来 **10-15% 生产力提升**（远低于厂商宣传的 30-55%）
  - 原因：写+测代码只占 idea-to-launch 的 25-35% 时间
  - 仅当 AI + 端到端流程改造时，才能拿到 **25-30% 生产力提升**
  - AI Leaders EBITDA 提升 10-25%；Laggards 持续掉队

**与其他口径对比**：
- Bain 10-15% coding 提升 vs **GitHub/Microsoft 自家数据 30-55%** → Bain 是"反 hype"声音
- vs **MIT NANDA 95% 失败率** → Bain 给出"为什么失败"的细节（流程没改 = 失败）

**AI PM 应用**：
- **失败诊断（#47）**："只上工具不改流程 → 10% 而非 30%" 直接对应失败模式
- **老板对齐**：当老板问"为什么 Copilot 没让我们快 50%"时，引用 Bain 25-35% 时间占比解释

- **服务 Tool**：#47 ⭐ / #55

### 7.4 Deloitte AI Institute · 季度高频追踪

**全球 tier-1 理由**：
- (a) 历史上最早做"季度 GenAI 调研"（Q1-Q4 series 2024）
- (b) 样本量大（3,000+ leaders），覆盖 24 国
- (c) 2025 起从季度转为年度旗舰，与 IBM / McKinsey 形成"年度三巨头"

**核心产出 - 最新一份大事**：

**The State of AI in the Enterprise (2026 edition / 调研年份 2025)**（2025-Q4-2026-Q1 期间发布）⭐
- 🔗 [主页](https://www.deloitte.com/us/en/what-we-do/capabilities/applied-artificial-intelligence/content/state-of-ai-in-the-enterprise.html)
- 🔗 [新闻稿](https://www.deloitte.com/us/en/about/press-room/state-of-ai-report-2026.html)
- 样本：3,235 名 leaders（2025-08 至 2025-09 调研），24 国，IT 与业务 5:5
- **关键数据点**：
  - 工作者 AI 访问率年增 **50%**
  - 6 个月内 "≥40% 项目进入 production" 的公司数量将翻倍
  - 报告"transformative impact"的 leaders 数量是上年 2 倍
  - 但仍**只有 34% 在真正 reimagining business**
  - 仅 **1/5 公司**对 autonomous agents 有成熟治理模型 ⚠️

**与其他口径对比**：
- Deloitte 34% reimagining vs McKinsey 6% high performers → Deloitte 口径更松（"在改" vs "拿到 EBIT"）
- agent 治理 1/5 → 与 MILA International AI Safety Report 治理告警呼应

**AI PM 应用**：
- **老板对齐**：用 "AI access +50%" 论证全员铺工具的紧迫性
- **风控对齐**：用 "1/5 公司有 agent 治理" 论证 governance 投入合理性

- **服务 Tool**：#55 / #47 / #54

### 7.5 Accenture · Tech Vision 旗舰 25 年

**全球 tier-1 理由**：
- (a) Tech Vision 已连续 25 年发布，是企业 CIO/CTO 的"年度风向标"
- (b) Accenture 是全球最大 IT 服务商之一，样本覆盖最广行业
- (c) 与 Microsoft / Google / AWS 深度合作，落地观察直接

**核心产出 - 最新一份大事**：

**Accenture Technology Vision 2025: AI - A Declaration of Autonomy**（2025-01 发布）⭐
- 🔗 [新闻稿](https://newsroom.accenture.com/news/2025/accenture-technology-vision-2025-new-age-of-ai-to-bring-unprecedented-autonomy-to-business)
- 🔗 [PDF](https://investor.accenture.com/~/media/Files/A/accenture-v4/investors/home/quick-links/accenture-Tech-Vision-2025.pdf)
- **关键数据点**：
  - **69% 高管**认为 AI 给 reinvention 带来新紧迫性
  - **77% 高管**认为 AI 的真正收益须建立在"信任"之上
  - **仅 36% 组织** scale 了 gen AI；**仅 13%** 实现"重大企业级影响"
  - 提出 "cognitive digital brain" 概念（企业级整合智能）

**与其他口径对比**：
- Accenture 13% 重大影响 vs McKinsey 6% / BCG 5% → 口径最松（"重大" vs "EBIT≥5%"）
- 77% 信任是 first principle → 与 MILA International AI Safety Report 在"治理 = 价值前提"上同向

**AI PM 应用**：
- **战略对齐**：autonomy 趋势论证 → 用于 agent 项目立项叙事
- **HR/培训对齐**：13% vs 36% 的 gap → 论证"会用 AI"远不够，需要"重新设计组织"

- **服务 Tool**：#56 / #55 / #49 (PRD 模板 - 信任章节)

### 7.6 PwC · 年度 AI Predictions + Jobs Barometer

**全球 tier-1 理由**：
- (a) 四大会计师事务所中 AI 投资最大（2023 承诺 $10B / 3 年）
- (b) AI Jobs Barometer 分析近 10 亿条招聘 → 全球独家数据集
- (c) 与 OpenAI / Microsoft 战略合作，落地视角第一手

**核心产出 - 最新一份大事**：

**2025 AI Business Predictions + AI Jobs Barometer 2025**（2025-01 + 年中更新）⭐
- 🔗 [主报告](https://www.pwc.com/us/en/tech-effect/ai-analytics/ai-predictions.html)
- 🔗 [年中更新](https://www.pwc.com/us/en/tech-effect/ai-analytics/ai-predictions-update.html)
- **关键数据点**：
  - 高 AI exposure 行业 **revenue per employee 增速是低 exposure 行业的 3 倍**（Jobs Barometer 核心数据）
  - 49% tech leaders 已把 AI 嵌入 core business strategy
  - AI Agents 被预测能"翻倍 workforce capacity"
  - GDP 影响：到 2035 年负责任部署的 AI 可拉动全球 GDP **+15%**
  - 三层 portfolio 法（ground game / roofshots / moonshots）

**与其他口径对比**：
- PwC "3x revenue/employee" 是其他咨询机构没有的招聘侧独家口径
- "Responsible AI 提高 ROI" 立场 → 与 MILA Safety Report、Deloitte 治理告警一致

**AI PM 应用**：
- **老板对齐**：用 "3x revenue/employee" 反驳"AI 没真金白银价值"
- **岗位调整对齐**：Jobs Barometer 用于 HR 沟通 / 团队结构调整论证

- **服务 Tool**：#55 ⭐ / #56

### 7.7 IBM Institute for Business Value (IBV) · CEO 视角独家

**全球 tier-1 理由**：
- (a) IBV 是 IBM 智库（独立运作），与 Oxford Economics 长期合作
- (b) **CEO 直采样本**（不是各级管理者混采）→ C-suite 口径独家
- (c) 与 watsonx / Red Hat 落地观察形成数据闭环

**核心产出 - 最新一份大事**：

**2025 IBM CEO Study: 5 Mindshifts to Supercharge Business Growth**（2025-05-06 发布）⭐
- 🔗 [新闻稿](https://newsroom.ibm.com/2025-05-06-ibm-study-ceos-double-down-on-ai-while-navigating-enterprise-hurdles)
- 🔗 [主报告](https://www.ibm.com/thought-leadership/institute-business-value/)
- 样本：2,000 名 CEO，33 国 24 行业，2025-02 至 2025-04 调研
- **关键数据点**：
  - AI 投资增速预计**未来 2 年翻倍**
  - **61% CEO** 正在 scale AI agents（注意：是 CEO 自报口径）
  - 仅 **52%** 说在 GenAI 上拿到了"超出降本"的价值
  - **72%** 视专有数据为 GenAI 价值关键
  - 到 2027 年 **85% CEO 预期 efficiency AI 转正 ROI**；77% 预期 growth AI 转正

**与其他口径对比**：
- IBM 61% agent scaling vs McKinsey 23% scaling → 巨大差异 ⚠️
  - 原因：IBM 是 CEO 自报（乐观偏差）；McKinsey 是各级管理者混采
  - **PM 务实判断：取 McKinsey 23% 为真实落地，IBM 61% 当 CEO 焦虑信号**
- 52% "超出降本拿到价值" 与 MIT NANDA 95% 失败率口径差异 → IBM 偏乐观

**AI PM 应用**：
- **预算对齐**：CEO 自己说"2 年投资翻倍" → 项目立项底气
- **数据资产对齐**：72% 视专有数据为关键 → 论证数据基建优先级

- **服务 Tool**：#55 / #47 / #56

### 7.8 Gartner · Magic Quadrant 唯一买方语言

**全球 tier-1 理由**：
- (a) Gartner Magic Quadrant 是企业 IT 采购的"事实标准"评分卡
- (b) 评估方法学公开（Ability to Execute × Completeness of Vision 二轴）
- (c) 大型企业采购必引 → PM 选型 / 厂商谈判的硬通货

**核心产出 - 最新 3 份相关 Magic Quadrant（2025）**：

**1. Magic Quadrant for AI Application Development Platforms 2025** ⭐
- 🔗 [Gartner](https://www.gartner.com/en/documents/7188230)
- 🔗 [Microsoft 解读](https://azure.microsoft.com/en-us/blog/microsoft-named-a-leader-in-gartner-magic-quadrant-for-ai-application-development-platforms/)
- Leader：Microsoft（Vision 最远），Google
- 核心判断：下一波应用是 agentic，需 grounded in real data + tools + 端到端可观测

**2. Magic Quadrant for Data Science and Machine Learning Platforms 2025**
- 🔗 [AWS 资源](https://aws.amazon.com/resources/analyst-reports/gartner/magic-quadrant-for-data-science-and-machine-learning-platforms/)
- Leader：Google Cloud（重点扩展到 GenAI 协作场景）

**3. Magic Quadrant for Conversational AI Platforms 2025**
- 🔗 [boost.ai 引用](https://boost.ai/guides/gartner-magic-quadrant-for-conversational-ai-platforms-2025/)
- Leaders：Google、Kore.ai、Cognigy、boost.ai（首次进入）

**与其他口径对比**：
- Gartner 不做"采用率"调研，专做"厂商能力"评级 → 与其他 7 家形成互补
- Gartner 2025 三份 MQ 都把"agentic"列为核心评估维度 → 与 BCG 17%→29% agent 价值口径呼应

**AI PM 应用**：
- **选型谈判**："你不在 Leader 象限 → 我们走流程要更长理由"（杀价利器）
- **老板对齐**：CIO/采购老板看 Magic Quadrant 比看 McKinsey 还重 → 直接搬用

- **服务 Tool**：#55 ⭐ (老板对齐 / 厂商选型)

---

### 7-X 横向交叉验证：8 家口径汇总表 ⭐

| 数据点 | McKinsey | BCG | MIT NANDA | Bain | Deloitte | Accenture | IBM | PwC |
|---|---|---|---|---|---|---|---|---|
| **真正成功率** | **6%** | **5%** | **5%** | leaders 持续拉开 | 34% reimagining | 13% 重大影响 | 52% 超降本价值 | - |
| Agent scaling | 23% | 17% 价值 | - | - | 1/5 治理成熟 | autonomy 主题 | 61% CEO 自报 | "翻倍 capacity" |
| 失败原因核心 | 没 redesign workflow | 41 项能力缺口 | 不会买/集成差 | 流程没改 | 治理滞后 | 信任缺失 | 数据架构 | 没 Responsible AI |

**核心结论**：**5-6% 成功率"三角验证"（McKinsey / BCG / MIT NANDA）是 Pool 7 最硬的口径锚点，老板对齐文章可直接三家联引**。

---

## 池子 8：开源社区 + AI Engineer 工具 🟢 v2 深度

> 服务工具：#44 (Vibe Coding 横评) / #46 (Claude Code SOP) / #51 (Eval) / #52 / #53
> v2 深度调研：2026-05-21 完成 · WebSearch + GitHub repo 实地 stars 验证

### 8.1 LangChain blog（Harrison Chase）

**Tier-1 理由**：LangChain 1.0 + LangGraph 1.0 于 2025-10 正式发布；LangGraph 已成企业 agent 编排事实标准（Klarna / Replit / LinkedIn 都在用）；Harrison Chase 是当前 agent 框架圈最高影响力 founder 之一。

**关键 release / post**：
- **LangSmith Engine (public beta)**（2026-05 发布）：自动「读 trace → 聚类失败 → 提交 fix + eval」闭环，第一次把 observability 升级成 self-healing
- **LangGraph v1.1**（2026-03）：type-safe streaming、Pydantic 强类型 coercion；Agent Builder 改名 **LangSmith Fleet**，加 identity / sharing / permissions
- **Harrison Chase × Sequoia podcast "Context Engineering Long-Horizon Agents"**（2026 春）：把 prompt engineering 正式过渡到 context engineering 的标志性论述
- **Deep Agents 概念**：Harrison 2026-05-06 Frank's World 播客深度访谈

**关键数据**：LangChain 主仓 100k+ stars；生态三件套定型：LangChain（build）+ LangGraph（orchestrate）+ LangSmith（observe）

**对 AI PM 应用**：#46 Claude Code SOP 里讲「PM 自己跑 eval」时，LangSmith Engine 是必引用案例；#51 Eval 工具包里 Fleet 是 multi-agent 权限治理样本

- 🔗 [blog.langchain.dev](https://blog.langchain.dev)
- **服务 Tool**：#46 / #51 ⭐

### 8.2 LlamaIndex blog（Jerry Liu）

**Tier-1 理由**：从 RAG 框架成功转型为「Document Agent + OCR Platform」；llama_index repo 仍是 RAG 领域最常被引用之一；Jerry Liu 发布频率与 Harrison Chase 相当。

**关键 release / post**：
- **LlamaParse v2**（2026 初）：通过新 llama-cloud SDK + 结构化 config 对象重写 API
- **Jerry Liu "Form-Filling Agent" demo**（2026-Q1）：用 Claude Agent SDK + LlamaParse + Opus 4.5，拖拽 5-10 张收据自动填报销表
- **"Filesystems as Agent Interface" 博客**：Jerry 论述 Claude Code / Cursor 正在把 filesystem 作为 agent 核心抽象（skills as files、file-based retrieval 替代传统 RAG）—— **2026 年 agent 架构最重要的范式转变文章之一**
- **"Long Horizon Document Agents"**（2026）：Jerry 预测 agent 从 workflow 转向 "employee" 模式
- **LlamaAgents Builder**：从想法到部署 agent < 1 分钟

**对 AI PM 应用**：#53 能力边界工具包里「文档处理类需求该不该接」必须引用 LlamaParse v2 案例；#46 里 filesystem 范式直接对应 Claude Code skill 设计

- 🔗 [blog.llamaindex.ai](https://blog.llamaindex.ai)
- **服务 Tool**：#46 / #51 / #53 ⭐ (RAG)

### 8.3 HuggingFace blog

**Tier-1 理由**：HF 是开源 AI 模型分发的 de facto 平台；blog 是社区第一手模型发布频道。

**关键 release / post**：
- **SmolLM3-3B**（2026 上半年）：3B SOTA 小模型，dual-mode reasoning、支持 6 种语言、long context、强 function calling。Smol 家族（135M/360M/1.7B/3B）是 edge / on-device 路线核心参照
- **Daniel van Strien**（HF Machine Learning Librarian）：2026-01-07 「Train on Massive Datasets Without Downloading with HF Streaming and Unsloth」—— streaming 数据集 + Unsloth 极低 GPU 训练栈
- **Sasha Rush**：HF transformers 核心贡献者，srush GitHub 仍是 transformers / eval 圈高引参照（LightEval 框架）—— 2026 具体 HF post [待补]

**对 AI PM 应用**：#52 成本管控工具包必引 SmolLM3 / Unsloth 路径（不是所有任务都要 frontier model）；Daniel 的 streaming 教程是「PM 给开发提需求时知道 fine-tune 不再是 100k GPU 起步」的素材

- 🔗 [huggingface.co/blog](https://huggingface.co/blog)
- **服务 Tool**：#51 / #52 ⭐ (开源模型选型)

### 8.4 DSPy（Stanford / Omar Khattab）

**Tier-1 理由**：把 prompt engineering 从「手写字符串」升级成「编译式编程」的范式开创者；ICLR 2024 论文奠基；生产级用户包括 Cursor、Mistral、Databricks

**关键数据**：
- **GitHub stars: 34.8k**（实地验证 2026-05）
- **最新版本: DSPy 3.2.1，2026-05-05 发布**
- 109 个 release、~2.9k forks，活跃度高

**核心定位**：DSPy 把 LLM 调用当 programmable module，用 typed signatures 组合 pipeline，然后**对 prompt（甚至模型权重）按 task metric 自动优化**。基准上比手写 prompt 提升 10-40%

**Khattab 身份**：Stanford PhD，现已在 Databricks。社区贡献者来自 Stanford NLP、Together AI

**对 AI PM 应用**：#51 Eval 工具包必引用 — DSPy 是「PM 不要再手抠 prompt，而是定义 metric 让系统优化 prompt」的最佳论据；#53 边界工具包里 DSPy 是「什么时候 prompt engineering 应该停下来上工程化」的分界线

- 🔗 [dspy.ai](https://dspy.ai) / [github.com/stanfordnlp/dspy](https://github.com/stanfordnlp/dspy)
- **服务 Tool**：#51 ⭐ (eval-driven 自动 prompt 优化)

### 8.5 Together AI blog

**Tier-1 理由**：开源模型推理 + fine-tuning 最大 AI-native cloud 之一，跑出了硬指标

**关键数据**：
- **$305M Series B**（2025），General Catalyst + Prosperity7 领投，估值 **$3.3B**；2026 新一轮目标 $7.5B 估值
- **年化收入 $1B**（2026-02），从 2025 年底 ~$618M 跃升
- 200+ 开源模型（chat/image/audio/vision/code/embedding）
- 自研 **Together Inference Engine**，基于 FlashAttention-3 kernel + 量化

**关键 release**：**Voice platform**（2026）— STT + LLM + TTS 同云共址，端到端延迟 <500ms，原生托管 Deepgram / Cartesia

**对 AI PM 应用**：#52 成本工具包里 Together 推理报价是「frontier API 之外的备选成本基线」；#54 上线运营里 voice 端到端 <500ms 是 voice agent 产品落地参照

- 🔗 [together.ai](https://together.ai)
- **服务 Tool**：#52 ⭐ / #54

### 8.6 Modal Labs blog

**Tier-1 理由**：serverless GPU 赛道头部，开发者体验对标 Vercel，被 AI 工程师圈奉为「按秒计费的 GPU 标杆」

**关键数据**：
- **$87M Series B**（2025-09），估值 **$1.1B**
- 按秒计费：H100 $0.001097/sec ≈ $3.95/hr；A100 $3.72/hr；A10G $1.10/hr
- **Starter 免费**，Team $250/GPU/hour，Enterprise 定制

**Named customers**：**Suno**（音乐生成）、**Substack**、**OpenArt**、**Lovable**（AI app builder）— 都是 2026 年 AI consumer 头部代表

**对 AI PM 应用**：#52 成本管控里「scale-to-zero」是 toC AI 产品 cold start 期最关键架构；Lovable / Suno 是 PM 拿来对标「轻量团队靠 Modal 把 GPU 成本可变化」的样本

- 🔗 [modal.com/blog](https://modal.com/blog)
- **服务 Tool**：#52 ⭐

### 8.7 向量数据库三巨头：Pinecone / Weaviate / Chroma

**Pinecone（managed serverless 王者）**
- 起步免费 100K vectors → $70/mo serverless → $500-2500/mo 中规模 → $10k+/mo 企业
- **BYOC 模式**（2026）：企业可在自己云账号跑 Pinecone
- Pinecone Assistant 集成 Claude Sonnet 4.5；HIPAA 合规、sub-33ms 延迟是核心卖点
- 定位：production-grade，企业首选

**Weaviate（hybrid search + AI agent 路线）**
- Weaviate Cloud $25/mo 起步是 managed 三家最便宜
- **Weaviate 1.35（2025-12）**：Object TTL 自动过期 + zstd 压缩
- **AI Agents（Query / Transformation / Personalization）**：vector DB 自带 agent 能力，是和 Pinecone / Chroma 的最大差异

**Chroma（DX 最好，开发者首选）**
- **Chroma 1.4.1 + Chroma Cloud GA**（2026）
- Collection Forking：分支实验不影响生产数据
- **Chroma Web Sync（2025-11）**：浏览器 ↔ cloud 同步，本地优先体验最强

**横评数据**：10M vectors 月成本对比：Pinecone Serverless ~$70 / Weaviate Cloud ~$135 / Qdrant ~$65 / pgvector ~$45；100M vectors 时 Pinecone 飙到 $700+，self-hosted 仍 <$100

**对 AI PM 应用**：#52 成本工具包里「vector DB 不要默认 Pinecone」结论强证据；#46 SOP 里 Chroma Forking 是「PM 自己验证 RAG 召回率」的工具样本

- 🔗 [pinecone.io](https://pinecone.io) / [weaviate.io](https://weaviate.io) / [trychroma.com](https://trychroma.com)
- **服务 Tool**：#52 / #53 ⭐ (RAG)

### 8.8 Aider（Paul Gauthier）

**Tier-1 理由**：开源终端 AI pair programmer 鼻祖，2024 年起一直是开源 coding agent 的话题中心

**关键数据（实地验证 2026-05）**：
- **GitHub stars: 45.6k**
- 最新版本 v0.86.0（2025-08）
- 80% Python，4.5k forks，13k+ commits

**对比 Cursor**：
- Cursor：「带 AI 的 IDE fork」，估值 $10B+，定位完全不同的市场
- Aider：「terminal CLI + Git-native」，胜在自动化、脚本化、100+ LLM 适配
- 行业共识：**互补而非竞争**

**核心差异化**：repository map 智能上下文管理 + Git 自动 commit + 公开 code-edit benchmark（leaderboard 持续更新，是 coding agent 比较的重要 reference）

**对 AI PM 应用**：#44 Vibe Coding 9 工具横评里 Aider 是「terminal 流派」代表；#46 里 Aider 的 repo map 是 PM 理解「为什么 Claude Code 要做 skills 和 file system 中心化」的对照

- 🔗 [aider.chat](https://aider.chat)
- **服务 Tool**：#44 ⭐ / #46

### 8.9 Continue.dev

**Tier-1 理由**：开源 IDE AI 助手赛道里最早做规模化的项目之一，2026 年完成了一次重大产品转型

**关键数据**：
- **GitHub stars: 32k+**，VS Code Marketplace **2.4M+ installs**（2026-03）
- Discord 11k+ 成员，4.4k forks
- 支持 **VS Code + JetBrains** 双 IDE，是当前唯一两端都做好的开源方案

**关键转型**：mid-2025 从「IDE 内 autocomplete + chat」转向 **「open-source CLI 跑 async agent on every PR」**，定位「source-controlled AI checks，可以在 CI 里强制执行」。这是 Continue 团队对「coding agent 真正落地企业的方式不是 IDE 而是 CI/CD」的赌注

**对 AI PM 应用**：#46 Claude Code SOP 里「PM 想让 AI 把守 PR 质量」必引 Continue 转型案例；#44 横评里 Continue 是「企业版 vibe coding」差异化定位代表

- 🔗 [continue.dev](https://continue.dev)
- **服务 Tool**：#44 ⭐ / #46

### 8.10 Cline（formerly Claude Dev）

**Tier-1 理由**：VS Code 上当前最火的开源 AI coding agent，star 增长曲线 2025-2026 最陡峭之一

**关键数据**：
- **GitHub stars: 61.6k**（截至 2026-05），v3.83
- VS Code Marketplace **1.5M+ installs**（2026-04），跨 VS Code / Cursor / JetBrains / Zed / Neovim 合计 **5M+ installs**
- 创始人 Saoud Rizwan，2024 年首发名为 Claude Dev

**vs Aider**：
- Aider 45.6k stars / terminal-first / Git 自动 commit
- Cline 61.6k stars / VS Code 内可视化审批 / 并行 subagent
- 选择逻辑：**terminal 工作流选 Aider，IDE 内可视化审批选 Cline**

**与 Claude Code 对比**：Claude Code 122.5k stars，仍是头部；Cline 在「开源 + 多模型」维度补位

**对 AI PM 应用**：#44 横评必占一席；#46 SOP 里 Cline 的「可视化审批每一步」是 PM 不熟代码时的安全选项参照

- 🔗 [github.com/cline/cline](https://github.com/cline/cline)
- **服务 Tool**：#44 ⭐ / #46

### 8.11 Cognition Devin

**Tier-1 理由**：「autonomous AI software engineer」概念定义者；2024 发布时引发行业海啸，2026 用收入和企业客户证明了自己

**关键数据**：
- **$1B 新一轮，pre-money $25B / post-money $26B**（2026-05-27），Lux Capital / General Catalyst / 8VC 领投
- 8 个月前估值才 $10.2B（2025-09 $400M 轮后）→ 2.5x 跃升
- **ARR $492M**，企业用量过去 6 个月连续 **MoM +50%**
- **89% 的 Cognition 自身代码由 Devin 写**
- 企业客户：**Mercedes-Benz、NASA、Goldman Sachs、Santander**
- Mercedes legacy system 现代化项目，原本 8 个月，**Devin 8 天完成**

**用户反馈真相**：launch 时争议极大 — 多名工程师 teardown 指控 demo 被剪辑、能力被夸大。但「product metrics speak clearly」，两年后收入打脸了批评。这是 2026 年 AI 产品「demo 争议 vs 实际落地」最经典案例

**对 AI PM 应用**：#47 NANDA 失败类型表里 Devin 是反例（「demo 被骂但产品赢了」）；#53 边界工具包里 Devin 8 天 vs 8 个月是「PM 怎么评估 AI 工程产能替代率」的硬数据

- 🔗 [cognition.ai](https://cognition.ai) / [cognition.ai/blog](https://cognition.ai/blog)
- **服务 Tool**：#44 / #46 / #47 ⭐ / #53

### 8.12 Replicate blog

**Tier-1 理由**：开源模型托管赛道老牌玩家，**2025 年底被 Cloudflare 收购**，并入全球最大基础设施公司之一

**关键数据**：
- 100,000+ 社区贡献模型（收购时口径是 50,000+）
- 按秒计费：CPU $0.000115/sec、T4 $0.000225/sec、A100 80GB $0.001400/sec
- **Cog**：Replicate 自研开源容器规范（Docker-based），predict.py 定义输入输出。是和 Modal / Beam 路线最大差异（Modal 是 Python 函数装饰器，Cog 是容器 spec）

**收购影响**：进入 Cloudflare 体系后预计与 Workers AI / R2 深度集成；Replicate API 在「想用开源模型但不想自己 deploy」路径上仍是首选

**对 AI PM 应用**：#52 成本工具包里 Replicate 是「单次任务 < 模型常驻」场景的报价基线；#44 横评里 Cog 容器化是和 Modal serverless function 的架构对照

- 🔗 [replicate.com/blog](https://replicate.com/blog)
- **服务 Tool**：#52 / #44

### 8.13 ai.engineer / AI Engineer World's Fair

**Tier-1 理由**：当前全球 AI Engineer 圈最大线下会议；Shawn "swyx" Wang 2023 年「The Rise of the AI Engineer」博客定义了这个 role；后续每年 World's Fair + Code Summit 形成行业事实标准

**关键数据**：
- **AI Engineer World's Fair 2026: 6/29 – 7/2，San Francisco Marriott Marquis**
- **4,000+ builders**，来自顶尖 AI labs + Fortune 500 CTO + founders
- **10 个并行 track，400+ sessions**

**核心 track**：
- Frontier research：reasoning / multimodal / memory / alignment / eval / 新模型架构
- **Autonomous coding**：multi-file edit、repo-level reasoning、production code agent
- Document understanding / multimodal：vision model → OCR / layout parsing
- 历届高引议题：Agents、Evals、RAG、LLM Ops

**swyx 本人**：AI Engineer 公司 CEO，Latent Space podcast 主持人；同时**在 Cognition 帮做 coding agent eval 标准**（这一点至关重要 — 行业评测话语权集中在他这里）

**对 AI PM 应用**：#56 PM 成长包里 AIE WF 是「PM 一年必看一次的会议」推荐；#51 Eval 工具包里 swyx 在 Cognition 做的 coding agent eval 标准是「PM 自己定 eval 维度时的参照模板」

- 🔗 [ai.engineer](https://ai.engineer)
- **服务 Tool**：#46 / #51 ⭐ / #56

---

## 池子 9：顶级技术 podcast / 博客 / community 🟢 v2 深度

> 服务工具：#46 (Claude Code SOP) / #52 (成本算力) / #55 (老板对齐 / 战略) / #56 (成长包)
> v2 深度调研：2026-05-21 完成

### 9.1 Latent Space（swyx + Alessio Fanelli）⭐

**Tier-1 理由**：最接近 AI Engineering 行业「机关报」的 podcast / Substack，swyx 本人是「AI Engineer」这个词的发明者，并组织 AI Engineer World's Fair。听众覆盖 OpenAI / Anthropic / Gemini / Meta / Sierra 的工程师，常年位列 US 技术播客榜 Top 10

**2024-2025 必听 episode**：
- **"The State of Silicon and the GPU Poors" – Dylan Patel（SemiAnalysis）**，2024 — 行业首次系统化「GPU rich / GPU poor」对话
  - 🔗 [latent.space/p/semianalysis](https://www.latent.space/p/semianalysis)
- **"AI Engineering Goes Mainstream" – AIE WF 2025 Keynotes 复盘**，2025-06 — swyx 亲笔总结四大主题：Social-Data Network Effects / Prompts as the New Patents / Software is Content / Domain Experts > Tech Experts
  - 🔗 [latent.space/p/aiewf-2025-keynotes](https://www.latent.space/p/aiewf-2025-keynotes)
- **Cognition Walden Yan（背景 agent）/ Railway Jake Cooper（agent-native infra）/ Sean Grove (OpenAI)** — 2025 下半年密集出现的 agent 工程化主题
- Sean Grove 金句："the best coder is actually just going to be the best communicator"

**核心 takeaway**：AI Engineer 已经从 prompt 工程升级为「规格 + 评测 + agent 编排」三位一体；spec-to-PR 是 2025 的核心生产范式

**对 AI PM 工作的应用**：用 swyx 的 keynote 复盘文章直接喂给老板/团队，作为「AI PM 工作流为何要重构」的官方背书。spec-driven 直接对应专栏 P0-17 的 Claude Code SOP

- 🔗 [latent.space](https://latent.space)
- **服务 Tool**：#46 ⭐ / #56 ⭐ / 所有 AI Engineer 主题

### 9.2 SemiAnalysis（Dylan Patel）

**Tier-1 理由**：被 Sam Altman 公开转发的算力分析号，订阅含付费版（年费 $500+），Nvidia / AMD / TSMC / 国务院都在读。Dylan 是「GPU rich / GPU poor」概念发明者（出自 "Gemini Eats the World" 一文）

**2024-2025 必读长文**：
- **"Gemini Eats the World"**（2023 中，2024 持续发酵）— 提出 GPU 贫富差距框架，被 Sam Altman 公开 diss 后火出圈
- **Dwarkesh Podcast: "Dylan Patel — Deep dive on the 3 big bottlenecks to scaling AI compute"**（2026-03）— 系统讲 logic / memory / power 三大瓶颈
  - 🔗 [dwarkesh.com/p/dylan-patel](https://www.dwarkesh.com/p/dylan-patel)
- **GSA EMTech Webinar**（2025-11）— 半导体行业协会主题演讲
  - 🔗 [PDF](https://www.gsaglobal.org/events/wp-content/uploads/sites/10/2025/11/semianalysis_gsa-nov-2025-emtech-webinar.pdf)

**核心 takeaway**：「Buying a GPU in 2025 is like buying cocaine」— H100/A100 仍在灰市流通；hyperscaler CapEx 2026 将突破 5000 亿美元

**对 AI PM 工作的应用**：做 AI 产品成本测算（专栏 #52）时引用 SemiAnalysis 数字最有说服力；对老板讲「为什么我们调用成本下不来」直接搬「3 个 bottleneck」框架

- 🔗 [semianalysis.com](https://semianalysis.com)
- **服务 Tool**：#52 ⭐ (成本管控的算力侧)

### 9.3 Stratechery（Ben Thompson）

**Tier-1 理由**：硅谷战略博客绝对天花板，CEO 级读者，年费 $300。Bill Gates / Satya Nadella 公开承认是订阅者。Aggregation Theory 框架在 AI 时代仍是分析底座

**2024-2025 必读 AI 文章**：
- **"DeepSeek FAQ"**（2025-01-27）— Stratechery 史上 Top 5 阅读量，DeepSeek 引爆全球当天发布
  - 🔗 [stratechery.com/2025/deepseek-faq/](https://stratechery.com/2025/deepseek-faq/)
- **"Tech Philosophy and AI Opportunity"**（2025）— 按 tech philosophy 把 AI 公司分成 winners/losers
  - 🔗 [stratechery.com/2025/tech-philosophy-and-ai-opportunity/](https://stratechery.com/2025/tech-philosophy-and-ai-opportunity/)
- **"It's OpenAI's World, We're Just Living in It"**（2025）
  - 🔗 [stratechery.com/2025/its-openais-world-were-just-living-in-it/](https://stratechery.com/2025/its-openais-world-were-just-living-in-it/)
- **"Google, Nvidia, and OpenAI"**（2025）— 论 Google 反击战
  - 🔗 [stratechery.com/2025/google-nvidia-and-openai/](https://stratechery.com/2025/google-nvidia-and-openai/)
- **"AI's Uneven Arrival"** — o1/o3 指向 AGI，但企业落地比想象慢

**核心 takeaway**：DeepSeek 证明算法效率可以大幅降低训练成本，但推理需求会反向放大 Nvidia 受益（Jevons 悖论的 AI 版）

**对 AI PM 工作的应用**：写战略类专栏（#01 行业格局 / #25 趋势判断）的引用源；Ben Thompson 的框架可直接套用到「AI PM 如何在大厂/小厂选位置」

- 🔗 [stratechery.com](https://stratechery.com)
- **服务 Tool**：#55 ⭐ / #56

### 9.4 The Pragmatic Engineer（Gergely Orosz）

**Tier-1 理由**：Substack 技术类付费榜 #1（公开订阅数 100 万+），前 Uber 工程经理。每年的「AI Tooling Survey」是开发者圈共识来源

**2024-2025 必读文章**：
- **"AI Tooling for Software Engineers in 2026"**（2026-03）— 近千人调研：95% 开发者每周用 AI，75% 至少一半工作用 AI，Claude Code 8 个月内成 #1
  - 🔗 [newsletter.pragmaticengineer.com/p/ai-tooling-2026](https://newsletter.pragmaticengineer.com/p/ai-tooling-2026)
- **"AI Engineering in the real world"**（2025-03-25）— 定义 AI Engineering 边界
  - 🔗 [newsletter.pragmaticengineer.com/p/ai-engineering-in-the-real-world](https://newsletter.pragmaticengineer.com/p/ai-engineering-in-the-real-world)
- **"Software engineering with LLMs in 2025: temperature check"**
  - 🔗 [blog.pragmaticengineer.com/software-engineering-with-llms-in-2025/](https://blog.pragmaticengineer.com/software-engineering-with-llms-in-2025/)
- **"AI Engineering with Chip Huyen"**
  - 🔗 [newsletter.pragmaticengineer.com/p/ai-engineering-with-chip-huyen](https://newsletter.pragmaticengineer.com/p/ai-engineering-with-chip-huyen)
- **"The Pragmatic Engineer in 2025"** 年终复盘：vibe coding 主流化 / MCP 协议胜出 / Claude Code 成开发者最爱

**核心 takeaway**：2025 主线就是「coding agent 取代 autocomplete」；Cursor 仍在追赶 Copilot；70% 工程师同时用 2-4 个 AI 工具

**对 AI PM 工作的应用**：所有「Vibe Coding 工具横评」（专栏 #17）的数据底座；Gergely 的调研数字是说服「AI 工具替代度」最硬的引用源

- 🔗 [pragmaticengineer.com](https://pragmaticengineer.com)
- **服务 Tool**：#44 ⭐ / #55 / #56

### 9.5 20VC（Harry Stebbings）

**Tier-1 理由**：欧洲最具影响力 VC 播客，月下载量 800 万+，自己也是 20VC Fund GP（管理 4 亿美元）。直接采访 Reid Hoffman / Doug Leone / Brian Chesky / Bill Gurley

**2024-2025 必听 AI 创始人 episode**：
- **Aravind Srinivas (Perplexity)**（2024-06）— 论 foundation model 是否会商品化、推理是下一个性能拐点
  - 🔗 [open.spotify.com/episode/2TpLqRzfCsSULxuZSFrkEP](https://open.spotify.com/episode/2TpLqRzfCsSULxuZSFrkEP)
- **Reid Hoffman**（2024）— Inflection AI 卖给微软的内幕 + 从 Sam Altman、Brian Chesky 和 OpenAI 董事会得到的教训
- **Legora 和 Harvey 创始人**（2026-01 背靠背）— 法律 AI 双雄
- David Cahn (Sequoia)「AI's $600B question」相关 episode 也极有传播力

**核心 takeaway**：foundation model 商品化已成共识，应用层 + 工作流改造是 2025-2026 主战场；法律、医疗、销售三大赛道率先跑出独角兽

**对 AI PM 工作的应用**：写「AI PM 在垂类 SaaS 的机会」（专栏 #18）时直接引用 Harvey / Legora / Mercor 案例；20VC 风格的「直球质问」可学习用在 PM × 老板对齐（#55）

- 🔗 [20vc.com](https://20vc.com)
- **服务 Tool**：#55 / #56

### 9.6 Acquired（Ben Gilbert / David Rosenthal）

**Tier-1 理由**：全球商业史叙事类 Top 1 播客，单集 4-7 小时深度，订阅 100 万+，企业 CEO 必听。Bezos / Buffett / Jensen Huang 主动上节目

**2024-2025 必听 AI 公司深度**：
- **"NVIDIA CEO Jensen Huang"**（2023-10-16，2024-2025 持续被翻听）— Acquired 团队累计研究 Nvidia 500+ 小时
  - 🔗 [acquired.fm/episodes/jensen-huang](https://www.acquired.fm/episodes/jensen-huang)
- **"Nvidia: The Dawn of the AI Era"**（2023，三部曲第三集）— LinkedIn 万赞
- **"Google: The AI Company"**（2025-10-06）— Google 的第三部，深扒 Ilya Sutskever、Dario Amodei 从 Google 出走的故事
  - 🔗 [acquired.fm/episodes/google-the-ai-company](https://www.acquired.fm/episodes/google-the-ai-company)

**核心 takeaway**：Nvidia 的 CUDA 平台战略可追溯到公司创立，不是 AI 时代偶然成功；Google 当年的人才流失直接造就了 OpenAI 和 Anthropic 两家最危险的对手

**对 AI PM 工作的应用**：跟产品同事 / 老板讲「为什么 AI 时代的产品要有 10 年视角」时，Acquired 的叙事方式可直接借用；做 AI 公司竞争分析（#01）时是最硬核的史料源

- 🔗 [acquired.fm](https://acquired.fm)
- **服务 Tool**：#56 ⭐ (PM 成长包 - 标杆公司案例)

### 9.7 Sequoia Training Data podcast

**Tier-1 理由**：Sequoia Capital 官方播客，2024 年新开，但因 Sonya Huang / Pat Grady 亲自下场，订阅增长极快。所有嘉宾几乎都是 Sequoia 投资标的或目标公司创始人/研究员

**2025 高信号量 episode**：
- **Bob McGrew (OpenAI 前研究负责人)** — 提出 AGI 三脚凳框架，预测 2025 由 reasoning 定义，预训练边际收益递减
- **Bill Peebles (OpenAI Sora 2 团队)** — 论 space-time tokens 与视频物理一致性
- **Nicole Brichtova & Hansa Srinivasan** — Nano Banana 与角色一致性突破
- **Ryan Daniels & John Sarihan (Crosby)**（2025-09-02）— AI 法律事务所
- **Jan Oberhauser (n8n 创始人)**（2025-08-26）— 工作流工具如何转型 AI 自动化平台
- **John Noronha (Gamma)**（2025-08-19）— Gamma 如何变成「AI 模型试验室」

**核心 takeaway**：2025 是 reasoning 之年；agent 化的工作流工具（n8n / Gamma）是中间层最大赢家；垂直 AI 公司（Crosby 法律 / Abridge 医疗）已开始抢传统 SaaS 蛋糕

**对 AI PM 工作的应用**：写「AI PM 选赛道」（专栏 #26）的最佳一手案例库；n8n / Gamma 的 product evolution 路径可直接当案例讲产品转型

- 🔗 [sequoiacap.com/series/training-data/](https://sequoiacap.com/series/training-data/)
- **服务 Tool**：#56

### 9.8 Hard Fork（NYT，Casey Newton / Kevin Roose）

**Tier-1 理由**：纽约时报旗下，最主流的 AI 科技播客，听众覆盖普通商务人士、政策制定者，破圈能力最强。Kevin Roose 是「Sydney 事件」的引爆者

**2024-2025 必听 AI episode**：
- **"A.I. Goes to War"** — 论美国/以色列用 AI 做军事目标识别
- **Matthew Prince (Cloudflare CEO)** — 论如何对抗 AI scraper、内容创作者保护
- **Julie Bedard（研究员）** — 「A.I. brain fry」职场新症状
- **Trump 反「woke AI」** 政策讨论 — 第一修正案与 AI 内容审查

**核心 takeaway**：AI 已经从技术议题变成地缘政治、劳动法、内容版权多线议题；普通用户的「AI brain fry」（认知疲劳）会成为产品体验新设计约束

**对 AI PM 工作的应用**：写给老板/非技术决策者看的 AI 趋势文（专栏 #25），Hard Fork 的叙事节奏可学习；做 AI 产品的内容审核 / 合规设计（#14, #20）必听 Cloudflare 那期

- 🔗 [nytimes.com/podcasts](https://www.nytimes.com/podcasts)
- **服务 Tool**：#55 / #56

### 9.9 No Priors（Sarah Guo + Elad Gil）

**Tier-1 理由**：硅谷顶级独立投资人组合（Conviction / Color Genomics 创始人），创始人访谈密度最高。Spotify 全球科技播客 Top 20

**2024-2025 必听创始人 episode**：
- **"The Best of 2025 (So Far)"** 合集 — 一集听完整年高光：
  - Winston Weinberg (Harvey 法律 AI)
  - Fei-Fei Li (World Labs 空间智能)
  - Brendan Foody (Mercor 招聘 AI)
  - Dan Hendrycks (Center for AI Safety)
  - Noubar Afeyan (Flagship Pioneering / Moderna 创始 VC)
  - Brandon McKinzie & Eric Mitchell (OpenAI o3 团队)
  - Isa Fulford (OpenAI)
  - Arvind Jain (Glean)
  - Dr. Shiv Rao (Abridge 医疗 AI)
  - 🔗 [Spotify](https://open.spotify.com/episode/5ugCP5CKYIbIY5d9QPTKqg)
- **Jensen Huang 单集** — 公开 diss Dario Amodei「他们的意图明显与社会利益冲突」
- **Eric Zelikman (humans& 创始人，前 xAI)** — IQ → EQ 模型转向
- **Kyle Vogt (The Bot Company)** — Twitch / Cruise 创始人做家庭机器人
- **Zach Dell (Base Power)** — 10 亿美金融资细节

**核心 takeaway**：2025 创始人共识：垂直深度（法律、医疗、招聘）+ EQ/记忆/世界模型 > 通用智能竞赛；agent 安全和 alignment 是企业部署的真实卡点

**对 AI PM 工作的应用**：「AI PM 成长包」（#56）必听清单，每集都是顶级 AI 创业者亲口讲的产品决策逻辑；Harvey / Glean / Abridge 是 B2B AI PM 标杆案例

- 🔗 [noprior.org](https://noprior.org)
- **服务 Tool**：#56 ⭐ / #55

### 9.10 ai.engineer / AI Engineer World's Fair（与 9.1 互补 - 大会视角）

**Tier-1 理由**：swyx 创办，全球首个面向 AI Engineer 的大会，2025 年规模翻倍至 3000+。Andrej Karpathy、Sean Grove (OpenAI)、Mitesh (Nvidia) 等亲临。2026 年 6/29-7/2 在 SF

**2025 大会核心议题**（按热度排序）：
1. **Agent reliability**（最热）
2. **MCP**（Model Context Protocol）
3. **Infra**（agent-native infra）
4. **Evals**（被反复强调「AI 产品 #1 该做的事」）
5. **GraphRAG**（Nvidia Mitesh：「RAG 没死」）
6. **AI Product Management**（独立 track）
7. **SWE agents + Claude Code**（最爆满 track）
8. **AI in Fortune 500**
9. **AI Design / UX**
10. **Vibe Coding**
11. **Security**
12. **Voice**（ElevenLabs / Vapi 新品发布）

**Keynote 四大主题**（swyx 总结）：Social-Data Network Effects / Prompts as the New Patents / Software is Content / Domain Experts > Tech Experts

- 🔗 [ai.engineer/worldsfair/2026](https://www.ai.engineer/worldsfair/2026)
- 🔗 [2025 复盘](https://www.latent.space/p/aiewf-2025-keynotes)

**核心 takeaway**：AI PM 已经被 AIE WF 单独列为 track —— 行业承认「AI PM」是独立工种。Eval、agent 可靠性、MCP 是 2025-2026 三大工程主题

**对 AI PM 工作的应用**：专栏 12 个工具包的话题命中度极高，AIE WF 议题表可直接拿来做「AI PM 应该学什么」的权威清单（#56 成长包）；每一个 track 都对应专栏一篇文章

- **服务 Tool**：#46 / #51 / #56 ⭐ / 整体 community 锚

### 9.11 r/LocalLLaMA + r/MachineLearning（Reddit）

**Tier-1 理由**：
- **r/LocalLLaMA**：73.5 万订阅（2025），全球最活跃开源 LLM 社区，Meta Llama 团队、Qwen 团队、DeepSeek 团队都在潜水
- **r/MachineLearning**：290 万订阅，学术圈 + 工业圈共用，论文讨论密度最高

**r/LocalLLaMA 2024-2025 高 upvote 帖子规律**：
- **新开源模型发布日**（Llama 3 / Qwen 3 / DeepSeek V3 / GLM 4.5/4.7）当日必上万赞
- **"Codegraph" 工具帖** — 声称本地工具调用减少 94%
- **「我花 $20k 自建本地 coding agent」配置帖** — 硬件折腾流量密码
- **DeepSeek 102.9 亿美元融资** — 开源派的政治高潮
- **Benchmark 翻车帖** — 闭源 vs 开源对比

**社区主推模型排名**（2026-04，from r/LocalLLaMA 共识）：Qwen 3.5 / Gemma 4 / GLM-5/4.7 / MiniMax M2.5-M2.7

**r/MachineLearning 高赞规律**：
- 顶会（NeurIPS / ICML / ICLR）放榜讨论
- "[D]" 标签的方法论辩论
- 反炒作贴（"This paper is overhyped"）

**核心 takeaway**：开源模型已经在 coding、agent、tool use 上逼近闭源；本地部署需求被 Cursor/Claude Code 等订阅成本反向催熟

**对 AI PM 工作的应用**：做「AI 产品成本管控」（#52）时，r/LocalLLaMA 是「能否用开源替代闭源」的最快情报源；写「AI 产品能力边界」（#53）必看本地模型基线

- 🔗 [reddit.com/r/LocalLLaMA](https://reddit.com/r/LocalLLaMA) / [reddit.com/r/MachineLearning](https://reddit.com/r/MachineLearning)
- **服务 Tool**：#44 ⭐ / #52 / #53

### 9.12 HackerNews（YC）

**Tier-1 理由**：YCombinator 旗下，全球技术社区最高权重的「信号过滤器」。一篇文章上 HN 首页 = 当天 5-10 万独立访问。VC / CTO / 工程师必刷

**2024-2025 AI 板块爆款规律**：
- **Simon Willison 连续 3 年（2023/24/25）成 HN 最受欢迎博主** — 他写 AI/LLM，无利益绑定，「power user 视角」+「试遍所有工具」=「中立可信」公式
  - 🔗 参考：[refactoringenglish.com/blog/2025-hn-top-5/](https://refactoringenglish.com/blog/2025-hn-top-5/)
- **DeepSeek 周（2025-01）** — Ben Thompson 的 DeepSeek FAQ、DeepSeek 论文、How they did it 系列连续霸榜
- **Anthropic / OpenAI 新模型发布日** — 评论区比官方 blog 信息密度高
- **「Show HN」+ AI Demo** — 个人开发者爆款入口
- **反 AI 炒作文** — 学术圈对 AI 公司估值/能力的批判帖也高赞
- **AI 编程工具体验帖**（Claude Code / Cursor / Codex 评测）2025 全年长青

**爆款公式**（Every.to 研究）：早期 upvote 决定 momentum；AI 模型只能预测 60% 准确率（比随机高 20%）；标题包含具体数字、技术争议、或顶级 lab 名字最易上首页

**Simon Willison 模板**：从 Twitter/TikTok 等围墙花园里挖故事，搬到开放 web 让 HN 讨论 —— 「短引述 + 链接 + 一段评论」就是高赞结构

**核心 takeaway**：HN 的 AI 共识基本就是硅谷主流工程师共识；「中立 power user」是最稀缺的内容角色

**对 AI PM 工作的应用**：每天 15 分钟扫 HN front page + 搜 "AI" tag 就能跟上硅谷 AI 工程圈共识；写「AI PM 如何建立行业判断力」（#56）时 Simon Willison 是最佳模板

- 🔗 [news.ycombinator.com](https://news.ycombinator.com)
- **服务 Tool**：#44 / #56 ⭐

---

## 池子 10：国际 PM 社区 + 教育 🟢 v2 深度

> 服务工具：#46 (Claude Code SOP) / #51 (Eval 工具包) / #56 (PM 成长包)
> v2 深度调研：2026-05-21 完成

### 10.1 Mind the Product (MTP) — 全球最大 PM 社区

**Tier-1 理由**：2010 年伦敦起家，运营全球最大 PM 社区生态——155+ 城市 ProductTank 本地 meetup（伦敦、纽约、东京、新加坡、上海均有）+ 三层会议体系（meetup → MTP Engage → mtpcon 旗舰）。mtpcon London / SF 是全球公认两大顶级 PM 大会。Marty Cagan、Kathy Sierra、Teresa Torres 都是常驻讲者

**与同类差异 vs ProductSchool**：MTP = **社区驱动 + 思想领袖会议**（免费 meetup 为基础，付费大会赚利润，不卖证书）；ProductSchool = 培训 + 招聘漏斗（卖证书赚钱）。MTP 偏 senior PM 思考，ProductSchool 偏入门到中级训练

**2024-2025 关键内容**：
- **mtpcon London 2025**（2025-03-11，Barbican Centre，1500+ PM 现场 + 线上）
- **MTP Engage Hamburg & Manchester 2025**：定位「介于本地 ProductTank meetup 和旗舰 mtpcon 之间」的区域会议
- **mtpcon SF 2025**（2025-11-18，1 day）
- **Industry 2025 Conference**（Cleveland，三天 workshop 形式）
- **AI 主题课**：「Practical AI for Product Managers」by Nacho Bassino（dLocal VP of Product, AI & Product Ops）—— 给 PM 实战 AI 框架和 guardrails
- **ProductTank Barcelona「Build with AI」session**：核心论点 "Product thinking is the multiplier, AI is the accelerator"

**AI PM 应用**：上海/北京 PM 应关注 ProductTank 本地分会 + 订阅 mindtheproduct.com 文章；mtpcon 视频是公众号选题富矿（每场 keynote 都可拆解为 1-2 篇文章）

- 🔗 [mindtheproduct.com](https://www.mindtheproduct.com/)
- 🔗 [Industry 2025 recap](https://www.mindtheproduct.com/recap/industry-2025/)
- 🔗 [MTP Engage](https://www.mindtheproduct.com/mtpengage/)
- **服务 Tool**：#56 ⭐

### 10.2 Reforge — 高端 PM/Growth 进阶（Brian Balfour / Casey Winters / Sachin Rekhi）

**Tier-1 理由**：2016 年 Brian Balfour（HubSpot 前 Growth VP）创办，目标做「美国 PM/Growth 圈的高端 cohort 制教育」。导师阵容堪比硅谷名人堂：Casey Winters（前 Eventbrite CPO / Pinterest Growth）、Sachin Rekhi（LinkedIn 前 Sales Solutions Head of Product）、Fareed Mosavat、Kevin Kwok、Jiaona Zhang（Laurel CPO，前 Linktree）、Britt Jamison（OpenAI ChatGPT Enterprise Head of Product）。会员制 ~$2000/年，全库 40 门课

**与同类差异 vs Maven**：Reforge = **会员制 + 自有 IP 课程库**，强调长期系统化进阶；Maven = **讲师市场**，单课购买，更新更快、更垂直

**2024-2025 AI 课程清单**：
- **AI Product Leadership**（Jiaona Zhang + Britt Jamison）—— AI 时代如何带产品团队，调整策略/工具/团队结构/GTM
- **AI Foundations**（Sachin Rekhi 创办）—— AI 在 PM 关键 workflow 中的应用
- **AI Strategy**（Sachin Rekhi 创办 + Michael Sippey 主持）
- **AI Productivity / Mastering AI Productivity**（Brian Balfour 亲授，BUILD 框架）
- **AI Growth**（Brian Balfour + Casey Winters）
- **Advanced Product Strategy**（Sachin Rekhi + Michael Sippey）—— OKR + 战略路线图

**AI PM 应用**：Sachin Rekhi 的 AI Foundations + AI Strategy 是 senior PM 最值得刷的两门（PM 视角而非工程视角）；Brian Balfour 的 BUILD 框架可直接对标公众号「AI PM 工作流」选题

- 🔗 [reforge.com/courses](https://www.reforge.com/courses)
- 🔗 [AI Product Leadership](https://www.reforge.com/courses/ai-product-leadership)
- 🔗 [sachinrekhi.com/p/courses](https://www.sachinrekhi.com/p/courses)
- **服务 Tool**：#56 ⭐

### 10.3 Maven — AI PM Eval 标杆课所在地

**Tier-1 理由**：Maven 是 Wes Kao + Gagan Biyani 创办的「讲师市场型 cohort 平台」，2024-2025 成为 AI PM 内容增长最快的教育平台。最具标志性产品就是 Hamel Husain × Shreya Shankar 的 **AI Evals for Engineers and PMs**——Maven 史上 #1 营收课程，OpenAI / Anthropic / Google 等大厂内部员工大批组团报名

**与同类差异 vs Reforge**：Maven 单课付费、讲师 IP 强、可以承载非 PM 出身的 ML/AI 专家来教 PM（Reforge 都是 PM/Growth 出身导师）

**2024-2025 旗舰课程详情**：

**AI Evals for Engineers & PMs**（Hamel Husain + Shreya Shankar）
- 时长：4 周 cohort，每周 3-4 小时 + 10+ 直播 office hours
- 价格：$2,500（Lenny 折扣可至 $2,125）
- 内容：77 节课 + 4 个 coding assignment + 150+ 页 reader + 6 个月 Eval Assistant 工具 + Discord 终身访问
- 覆盖：error analysis、synthetic data 生成、LLM-as-judge、RAG debugging、CI/CD 集成
- 成果：已训练 2000+ PM/工程师，覆盖 500+ 公司；方法论同源 OpenAI / Anthropic 内训
- Hamel 背景：20+ 年 ML，Airbnb / GitHub，OpenAI Codex 早期研究合作
- Shreya 背景：UC Berkeley PhD，开源 AI data 系统

**其他相关 Maven 课**：
- AI Product Management Certification by **Product Faculty**（Rohan Varma + Henry Shi）
- Aakash Gupta 的 Growth/AI 系列

**AI PM 应用**：这门是公众号 #51（Eval 工具包）+ 第 12/13/19/21 篇正文最重要的引用源。中国 PM 自学 AI 评测，这门 + Aishwarya Reganti 的免费版课程是双绑配

- 🔗 [maven.com/parlance-labs/evals](https://maven.com/parlance-labs/evals)
- 🔗 [ai-evals-course.com](https://ai-evals-course.com/)
- 🔗 [maven.com/product-faculty/ai-product-management-certification](https://maven.com/product-faculty/ai-product-management-certification)
- **服务 Tool**：#51 ⭐⭐ (Eval 工具包核心参照)

### 10.4 Product School — 全球 PM 培训规模冠军

**Tier-1 理由**：2014 年 Carlos González de Villaumbrosia 在旧金山创办，已发展为全球规模最大的 PM 培训机构，9 个 certification 全线条覆盖入门到高阶。运营 ProductCon 大会（年会）+ 校友社区 + 招聘对接

**与同类差异 vs Reforge**：Product School = 入门到中级 + **证书 + 招聘漏斗**（讲师多来自 Google/Meta 现任产品 leader）；Reforge = senior 自我进阶，不卖证书。Product School 更工业化、Reforge 更精英化

**2024-2025 AI 课程**：
- **AIPC™（Artificial Intelligence Product Certification）**
  - 3 周 / 15 小时 / 6 个 live module
  - 价格：$2,999（单课）
  - 课程作者：Samantha Stevens（前 Google 产品 leader，现 CatalistAI CEO）
  - 覆盖：generative AI 基础、data-driven 决策、UX 创新、最终带 portfolio project
- **会员体系**：
  - Pro Membership：年 2 门 live + on-demand + 校友
  - Unlimited Membership：年 10 门 live + $10,000 价值 AI 工具访问 + ProductCon 门票
- **新增系列**（2024-2025 转向）：AI Prototyping、AI Evaluation、AI Agents 三门垂直证书

**AI PM 应用**：对刚转 AI PM 的同学，AIPC 是「速成 + 简历贴牌」选择；对资深 PM 性价比不如 Reforge / Maven。公众号选题角度：Product School 每年发布的「AI Product Manager Salary Report」「State of PM」可作为数据引用源

- 🔗 [productschool.com/certifications/ai-for-product-managers](https://productschool.com/certifications/ai-for-product-managers)
- 🔗 [Blog](https://productschool.com/blog/news/artificial-intelligence-certification)
- **服务 Tool**：#56

### 10.5 First Round Review — 硅谷 PM/创始人深度内容标杆

**Tier-1 理由**：First Round Capital（早期投了 Uber、Square、Notion、Roblox）的官方 review.firstround.com，被誉为「硅谷企业建造内容的金标准」。内容来自他们投的 CEO/CPO/founder 第一手访谈，几乎不外发，质量碾压一般博客。年度「Annual Roundup」是 PM/founder 必读

**与同类差异 vs a16z**：First Round = **战术深度 + 创始人内省**（每篇 5000-10000 字，单一访谈讲透）；a16z = trend & 论文式宏观。First Round 更适合 PM 拿来当方法论，a16z 适合做行业判断

**2024-2025 AI 主题代表文章**：
- **Replit's Path to Product-Market Fit**（Amjad Masad 讲 Replit 从大学副业到 $1B AI startup 的 journey，PMF 系列最新一篇）
- **Gong's Path to Product-Market Fit**（Eilon Reshef 与 Todd Jackson 对谈，讲怎么在早期押注 AI 做出 revenue intelligence 品类龙头）—— 同步出 First Round Podcast「A Masterclass in Founder Conviction」
- **2025 Annual Roundup（第 13 届）**：Gusto、Mercury、Meter 等 founder 最坦诚的 PMF 教训
- **专题入口**：review.firstround.com/articles/ai/（AI 全量索引）+ review.firstround.com/series/product-market-fit/

**AI PM 应用**：First Round 的 Eilon Reshef 访谈是公众号「AI PM 创业判断力」选题的最佳引用；Replit 案例可拆为「AI Coding 工具的 PM 视角」单篇。订阅其 newsletter，每月 1-2 篇够用

- 🔗 [review.firstround.com/articles/ai/](https://review.firstround.com/articles/ai/)
- 🔗 [Replit PMF](https://review.firstround.com/replits-path-to-product-market-fit/)
- 🔗 [Gong PMF](https://review.firstround.com/gongs-path-to-product-market-fit/)
- **服务 Tool**：#56 ⭐ / #50 (案例 PRD 创业 PM 视角)

### 10.6 Productboard / Linear / Notion 官方产品博客 — 三家 AI 实践公开样本

**Tier-1 理由**：三家都是「自己做 PM 工具 + 自己用 AI 重构 PM 工具」的标本企业，官方博客即一手实践，没有中间商赚价差

**Productboard Blog**（产品发现 + 路线图工具厂）
- 关键文章：「A Product Manager's Guide to Essential AI Terms and Systems」「How AI Is Reshaping Product Operations」「The Power of AI Agents in Product Operations Workflows」
- 视角：从 PM 操作层讲 AI agent 怎么进入 product ops
- 🔗 [productboard.com/blog](https://www.productboard.com/blog/)

**Linear Blog / linear.app/now / changelog**（开发者协作工具）
- 关键发布：**Linear for Agents**（2025-05-20 changelog）—— 把 Cursor / Devin / Codegen 等 AI agent 作为 first-class user，可分配 issue、@mention、加入 team/project
- **Product Intelligence**：自动 triage bug、推荐 assignee、识别重复 issue、推荐 label
- **Linear Agent 读 codebase 回答问题**
- 案例：**Ramp 内部 coding agent 已写 60%+ 合并 PR**，Linear 是 structured context layer
- 内容定位：Linear 写文章最克制最技术，每篇都是真实功能上线 + 真实客户案例，没有水文
- 🔗 [linear.app/now](https://linear.app/now)
- 🔗 [linear.app/ai](https://linear.app/ai)
- 🔗 [Linear for Agents](https://linear.app/changelog/2025-05-20-linear-for-agents)

**Notion Blog**（all-in-one workspace）
- **Notion 3.0**（2025-09-18 发布）：核心是 **AI Agents**——可自主运行 20 分钟、跨数百页操作、可建 doc/database、可搜跨工具
- Custom Agents（即将上线）：从 1 个个人 Agent 扩到一队 Custom Agents
- **MCP 集成**：Lovable、Perplexity、Mistral、HubSpot 成第一方 MCP 合作伙伴
- 内置模型：Claude Sonnet 4 + GPT-5 可切换
- **Enterprise Search + AI Connectors**：跨 Jira/Linear/GitHub/Slack 搜索 + Research Mode 生成报告
- 🔗 [Notion 3.0 announcement](https://www.notion.com/blog/introducing-notion-3-0)
- 🔗 [Release notes 2025-09-18](https://www.notion.com/releases/2025-09-18)

**AI PM 应用**：
- Productboard 适合做「AI 重构 product ops」选题素材
- Linear 适合做「PM 工具如何把 agent 当 first-class user」拆解（公众号 #46 Claude Code SOP 强引用）
- Notion 3.0 是 2025 年 AI PM 工具发布会级事件，应单独写 1 篇深度拆解
- 三家 changelog/blog 应订阅 RSS，每月扫描，是公众号「AI PM 工作流」最稳定的一手素材库

- **服务 Tool**：#46 / #49 (PRD 模板参照) / #56 ⭐

---

## Pool 总览（v1.1）

| Pool | 名称 | 条目数 | 核心服务 |
|---|---|---|---|
| 1 | KOL & 框架 | 14 | #46 #49 #55 #56 |
| 2 | 机构标准 & 报告 | 18 | 全工具 |
| 3 | Eval / SaaS | 16 | #51 #52 #54 |
| 4 | 真实业内案例 | 22 | #48 #54 #55 |
| **5** | **学术 AI Safety** | **9** | **#51 #53 #54 #56** |
| **6** | **风投视角** | **10** | **#52 #55 #56** |
| **7** | **行业咨询** | **8** | **#47 #55 #56** |
| **8** | **开源社区 + AI Engineer 工具** | **13** | **#44 #46 #51 #52 #53** |
| **9** | **技术 podcast / 博客 / community** | **12** | **#46 #52 #55 #56** |
| **10** | **国际 PM 社区** | **6** | **#46 #51 #56** |
| **合计** | | **~128** | |

---

## Tool → 主要参照 映射表（一目了然）

> v1.1 — 10 个池子全覆盖

| Task ID | 工具 | P1 KOL | P2 机构 | P3 Eval/SaaS | P4 案例 | P5 学术 | P6 风投 | P7 咨询 | P8 开源 | P9 Podcast | P10 PM社区 |
|---|---|---|---|---|---|---|---|---|---|---|---|
| **#44** | Vibe Coding 横评 | **Anna ⭐** | — | — | Cursor / Lovable | — | — | — | **Aider / Continue / Cline / Devin** | r/LocalLLaMA / HN | — |
| **#45** | Claude Code prompt 模板 | Cat Wu / Boris | — | — | Dennis Yang | — | — | — | — | Latent Space | — |
| **#46** | PM × Claude Code SOP | **Cat Wu / Krieger / Sachin / Lenny ⭐** | — | — | Dennis Yang | — | — | — | Aider / Cognition | **Latent Space ⭐** | Reforge |
| **#47** | MIT NANDA 失败分类 | — | **MIT NANDA / Gartner / Stanford HAI ⭐** | — | NYC MyCity / Manus | — | — | **McKinsey / BCG / Deloitte ⭐** | — | — | — |
| **#48** | 6 问 checklist | Hamel | **OpenAI Model Spec / Microsoft RAI v2 ⭐** / MIT NANDA | — | Air Canada / Klarna / McDonald's | — | — | McKinsey | — | — | — |
| **#49** | PRD 4 增 2 删 | Cat Wu / Krieger / Aparna / **Miqdad ⭐** | OpenAI MS / MS RAI / Anthropic ASL / Scrum DoD / Google Model Card | BMAD / Spec Kit | Chevy / Notion×Braintrust | — | — | — | — | — | Linear / Notion blog |
| **#50** | 案例 PRD 3 份 | — | — | — | Cursor / Lovable / Anthropic | — | — | — | — | — | — |
| **#51** | Eval 全套工具包 | **Hamel / Shreya ⭐** | Anthropic 统计 / EMNLP / MISQ | OpenAI Evals / Inspect / **Braintrust ⭐** / SWE-bench | Notion × Braintrust | NeurIPS / Apollo / MILA | — | — | LangChain / LlamaIndex / DSPy / HuggingFace | — | Maven |
| **#52** | 成本管控工具包 | — | **a16z / ICONIQ ⭐** | Helicone / Vellum / Traceloop / Finout | Token 5 事件 / Cursor / Anthropic caching | — | a16z / Bessemer | — | Together / Modal / Replicate | **SemiAnalysis ⭐** | — |
| **#53** | 能力边界工具包 | Teresa Torres | **METR ⭐** / OSWorld / Partnership on AI | — | Manus AI | Apollo / Redwood | — | — | LlamaIndex / Pinecone / Weaviate | — | — |
| **#54** | 上线运营工具包 | Hamel | Microsoft RAI / Anthropic Constitutional / Azure Content Safety | Datadog LLM / Arize / Helicone / PromptArmor / Lakera | **OpenAI sycophancy ⭐** / Gemini / Anthropic PM / DPD / Knight Capital | CAIS / Alignment Forum / Redwood | — | — | — | — | — |
| **#55** | PM 协作话术大全 | Cat Wu / Krieger / Aparna / Marty Cagan | OpenAI MS / Anthropic ASL | — | Air Canada / Klarna / McDonald's | — | Sequoia / a16z | **McKinsey / BCG / Bain ⭐** | — | Stratechery / Pragmatic Engineer | — |
| **#56** | PM 成长包 | **Sachin / Lenny / Marty Cagan ⭐** | Stanford HAI Index | SWE-bench | Lovable / Cursor / Anthropic / Humane Pin | Bengio / Stuart Russell / 5 经典论文 | **Sequoia / a16z / Bessemer / Conviction ⭐** | Accenture / PwC | HuggingFace 教育者 | **Acquired / Stratechery / Hard Fork / No Priors ⭐** | **Mind the Product / Reforge / First Round ⭐** |

---

## 已补完盲区（v1.1 - 2026-05-21）

✅ 蔡逸雯 2026-05-21 决议「全加上，做就做最好」——以下 6 类盲区已全部补齐：

| 类型 | 状态 | 加入位置 |
|---|---|---|
| 学术 AI Safety + 顶会 | ✅ 已补 9 条 | Pool 5 |
| 风投视角 | ✅ 已补 10 条 | Pool 6 |
| 行业咨询（Big 4 +） | ✅ 已补 8 条 | Pool 7 |
| 开源社区 + AI Engineer 工具 | ✅ 已补 13 条 | Pool 8 |
| 顶级技术 podcast / 博客 / community | ✅ 已补 12 条 | Pool 9 |
| 国际 PM 社区 + 教育 | ✅ 已补 6 条 | Pool 10 |

**v1.1 池子总数**：10 个 / **总条目**：~128 条全球 tier-1 源

## 持续维护原则

参照库不是"一次性建完"，需要持续更新：
- 每月新增：1-3 条（重大新框架 / 新事件 / 新报告）
- 每季 URL 全核查：避免链接失效
- 每篇文章发布前：对照 Tool 映射表，确认引用源更新

---

## 调研依据 4 级标准（v1.0）

接下来 12 个工具的「设计依据」章节按这 4 级填：

- **L1 强依据**：直接基于全球前沿框架（如 OpenAI Model Spec），有 URL，有具体引用
- **L2 中依据**：基于 KOL 公开观点（如 Hamel / Cat Wu），有出处但无标准化框架
- **L3 弱依据**：基于多个案例归纳（如 5 个 token 失控事件），有案例但无系统理论
- **L4 设计选择**：纯个人/团队判断（如「6 问而不是 4 问」），必须明确标注"待真 PM 验证"

每个工具至少 2 个 L1 + 3 个 L2，否则不能进入 ready-for-publish 状态。

---

## URL 核查进度

- 已核查：~30 条（GitHub repo 27-references v1.1 + 本次 Klarna / Fortune / TechCrunch / Bloomberg / OpenAI 等）
- 待核：~30 条（带 [URL: 待核] 标记的）
- 持续补：每月固定 1h 补核查（按出现频次优先级）

---

## 变更日志

- **2026-05-21 v1.0**：创建，覆盖 4 大池子约 60 条全球 tier-1 源 + 13 个 task 的映射表 + 4 级调研依据标准
- **2026-05-21 v1.1**：蔡逸雯决议「全加上」→ 补 6 个池子 68 条 → 总池子升到 **10 个 / 128 条**，新增覆盖：学术 AI Safety 顶会 / 风投视角 / Big 4 咨询 / 开源社区 + AI Engineer 工具 / 顶级技术 podcast / 国际 PM 社区。Tool → 参照映射表升级为 10 列全覆盖版
- **2026-05-21 v1.2**：蔡逸雯指出 v1.1 池子 5-10 是"敷衍占位"。决议 A+B 路径——A: 系统性补深度；B: 按需深度。**v1.2 Pool 5 完成 🟢 深度升级** — 9 条全部按"具体 paper + arXiv + 数据 + URL + PM 应用"标准重写，引入 Bengio 国际 AI 安全报告 / Apollo scheming paper / Redwood Ctrl-Z / DeepMind FSF v3 等具体最新成果
- **2026-05-21 v1.3**：蔡逸雯指令"多开 Agent 并行挖 / 不要老停下来问"。**并行启动 5 个调研 Agent（Pool 6-10 各 1 个）**，每个 Agent 独立做 WebSearch + URL 验证 + 深度内容生成。完成后 **Pool 6 (10 条 VC + Sequoia Act o1 / a16z 100 CIO / Bessemer Supernovas vs Shooting Stars / Conviction No Priors / GC Mistral 等) / Pool 7 (8 条咨询 + 8 家口径交叉验证 "5% 法则" 三角验证表) / Pool 8 (13 条开源 + GitHub stars 实地验证 DSPy 34.8k / Aider 45.6k / Cline 61.6k / Cognition Devin $26B 估值) / Pool 9 (12 条 podcast + 各家具体 episode + 嘉宾 + 日期) / Pool 10 (6 条 PM 社区 + Maven AI Evals $2500 价格 + Reforge AI Product Leadership 全清单)** 全部升 🟢 深度。整个参照库进入"全 10 池子真材料"状态
