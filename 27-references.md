# 参考资料索引 · 第一季 26 篇引用全清单

> 第一季《AI 时代 PM 工作流重构》· 配套资产 · 参考资料索引
> 作者：蔡逸雯（公众号「蔡逸雯」）
> **版本：v1.1**（2026-05-21 首发 · 已补 9 条最高频 URL）· 剩余 URL 持续补充中

---

## 关于本索引

本文档列出第一季全部外部引用——版权 hardening + 读者深挖参考。

**总览**：约 35 条 KOL 公开观点 + 15 份第三方报告 + 24 个业内案例 + 21 个开源 / 公开标准 + 多组模型公开数据。

### ⚠️ 当前版本状态（v1.1 首发）

**已完成**：
- ✅ 95 条引用的来源类型分类（5 大类）
- ✅ 每条引用在正文出现的篇号 + 行号区间
- ✅ 来源域名 / 平台 / 报告名称已标注
- ✅ **9 条最高频引用的官方 URL 已核查并补全**（出现 3-7 篇的高曝光引用——Air Canada / GPT-4o sycophancy / Cursor billing / Hamel Field Guide / OpenAI Model Spec / Microsoft RAI v2 / Cat Wu Lenny Podcast / Klarna 2024 + 2025 反转）
- ✅ 关键来源已交叉验证（官方 + 权威第三方双源）

**持续补充**：
- ⏳ 剩余 80+ 条引用的具体 URL 链接（v1.2 版预计 1 个月内补全核心 50 条 / v2.0 版预计 3 个月内补全 95 条）
- ⏳ URL 失效的引用 → 在表格末尾标注"原 URL 失效，建议读者按域名 + 关键词搜索"

**承诺**：
- 付费读者会自动收到 v1.1 / v2.0 更新版本
- 每条引用都可按"出现位置 + 来源域名"自行 Google 5 秒内找到

### 给读者的承诺

- 所有引用均来自公开来源（公开演讲 / 博客 / podcast / 学术论文 / 财报 / 监管文件 / 新闻报道）
- 任何一条引用都可在本索引中查到出现位置（篇号 + 行号区间），方便读者深挖
- 引用属合理使用（fair use）—— 评论性引用 + 标注作者 + 不替代原始来源

---

## 类 1：KOL 公开观点（约 35 条）

### 1.1 Hamel Husain（独立 AI 评估顾问，Maven 课程联合讲师）

**引用 A**："Writing good evals is becoming the defining skill for AI PMs."（写好 evals 正在成为 AI PM 的定义性技能）
- 出现位置：第 01 篇 L236-244 / 第 12 篇 L16
- 建议来源：Lenny Newsletter 2025 / Maven 课程 "AI Evals For Engineers & PMs"
- [URL: 待补]

**引用 B**："EDD was always front and center pre-generative AI. Ex: nobody cares about your fraud/churn/forecasting model if it's not accurate."
- 出现位置：第 12 篇 L290 / 第 13 篇 L216-224 / 第 13 篇 L285
- 建议来源：hamel.dev 个人博客 / Twitter @HamelHusain（2024-10）
- [URL: 待补]

**引用 C**："Field Guide to Rapidly Improving AI Products" SOP——每改一次至少手看 20-50 条 trace / 写自定义数据查看器 / 错误聚类→定义失败模式 / 每个失败模式写一条 eval / 把 eval 集做成 CI 卡口 / "until you stop finding new failure modes"
- 出现位置：第 12 篇 L130 / 第 13 篇 L173-176 / 第 18 篇 L140-148 / 第 21 篇 L99-112 / 第 21 篇 L268
- 来源：https://hamel.dev/blog/posts/field-guide/（Hamel 官方博客）

**引用 D**：三层 Eval 框架 L1（Unit Tests）/ L2（Human & Model Eval）/ L3（A/B Testing）；60-80% 开发时间花在 error analysis 和 evaluation 上；二元评分而非 5 分制
- 出现位置：第 12 篇 L108-141
- 建议来源：Hamel × Shreya Shankar Maven 课程材料
- [URL: 待补]

### 1.2 Cat Wu（Anthropic Claude Code Head of Product）

**引用 A**："Prototypes over PRDs"
- 出现位置：第 01 篇 L122-128 / 第 11 篇 L160 / 第 25 篇 L194
- 来源：https://www.lennysnewsletter.com/p/how-anthropics-product-team-moves（Lenny's Podcast Cat Wu 2026-04-23 集）

**引用 B**：Anthropic 产品团队"为什么比所有人都快"——PM/Designer/Eng 都用 Claude Code 直接产出 working prototype 评审，而不是 Figma + 文档
- 出现位置：第 17 篇 L242-244
- 来源：https://www.lennysnewsletter.com/p/how-anthropics-product-team-moves（Lenny's Podcast Cat Wu 2026-04-23 集）

**引用 C**：Product Note 三要点 "Prototypes over PRDs" / "Spec-first" / "Daily user sentiment loop"
- 出现位置：第 24 篇 L192-199 / 第 25 篇 L190-204
- 来源：https://www.lennysnewsletter.com/p/how-anthropics-product-team-moves（Lenny's Podcast Cat Wu 2026-04-23 集）

### 1.3 Mike Krieger（Anthropic CPO，前 Instagram 联合创始人）

**引用**：PM 不再写 10 页 PRD，改写 3-4 段的 Product Note（用户意图 + 期望结果 + 具体指标），配 `product_area_context.md` + `code_context.md` 两个上下文文件；orchestrator 合成 Functional Spec，PM 转身做 "Editor-in-Chief" 审 PR
- 出现位置：第 01 篇 L118-128 / 第 11 篇 L150-158
- 建议来源：Lenny's Podcast Mike Krieger 专访集
- [URL: 待补]

### 1.4 Boris Cherny（Anthropic Claude Code 负责人）

**引用**：自 2025-11 起 100% 代码由 Claude Code 写，自己已不手敲；Anthropic 内部工作流先做 prototype 再 dogfood
- 出现位置：第 01 篇 L134 / 第 17 篇 L238-241
- 建议来源：Lenny's Podcast Boris Cherny 专访
- [URL: 待补]

### 1.5 Sachin Rekhi（前 LinkedIn / Reforge 讲师）

**引用**：在面向 PM 的大型 webinar 上展示十多个自建 skills——客户访谈合成 / NPS 自治 / 无 SQL 的 EDA / 产品战略 critique / release notes 自动化；同期产出 "AI Prototyping Mastery Ladder"（Apprentice / Journeyman / Master 三档）
- 出现位置：第 01 篇 L134-138 / 第 17 篇 L233-237
- 建议来源：Sachin Rekhi 公开 webinar 录像 + Reforge 课程页 + sachinrekhi.com
- [URL: 待补]

### 1.6 Aparna Chennapragada（Microsoft CPO）

**引用**："Prompt sets are the new PRDs." + "prompt set 是活的产物，半是 spec 半是训练数据"；传统 PRD"为程序员而写、提前锁死需求再交付"，AI 产品本质非确定性
- 出现位置：第 01 篇 L202-208 / 第 11 篇 L194-199
- 建议来源：Lenny's Podcast Aparna Chennapragada 专访
- [URL: 待补]

### 1.7 Marty Cagan（SVPG）

**引用**："Product discovery 是判断（judgement），AI 可以自动化交付，但发现未满足需求、验证价值这件事不能。"
- 出现位置：第 01 篇 L176-180 / 第 03 篇 L170-174
- 建议来源：svpg.com 2025 年文章
- [URL: 待补]

### 1.8 Teresa Torres（Product Talk）

**引用**："客户访谈本身要变。在 AI 产品里，outcome 不是确定性的，访谈不能再问'你想要什么'，而要 log traces / 让人审 / 标错误类 / 写 evals / A/B 测修复"
- 出现位置：第 03 篇 L175-180
- 建议来源：Teresa Torres 2025 webinar / Product Talk 博客
- [URL: 待补]

### 1.9 Kevin Weil（OpenAI CPO）

**引用**：季度 roadmap 和年度策略已经反映不了真实出货节奏，roadmap 重新定义为 "rolling bets"
- 出现位置：第 03 篇 L181-184
- 建议来源：Lenny Newsletter 引用集 / Kevin Weil 公开访谈
- [URL: 待补]

### 1.10 Anton Osika（Lovable 创始人）

**引用**："我们的 PM 数量是 0，工程师都在做 PM 的事"
- 出现位置：第 25 篇 L76
- 建议来源：Lovable 创始人公开访谈 / Twitter @antonosika
- [URL: 待补]

### 1.11 Satya Nadella（Microsoft CEO）

**引用**："as much as 30% of our code is now written by AI"
- 出现位置：第 25 篇 L80 / L246
- 建议来源：Microsoft 2025-04 财报电话会议 transcript
- [URL: 待补]

### 1.12 Sundar Pichai（Google CEO）

**引用 A**："We were able to lower Gemini serving unit costs by 78% over 2025 through model optimisations, efficiency and utilisation improvements."
- 出现位置：第 08 篇 L207-211
- 建议来源：Google Alphabet Q4 2025 财报电话会议
- [URL: 待补]

**引用 B**：Gemini 图像生成 over-tune 事件后公开发文称 "unacceptable"
- 出现位置：第 18 篇 L196-199 / 第 21 篇 L207
- 建议来源：Google 官方博客 2024-02 声明
- [URL: 待补]

### 1.13 梁文锋（DeepSeek 创始人）

**引用**："我们不是有意成为一条鲶鱼，只是不小心成了一条鲶鱼……我们的原则是不贴钱，也不赚取暴利，这个价格也是在成本之上稍微有点利润。"
- 出现位置：第 08 篇 L213-217
- 建议来源：暗涌 Waves 专访
- [URL: 待补]

### 1.14 Sebastian Siemiatkowski（Klarna CEO）

**引用 A**：2024 宣布 AI 替代相当于 700 个客服等效工作量
**引用 B**：2025-05 公开承认"AI 缺乏共情"，重新开放招聘转 hybrid 模型
- 出现位置：第 04 篇 L263 / 第 22 篇 L221-223 / 第 25 篇 L160-164
- 来源 A（2024-02 公告）：https://www.klarna.com/international/press/klarna-ai-assistant-handles-two-thirds-of-customer-service-chats-in-its-first-month/
- 来源 B（2025-05 反转 Bloomberg 报道）：https://www.bloomberg.com/news/articles/2025-05-08/klarna-turns-from-ai-to-real-person-customer-service

### 1.15 Dario Amodei（Anthropic CEO）

**引用**：Research 团队占比约 1/3 以上
- 出现位置：第 24 篇 L52-60 / 第 25 篇 L34-36
- 建议来源：Anthropic CEO 公开访谈（Lex Fridman 等）
- [URL: 待补]

### 1.16 Lenny Rachitsky（Lenny's Newsletter）

**引用**："Everyone should be using Claude Code more" / "忘掉它叫 Claude Code，把它当作 Claude Local / Claude Agent" / 收集 50 个非技术用户的 Claude Code 用例
- 出现位置：第 17 篇 L228-232 / L355
- 建议来源：Lenny Newsletter 2026-02 文章
- [URL: 待补]

### 1.17 Dennis Yang（Chime PM）

**引用**：markdown 写 PRD → 终端打开 `claude` → 20 分钟跑出可点击原型 → Slack 录屏分享
- 出现位置：第 17 篇 L222-224
- 建议来源：Dennis Yang 公开分享 / Lenny Newsletter 引用
- [URL: 待补]

### 1.18 Anna Arteeva（Vibe coding 评测者）

**引用**："Lovable 赢非技术 PM，Bolt 赢速度，v0 赢 UI，Replit 赢全栈，Cursor / Claude Code 赢工程深度"
- 出现位置：第 17 篇 L202-206
- 建议来源：Anna Arteeva Medium / 公开 review 文章
- [URL: 待补]

### 1.19 Miqdad Jaffer（OpenAI Product Lead）

**引用**：productcompass.pm 公开的 "AI PRD Template"——结构：能力边界 / 输入输出 schema / 评估集 / 失败模式 / 成本上限
- 出现位置：第 02 篇 L36
- 建议来源：productcompass.pm
- [URL: 待补]

### 1.20 David Haberlah（Medium 数据分析）

**引用**：拆解 638 位 PM 实际产出——AI 相关内容从 2023 年初 4% 涨到 2026 Q1 67%；mocking & prototyping 占比从 60-70% 跌到 30-40%
- 出现位置：第 01 篇 L46-52 / 第 02 篇 L96
- 建议来源：David Haberlah Medium 文章
- [URL: 待补]

### 1.21 Shreya Shankar（Hamel 联合讲师）

**引用**：与 Hamel 联合推出 Maven 课程，教过 2000+ PM 和工程师
- 出现位置：第 01 篇 L236-244
- 建议来源：Maven 课程 "AI Evals For Engineers & PMs"
- [URL: 待补]

### 1.22 OpenAI 自身 GPT-4o sycophancy postmortem 声明

**引用**："Sycophancy 没有作为 blocking 项进入发版评估"；几位测试员"感觉怪"但没机制让这条意见停下发版；修复后写入"behavior issues 必须能 block 发布"
- 出现位置：第 01 篇 L302 / 第 14 篇 L242-248 / 第 18 篇 L188-194 / 第 21 篇 L195-201 / 第 23 篇 L88
- 来源 A（初次公告 2025-04-29）：https://openai.com/index/sycophancy-in-gpt-4o/
- 来源 B（详细 postmortem 2025-05-01）：https://openai.com/index/expanding-on-sycophancy/

---

## 类 2：第三方报告 / 调研数据（约 15 份）

### 2.1 MIT NANDA《State of AI in Business 2025》

- 引用数据：95% 企业 GenAI 项目零可衡量回报；外采+共建模式成功率 67%，纯内部自建仅 1/3
- 出现位置：第 04 篇 L17 / L42-44 / L219-223 / 第 06 篇 L86-87 / L197
- 建议来源：MIT Sloan / NANDA Initiative（mitsloan.mit.edu / nanda.media.mit.edu）2025-08
- [URL: 待补]

### 2.2 a16z 2025 企业 LLM 100 CIO 调研

- 引用数据：企业 LLM 年均花费 $4.5M → $7M；37% 企业同时跑 5+ 模型；74% CEO 把 AI 列为最高优先级；预算预期一年再涨 ~75%
- 出现位置：第 04 篇 L229-232 / 第 14 篇 L213 / 第 20 篇 L89-91 / 第 22 篇 L131-134 / 第 24 篇 L63-73
- 建议来源：a16z.com 2025 Enterprise AI Survey
- [URL: 待补]

### 2.3 Gartner 2025 GenAI Hype Cycle

- 引用数据：GenAI 进入 Trough of Disillusionment；企业 2024 GenAI 投入 $190 万；<30% CEO 对回报满意
- 出现位置：第 04 篇 L224-228
- 建议来源：Gartner Research 官方报告
- [URL: 待补]

### 2.4 ICONIQ 2025 AI 产品调研

- 引用数据：AI 产品平均毛利 2024=41% / 2025=45% / 2026=52%
- 出现位置：第 03 篇 L65-66 / 第 09 篇 L122 / L242-243 / 第 15 篇 L207-209
- 建议来源：iconiqcapital.com 2025 报告
- [URL: 待补]

### 2.5 Stanford RegLab + HAI 法律 AI 幻觉研究（2024-2025）

- 引用数据：Lexis+ AI 17% / Westlaw AI-Assisted Research 33% / GPT-4 43% 幻觉率
- 出现位置：第 04 篇 L67-68
- 建议来源：Stanford RegLab 论文 / hai.stanford.edu
- [URL: 待补]

### 2.6 The Information / Reuters 关于 Anthropic / OpenAI 财务

- 引用数据：Anthropic 推理成本一度超过当期收入；OpenAI 2025 收入 ~$13B
- 出现位置：第 09 篇 L233-243 / 第 15 篇 L196-205
- 建议来源：theinformation.com / reuters.com 2025 报道
- [URL: 待补]

### 2.7 Springer Nature 用户研究综述

- 引用数据："pre-experience expectations 与 post-experience evaluation 的系统性落差"
- 出现位置：第 01 篇 L170 / 第 03 篇 L34 / L119
- 建议来源：Springer Nature 期刊（具体 paper 待查）
- [URL: 待补]

### 2.8 TechXplore sycophantic 研究（2025-07）

- 引用数据：ChatBot 错了也仍然自信
- 出现位置：第 03 篇 L126
- 建议来源：TechXplore 2025-07 文章
- [URL: 待补]

### 2.9 EMNLP 2024 RLHF 对齐税论文

- 引用数据：OpenLLaMA-3B 偏好对齐奖励从 0.16 提到 0.35 时——SQuAD F1 掉 16 分、DROP F1 掉 17 分、WMT BLEU 掉 5.7
- 出现位置：第 02 篇 L128 / 第 07 篇 L168
- 建议来源：EMNLP 2024 论文集（aclanthology.org）
- [URL: 待补]

### 2.10 MIT MedRxiv 2025 医疗 AI 幻觉论文

- 引用数据：LLM 幻觉因为"用专业术语 + 看似 coherent"反而最难识别
- 出现位置：第 04 篇 L94
- 建议来源：medrxiv.org 2025 论文
- [URL: 待补]

### 2.11 MISQ Lebovitz / Levina / Lifshitz-Assaf 论文 *Is AI Ground Truth Really True?*

- 引用数据：专家 know-what 标注的不确定性导致"benchmark 高分 / 实战崩盘"
- 出现位置：第 04 篇 L96
- 建议来源：MIS Quarterly（misq.org）
- [URL: 待补]

### 2.12 METR "horizon length" 系列研究

- 引用数据：前沿模型能稳定完成的任务时长每 7 个月翻倍
- 出现位置：第 05 篇 L58 / L205
- 建议来源：metr.org 官方报告
- [URL: 待补]

### 2.13 Partnership on AI《Prioritizing Real-Time Failure Detection in AI Agents》（2025）

- 引用数据：把"实时失败检测"列为长 Agent 部署的核心命题
- 出现位置：第 05 篇 L167-171
- 建议来源：partnershiponai.org
- [URL: 待补]

### 2.14 Retool 关于 vibe-coded app 调研

- 引用数据：vibe-coded app 接真数据库时 SQL 注入是"等待发生的数据泄露"
- 出现位置：第 17 篇 L260
- 建议来源：Retool 官方 State of AI 报告
- [URL: 待补]

### 2.15 杰文斯悖论数据

- 引用数据：Token 价格 99.7% 跌，企业 AI 总支出反而涨到 $37B
- 出现位置：第 09 篇 L245-247 / 第 15 篇 L211
- 建议来源：综合 Bloomberg / a16z / ICONIQ 口径
- [URL: 待补]

---

## 类 3：业内案例（约 24 个）

### 3.1 Air Canada Moffatt 案（2024-02 判决）

- 关键事实：bot 编造"丧亲票 90 天内追溯申请退款"政策，BC Civil Resolution Tribunal 判赔加币 650.88（约 480 美元），裁定"chatbot 不是独立法律实体"
- 出现位置：第 04 篇 L132 / 第 11 篇 L252-262 / 第 14 篇 L218-223 / 第 19 篇 L222-228 / L294 / 第 22 篇 L226-230 / 第 24 篇 L83-87
- 来源：https://www.canlii.org/en/bc/bccrt/doc/2024/2024bccrt149/2024bccrt149.html（CanLII 官方判决全文，2024 BCCRT 149）

### 3.2 Klarna AI 替代 700 客服（2024 → 2025 反转）

- 出现位置：第 04 篇 L263 / 第 22 篇 L221-223 / 第 25 篇 L160-164
- 来源 A（2024-02 Klarna 官方公告）：https://www.klarna.com/international/press/klarna-ai-assistant-handles-two-thirds-of-customer-service-chats-in-its-first-month/
- 来源 B（OpenAI 客户案例页）：https://openai.com/index/klarna/
- 来源 C（2025-05 反转 Bloomberg 报道）：https://www.bloomberg.com/news/articles/2025-05-08/klarna-turns-from-ai-to-real-person-customer-service
- 来源 D（2025-05 Fortune 解读）：https://fortune.com/2025/05/09/klarna-ai-humans-return-on-investment/

### 3.3 DPD 聊天机器人 Ashley Beauchamp（2024-01）

- 关键事实：post-update 没回归 eval，调教出"DPD 是世界最差快递"的诗，单条推文 X 内数百万曝光
- 出现位置：第 12 篇 L219-223 / 第 19 篇 L206-212 / 第 20 篇 L196-200
- 建议来源：BBC / The Guardian 2024-01 报道 + Ashley Beauchamp X 推文链接
- [URL: 待补]

### 3.4 NYC MyCity 政府 chatbot（2024-03）

- 出现位置：第 04 篇 L173-184 / 第 11 篇 L264-272 / 第 12 篇 L224-226 / 第 19 篇 L214-220
- 建议来源：The Markup 调查报道（themarkup.org）
- [URL: 待补]

### 3.5 Chevy 经销商 chatbot 被 prompt injection 卖 $1 Tahoe（2023-11）

- 出现位置：第 11 篇 L275-284
- 建议来源：原始 X 推文 + Business Insider / The Verge 2023-11 报道
- [URL: 待补]

### 3.6 McDonald's × IBM 得来速 AI 点单（2021-2024.07）

- 出现位置：第 04 篇 L189-196 / 第 12 篇 L63 / 第 22 篇 L105-107 / L233-238
- 建议来源：CNBC / Bloomberg / Restaurant Business Online 2024-06 报道
- [URL: 待补]

### 3.7 Knight Capital $4.4 亿亏损（2012）

- 关键事实：8 台服务器漏更新 1 台，45 分钟亏 $4.4 亿
- 出现位置：第 18 篇 L287
- 建议来源：SEC 调查报告 / Wikipedia "Knight Capital Group"
- [URL: 待补]

### 3.8 OpenAI GPT-4o sycophancy（2025-04-25 → 2025-04-29 全量回滚）

- 出现位置：第 01 篇 L302-304 / 第 14 篇 L228-248 / 第 18 篇 L188-194 / 第 21 篇 L194-201 / 第 23 篇 L88 / 第 24 篇 L100-105
- 来源 A（OpenAI 初次公告 2025-04-29）：https://openai.com/index/sycophancy-in-gpt-4o/
- 来源 B（OpenAI 详细 postmortem 2025-05-01）：https://openai.com/index/expanding-on-sycophancy/
- 来源 C（TechCrunch 报道）：https://techcrunch.com/2025/04/29/openai-explains-why-chatgpt-became-too-sycophantic/

### 3.9 Cursor 2025-06 billing 暴雷

- 出现位置：第 01 篇 L268 / 第 02 篇 L163 / 第 08 篇 L246 / 第 09 篇 L218-224 / 第 15 篇 L156-165
- 来源 A（Cursor 官方道歉 blog 2025-07-04）：https://cursor.com/blog/june-2025-pricing
- 来源 B（TechCrunch 报道 2025-07-07）：https://techcrunch.com/2025/07/07/cursor-apologizes-for-unclear-pricing-changes-that-upset-users/

### 3.10 DoorDash chatbot 模拟器

- 出现位置：第 18 篇 L113-118
- 建议来源：DoorDash Engineering Blog
- [URL: 待补]

### 3.11 Anthropic 2025 Postmortem（性能优化误伤输出质量）

- 出现位置：第 20 篇 L162-167
- 建议来源：Anthropic Engineering Blog 2025 postmortem
- [URL: 待补]

### 3.12 Cursor "engine vs car" 论 + Claude 3.7 post-train

- 出现位置：第 02 篇 L132-134 / L182 / 第 07 篇 L172-174 / L208
- 建议来源：Cursor 团队公开博客 / 工程访谈
- [URL: 待补]

### 3.13 Humane AI Pin 翻车（2025-02 卖给 HP）

- 关键事实：融资 2.3 亿美元，2025-02 卖给 HP 仅 1.16 亿
- 出现位置：第 01 篇 L174
- 建议来源：Bloomberg / The Verge 2025-02 报道
- [URL: 待补]

### 3.14 ChatGPT「胡言乱语事件」（2024-02-20）

- 关键事实：线上约 5 小时回滚
- 出现位置：第 18 篇 L203-209
- 建议来源：OpenAI status page 报告
- [URL: 待补]

### 3.15 Gemini 图像生成 over-tune（2024-02）

- 出现位置：第 18 篇 L196-199 / 第 21 篇 L203-209
- 建议来源：Google 官方声明 + The Verge / Wired 报道
- [URL: 待补]

### 3.16 Google AI Overviews 胶水披萨（2024-05）

- 出现位置：第 20 篇 L190-195
- 建议来源：The Verge / BBC 2024-05 报道
- [URL: 待补]

### 3.17 Manus AI（蝴蝶效应公司）

- 关键事实：宣称 GAIA SOTA，实测 reliability / 上下文窗口 / 付费墙 / CAPTCHA 全卡死
- 出现位置：第 05 篇 L222-234
- 建议来源：多家技术媒体 2025 初实测报道
- [URL: 待补]

### 3.18 Khan Academy Khanmigo（教育 AI）

- 出现位置：第 06 篇要点列表（正文未深入展开）
- 建议来源：Khan Academy 公开声明
- [URL: 待补]
- ⚠️ 注：实际正文展开较少，作者可考虑补充或从索引删除

### 3.19 Nabla 医疗 AI scribe

- 出现位置：第 06 篇要点列表（正文未深入展开）
- 建议来源：Nabla 官方网站 / 公开报道
- [URL: 待补]
- ⚠️ 注：实际正文展开较少，作者可考虑补充或从索引删除

### 3.20 Token 账单 5 个真实失控事件

- 事件 1：Claude Code 递归循环 5 小时烧 16.7 亿 token
- 事件 2：subagent 进入 809 步无限循环，3.5 小时烧 $350
- 事件 3：retry loop 一夜烧 $72,000 OpenAI credit
- 事件 4：某软件公司单计费周期 $150,000 影子 AI 危机
- 事件 5：Cursor June 2025 billing 暴雷（同 3.9）
- 出现位置：第 09 篇 L200-224 / 第 15 篇 L133-137
- 建议来源：Hacker News / X 推文 / Reddit 多源汇总
- [URL: 待补]

### 3.21 Cursor 案例（人均 ARR）

- 关键事实：2025-Q3 工程团队约 100 人，撑起 $1B 量级 ARR
- 出现位置：第 01 篇 L32 / 第 25 篇 L57-60 / L260-262
- 建议来源：Cursor 官方口径 / Forbes / Bloomberg 报道
- [URL: 待补]

### 3.22 Lovable 案例（人均 ARR）

- 关键事实：2025-Q3 快照——18 人 ~$17M ARR
- 出现位置：第 01 篇 L30 / 第 16 篇 L109-110 / 第 25 篇 L72-77 / L252-254
- 建议来源：Lovable 创始人公开声明
- [URL: 待补]

### 3.23 Anthropic 销售配比

- 关键事实：~2000 人公司销售 quota carrier 只有数十名
- 出现位置：第 01 篇 L34
- 建议来源：Anthropic 公开口径
- [URL: 待补]

### 3.24 Notion × Braintrust 案例

- 关键事实：双轨 eval（regression + frontier），特定 workflow 提速近 10 倍
- 出现位置：第 12 篇 L100-104 / 第 18 篇 L103-110 / 第 25 篇 L51-53 / L248-250
- 建议来源：Braintrust 客户案例博客
- [URL: 待补]

### 3.25 thoughtbot 工程师 weekend MVP

- 出现位置：第 16 篇 L112-114
- 建议来源：thoughtbot 博客
- [URL: 待补]

### 3.26 Anna Arteeva AI Agents Benchmark vibeCrm 案例

- 出现位置：第 16 篇 L115-117 / L119-127
- 建议来源：Anna Arteeva Medium 评测
- [URL: 待补]

### 3.27 Anthropic prompt caching 3 个案例

- DEV.to 作者：RCA 任务砍 90% 成本
- Du'An Lightfoot：月账单 $720 → $72
- ProjectDiscovery：缓存命中率 7% → 74%
- 出现位置：第 08 篇 L99-114 / 第 09 篇 L186
- 建议来源：DEV.to / Du'An Lightfoot 公开博客 / ProjectDiscovery 官方
- [URL: 待补]

---

## 类 4：开源框架 / 公开标准（约 21 个）

### 4.1 BMAD-METHOD

- 全称：Breakthrough Method of Agile AI-Driven Development
- 出现位置：第 01 篇 L100-104 / 第 11 篇 L174-182 / 第 13 篇 L231-241
- 建议来源：github.com/bmad-code-org/BMAD-METHOD
- [URL: 待补]

### 4.2 GitHub Spec Kit（Spec-Driven Development）

- 维护方：GitHub
- 引用版本：2025-09 开源
- 流程：`/specify` → `/plan` → `/tasks` → `/analyze`
- 出现位置：第 01 篇 L106-116 / 第 11 篇 L164-172 / 第 13 篇 L243-255
- 建议来源：github.com/github/spec-kit
- [URL: 待补]

### 4.3 OpenAI Model Spec

- 维护方：OpenAI
- 三层结构：Objectives / Rules / Defaults
- 引用版本：2025-12-18（最新版，含 U18 Principles）
- 出现位置：第 11 篇 L139-147 / 第 14 篇 L172-180 / 第 24 篇 L167-175
- 来源 A（最新版）：https://model-spec.openai.com/
- 来源 B（2025-12-18 永久链接）：https://model-spec.openai.com/2025-12-18.html

### 4.4 Anthropic ASL（AI Safety Levels）/ Responsible Scaling Policy

- 维护方：Anthropic
- 能力四级 ASL-1 → ASL-4
- 出现位置：第 14 篇 L165-170 / 第 24 篇 L176-184
- 建议来源：anthropic.com/responsible-scaling-policy
- [URL: 待补]

### 4.5 Anthropic Constitutional AI（2022 训练阶段方法）

- 出现位置：第 21 篇 L117-122
- 建议来源：anthropic.com/research/constitutional-ai-harmlessness-from-ai-feedback
- [URL: 待补]

### 4.6 Anthropic Constitutional Classifiers（2025 推理阶段方法）

- 出现位置：第 21 篇 L123-128
- 建议来源：Anthropic 2025 Research 公告
- [URL: 待补]

### 4.7 Microsoft Responsible AI Standard v2

- 核心：「frequency × severity」二维矩阵
- 出现位置：第 11 篇 L48-49 / 第 14 篇 L115-122 / 第 24 篇 L78-93 / L185-191
- 来源 A（Microsoft CDN 官方 PDF）：https://cdn-dynmedia-1.microsoft.com/is/content/microsoftcorp/microsoft/final/en-us/microsoft-brand/documents/Microsoft-Responsible-AI-Standard-General-Requirements.pdf
- 来源 B（Microsoft Blog 存档 PDF）：https://blogs.microsoft.com/wp-content/uploads/prod/sites/5/2022/06/Microsoft-Responsible-AI-Standard-v2-General-Requirements-3.pdf

### 4.8 Microsoft Azure AI Content Safety

- 核心：四类伤害 × 四级严重度
- 出现位置：第 14 篇 L160-164
- 建议来源：learn.microsoft.com/en-us/azure/ai-services/content-safety/
- [URL: 待补]

### 4.9 Anthropic Acceptable Use Policy

- 出现位置：要点列表（正文未深入展开）
- 建议来源：anthropic.com/legal/aup
- [URL: 待补]
- ⚠️ 注：作者可考虑补充正文或从索引删除

### 4.10 SWE-bench Verified

- 维护方：OpenAI（基于 SWE-bench 团队）
- 500 条 Python hand-curated 高质量样本
- 出现位置：第 12 篇 L53-58 / L321 / 第 08 篇 表格中分数
- 建议来源：openai.com/index/introducing-swe-bench-verified/
- [URL: 待补]

### 4.11 OpenAI Evals Repo

- YAML + JSONL 数据结构；oaieval / oaievalset CLI
- 出现位置：第 12 篇 L254-263
- 建议来源：github.com/openai/evals
- [URL: 待补]

### 4.12 Inspect AI（UK AISI）

- 维护方：UK AI Safety Institute
- 四层抽象 Dataset → Task → Solver → Scorer
- 出现位置：第 12 篇 L264-271
- 建议来源：inspect.aisi.org.uk
- [URL: 待补]

### 4.13 Anthropic 统计学方法论文

- 核心：eval 结果要带置信区间
- 出现位置：第 02 篇 L110 / 第 08 篇 L143 / 第 12 篇 L273-279
- 建议来源：anthropic.com/research/statistical-approach-to-model-evals
- [URL: 待补]

### 4.14 Scrum.org《Definition of Done for AI Agents》

- 出现位置：第 01 篇 L70-74 / 第 02 篇 L46-48 / 第 11 篇 L206-209
- 建议来源：scrum.org 博客文章
- [URL: 待补]

### 4.15 Google Model Card（2018）+ Cambridge AI Product Card（2024）

- 出现位置：第 02 篇 L35
- 建议来源：cambridge.org/core/journals/data-and-policy
- [URL: 待补]

### 4.16 Anthropic Engineering Manager / Evals 招聘

- 关键事实：Evals 相关 EM base 区间到 $300K+；Netflix 招 "Software Engineer L4/L5, LLM Evaluation"
- 出现位置：第 02 篇 L69-71 / 第 13 篇 L84
- 建议来源：anthropic.com/careers / netflix careers 公开 JD
- [URL: 待补]

### 4.17 Anthropic 58 工具 token 数据 + Tool Search

- 关键事实：58 工具吃 ~55K token；Claude Opus 4.5 上 Tool Search 把准确率从 79.5% → 88.1%
- 出现位置：第 05 篇 L40-52 / L158-162
- 建议来源：Anthropic Engineering Blog（2025-2026）
- [URL: 待补]

### 4.18 OSWorld benchmark

- 数据（2024-Q4 快照）：Operator (CUA) 38.1% / Anthropic Computer Use 22.0% / 人类基线 72.4%
- 出现位置：第 02 篇 L154 / 第 05 篇 L66-71 / L263
- 建议来源：os-world.github.io / 原论文
- [URL: 待补]

### 4.19 PromptArmor / Lakera 红队工具

- 出现位置：第 19 篇 L75
- 建议来源：promptarmor.com / lakera.ai
- [URL: 待补]

### 4.20 Vellum / Traceloop 业内 best practice

- 引用观点：连续 N 次错误熔断 + spike detection + per-user hard cap
- 出现位置：第 15 篇 L108-117
- 建议来源：vellum.ai / traceloop.com 博客
- [URL: 待补]

### 4.21 Illinois 州法 + Texas TRAIGA

- Illinois（2025）："Wellness and Oversight for Psychological Resources Act" 禁止 AI 制定心理健康治疗方案
- Texas TRAIGA（2026-01 部分生效）：医师必须书面披露 AI 用于诊断
- 出现位置：第 22 篇 L62-65 / L156-158 / L240-243
- 建议来源：Illinois 州官方立法 PDF + Texas TRAIGA 官方文件
- [URL: 待补]

---

## 类 5：模型公司公开数据 / 价格 / benchmark

### 5.1 2026-Q2 主流模型对比表（第 08 篇 L31-49 核心数据）

| 模型 | 输入价 | 输出价 | 缓存读 | SWE-bench Verified | 首 token 延迟 | 合规 |
|------|-------|-------|-------|-------------------|------------|------|
| Claude Opus 4.7 | $5/M | $25/M | $0.50/M | 87.6% | ~2s | SOC2 II / HIPAA BAA / ZDR |
| Claude Sonnet 4.6 | $3/M | $15/M | $0.30/M | ~82% | 2s | 同上 |
| Claude Haiku 4.5 | $1/M | $5/M | $0.10/M | ~73% | <1s | 同上 |
| GPT-5.5 | $5/M | $30/M | 10% 自动 | 88.7% | 0.55s | SOC2 II / HIPAA |
| GPT-5.1 | $1.25/M | $10/M | 自动 | ~80% | <1s | 同上 |
| GPT-5 | $0.625/M | $5/M | 自动 | ~75% | <1s | 同上 |
| Gemini 3 Flash | $0.50/M | $3/M | - | 80.6% | 亚秒 | Vertex VPC SC / HIPAA BAA |
| DeepSeek V3.2 | $0.28/M | $0.42/M | 内置 cache hit $0.028 | ~70% | 中等 | 中国境内，无 BAA |
| Kimi K2.6 | $0.60/M | $2.50/M | - | ~75% | 中等 | 中国境内，无 BAA |

- 建议来源（按厂商）：
  - Anthropic：anthropic.com/pricing + model cards
  - OpenAI：openai.com/pricing + model cards
  - Google：ai.google.dev/pricing + Gemini model cards
  - DeepSeek：api-docs.deepseek.com
  - Kimi (Moonshot)：platform.moonshot.cn
  - 第三方榜单：artificialanalysis.ai / SEAL
- [URL: 待补 × 每家厂商]

### 5.2 Anthropic Opus 4.7 新 tokenizer 涨 35% 数据

- 来源：Finout 文章
- 出现位置：第 08 篇 L176-186
- 建议来源：finout.io 博客
- [URL: 待补]

### 5.3 Anthropic prompt caching 决策线

- system prompt > 1024 token + 复用率 > 2 次
- 出现位置：第 08 篇 L157-172
- 建议来源：Anthropic 官方文档 prompt caching
- [URL: 待补]

### 5.4 OpenAI / Azure monthly budget hard cap

- 出现位置：第 15 篇 L98-106
- 建议来源：platform.openai.com / learn.microsoft.com Azure docs
- [URL: 待补]

### 5.5 各 AI Observability SaaS 工具

- Datadog LLM Observability（factuality / toxicity / relevance）
- Braintrust（eval-driven development + CI/CD gates）
- Arize（企业级 AI observability）
- Helicone（一行 proxy）
- Traceloop（OpenTelemetry user_id 注入 trace）
- LangSmith（LangChain 官方）
- 出现位置：第 20 篇 L42 / L48 / L52 / L79 / L91 / L205-228 / 第 23 篇 L143-147
- 建议来源：datadoghq.com / braintrust.dev / arize.com / helicone.ai / traceloop.com / smith.langchain.com
- [URL: 待补 × 每家]

---

## 发布前 checklist

- [ ] 每条引用都补上具体 URL
- [ ] URL 失效的引用 → 改为"据 X 报道"模糊表述
- [ ] 高度敏感的引用（KOL 名言）→ 双重核对原始来源是否为公开演讲 / 文章
- [ ] 模型价格 / benchmark 数据（类 5）发布前 7 天内重核厂商官方 model card
- [ ] Air Canada / NYC MyCity / Chevy Tahoe 等判例类引用 → 核对原始判决书 / 调查报道链接
- [ ] Khan Academy Khanmigo / Nabla / Anthropic AUP 等只在要点列出但正文未深入的引用 → 决定补充正文或从索引删除
- [ ] OpenAI / Anthropic 财务数据 → 必须以官方披露或权威媒体（The Information / Reuters）为唯一来源
- [ ] Anthropic Postmortem / OpenAI sycophancy postmortem → 链接到官方 incident report 页
- [ ] 配套资产清单：本《参考资料索引》将作为付费读者解锁的配套资产之一

---

## 高曝光风险引用（URL 优先补）

按出现频次排序，这些是"被同行抓 URL 概率最高"的：

| 引用 | 出现篇数 | 风险等级 |
|------|---------|---------|
| Air Canada Moffatt 案 | 7 篇 | ⭐⭐⭐ 最高 |
| OpenAI GPT-4o sycophancy postmortem | 5 篇 | ⭐⭐⭐ 最高 |
| Cursor 2025-06 billing 暴雷 | 5 篇 | ⭐⭐⭐ 最高 |
| Hamel "EDD" 系列 | 4 篇 | ⭐⭐ 高 |
| OpenAI Model Spec | 3 篇 | ⭐⭐ 高 |
| Microsoft RAI Standard v2 | 3 篇 | ⭐⭐ 高 |
| Anthropic Cat Wu Product Note | 3 篇 | ⭐⭐ 高 |
| Cat Wu "prototypes over PRDs" | 3 篇 | ⭐⭐ 高 |
| Klarna 700 客服 | 3 篇 | ⭐⭐ 高 |

**作者发布前最优先**：补完上面 9 条的 URL，其他可以后续 batch 补。

---

> 配套资产 · 第一季《AI 时代 PM 工作流重构》
> 作者：蔡逸雯（公众号「蔡逸雯」）
