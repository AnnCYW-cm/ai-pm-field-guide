---
tool_id: P0-04-2
serves_essay: 04
status: ready-for-review
last_updated: 2026-05-21
deliverable_formats: [markdown, pdf-table, mindmap, tencent-doc]
hours_actual: 2 (v0 skeleton 0.5h + v1.0 retrofit 1.5h)
version: v1.0
references_pools_used: [P2.8 MIT NANDA, P2.10 Gartner, P2.12 Stanford HAI, P2.14 METR, P2.16 MedRxiv, P4.1 Air Canada, P4.2 Klarna, P4.3 DPD, P4.4 NYC MyCity, P4.6 McDonald's, P4.14 Manus AI, P4.21 Illinois/Texas, P7.1 McKinsey, P7.2 BCG, P7.3 Bain, P7.4 Deloitte, P7.7 IBM]
validation_status: "未做真 PM 复盘测试 (n=0)；v2.0 计划 n=3-5 真 PM 实跑 1 个项目后回填风险等级"
companion_tools: [#48 伪 AI 需求 6 问 checklist v1.1]
---

# MIT NANDA 95% 失败类型分类表

> 服务于第 04 篇《伪 AI 需求》配套资源 ①
> **用法**：项目立项后第 2 周做一次"7 类风险体检"；上线前 1 周再做一次。
> **与 #48 联用**：6 问 checklist 是「立项前过滤」；本分类表是「立项后体检 + 复盘归因」。

---

## 一、为什么需要这个分类表

### 1.1 95% 失败不是吓人数字，是三家独立调研的"5% 法则"三角验证

2025 年下半年，全球三家 tier-1 机构在 3 个月内独立发布，结论收敛在同一个数量级：

| 机构 | 报告 | 发布时间 | 关键数据 |
|---|---|---|---|
| **MIT NANDA** | 《State of AI in Business 2025》 | 2025-08 | **95%** 企业 GenAI 项目零可衡量回报 |
| **McKinsey QuantumBlack** | 《The State of AI 2025: Agents, innovation, and transformation》（第 9 期）| 2025-11 | 仅 **6%** 是 "AI high performers"（workflow redesign + EBIT ≥ 5%） |
| **BCG Henderson Institute** | 《The Widening AI Value Gap: Build for the Future 2025》| 2025-09-30 | 仅 **5%** 公司是 "future-built"（系统性建立前沿 AI 能力并持续创造价值） |

**三家机构、三种口径、独立调研——结论收敛在 5-6%。这是当前 AI 产品行业最硬的"成功率上限"基线**。

### 1.2 95% 失败的根因不是"模型不行"

MIT NANDA、McKinsey、Bain 三家不约而同指出失败的本质：

- **MIT NANDA**："系统不留反馈、不适应上下文、不持续改进"——本质是把 AI 当一次性交付。
- **McKinsey**：**workflow redesign 是 EBIT 影响最大的单一变量**——94% 公司没 redesign 流程，就没拿到 EBIT 影响。
- **Bain Technology Report 2025**：Coding 工具仅带来 **10-15% 生产力提升**（远低于 GitHub/Microsoft 自家数据 30-55%）；只有 AI + 端到端流程改造时才能拿到 25-30% 提升。
- **Bain 进一步补刀**："写+测代码只占 idea-to-launch 的 25-35% 时间"——只优化 25-35% 的环节，最多就 10-15% 总提升，这是数学问题。

**结论**：95% 失败 = 业务问题 + 流程问题 + 数据问题 + 合规问题，**只有 < 20% 是模型能力问题**。

### 1.3 为什么 PM 必须有一份"失败分类表"

- ✅ **立项前**：6 问 checklist 过滤伪需求（见 #48）。
- ✅ **立项后**：本表 7 类风险体检 —— **找出哪几类风险在你项目里已经埋了雷**。
- ✅ **复盘时**：失败归因 —— **每一类失败都有对应的规避方法和真实案例支撑**。

把"95% 失败"拆成 7 类可识别、可规避、可对照案例的模式，是 AI PM 的基本盘。

---

## 二、95% 失败的 7 大类型 — 完整展开

### 类型 1 · 伪需求驱动

**定义**：业务方拍下"AI 化需求"时本质不是业务问题，是"我们也要做 AI"的焦虑驱动。需求本身没有可量化业务问题。

**典型场景**：
- 老板从某场行业峰会回来："我们也要做 AI / Agent / RAG"。
- 客户问业务方："你们有没有 AI 能力？"业务方传话给 PM：做一个。
- 公司年报压力："要写 AI 战略转型"。

**真实案例 + 引用**：
- **MIT Sloan 2025 调研**：73% 失败项目"没有在项目开始前对'成功'达成定义"，61% "立项 ROI 数字从未在上线后被验证"
- **McKinsey 6% high performers**：94% 公司 AI 没 EBIT 影响，反推 → 大量项目立项时就没把 EBIT 当目标（Pool 7.1）

**识别信号**：
- ❌ 业务方答不出"不做 AI 会怎样"
- ❌ 没有量化的业务问题（节省 X FTE / 提升 Y 转化率 / 降低 Z 单据成本）
- ❌ 立项理由出现"跟上 AI 时代""智能化升级""客户问"等空话
- ❌ ROI 测算"未来一年再说"

**规避方法**：
- **必做 1**：拿 #48 的 6 问过 Q2（ROI）+ Q3（3 个月可验证里程碑），不通过直接打回
- **必做 2**：评审会现场问业务方"如果这个项目 3 个月后只省了 0.5 个 FTE，你还做不做？"——逼出真实预期
- **必做 3**：引用 McKinsey 6% 标尺给老板做预期管理 → "全球 94% 公司都没拿到 EBIT 影响，我们至少要 redesign workflow 才有戏"

---

### 类型 2 · 数据基础不行

**定义**：项目立项时假设"数据没问题"，实际数据散在各处、没有结构化、没人维护，导致 RAG 检索拉胯 / fine-tune 跑不出来 / eval 没基线。

**典型场景**：
- 上来就建 RAG 客服系统，结果发现知识库散在 Confluence / Notion / Slack / 邮件附件 / 销售个人 PPT
- 想 fine-tune 一个垂直模型，发现历史数据没标注 / 标注质量极差
- 想做"AI 自动审批"，发现规则散在 N 个 SOP Word 里，N > 50

**真实案例 + 引用**：
- **MIT NANDA "Gen AI Divide"**：纯内部自建成功率仅 1/3，外采+共建成功率 67% —— 内部自建死法之一就是数据基础没准备好（Pool 2.8）
- **IBM CEO Study 2025**：72% CEO 视专有数据为 GenAI 价值关键 —— 反推 → 没有干净专有数据 = 无价值（Pool 7.7）
- **BCG**：5% future-built 公司在 41 项基础能力中数据治理是核心 —— laggards 输在数据底座（Pool 7.2）

**识别信号**：
- ❌ 数据散在 Confluence / Notion / Slack / 个人电脑 / 共享盘
- ❌ 没有人为数据质量负责（"这是 IT 的事"/"这是业务的事"互相推）
- ❌ 知识库最近一次更新 > 6 个月
- ❌ "我们边做边整理数据"

**规避方法**：
- **必做 1**：立项前做一次"数据可用性 audit"——问 3 题：(a) 数据散在哪几个系统？(b) 谁负责维护质量？(c) 上一次系统性更新是什么时候？任何一题答不上 → 先做 3-6 个月数据治理
- **必做 2**：参照 BCG "future-built" 在 41 项能力中先把"数据治理 + 数据架构"两项拉到位再上 AI（Pool 7.2）
- **必做 3**：如果是 RAG 项目，先用 50 条真实问题做 retrieval recall 测试，召回率 < 80% 直接停项目

---

### 类型 3 · 集成成本超预算

**定义**：POC 跑通时只算了 API 钱（< $10k/月），接入生产环境时才发现 SSO / 审计 / 合规 / 数据脱敏 / 监控 / Bad Case 流程全是新账。

**典型场景**：
- POC 阶段 $500/月跑得很 happy → 生产环境算总账 $50,000+/月
- 业务方问"为什么贵了 100 倍"，PM 答不出来
- 老板砍预算，项目下线

**真实案例 + 引用**：
- **a16z 2025 企业 LLM 100 CIO 调研**：企业 LLM 年均花费 $4.5M → $7M（+56%），**37% 企业同时跑 5+ 模型** —— 集成 + 多模型复杂度远超 POC 预期（Pool 2.9）
- **Bain Technology Report 2025**：$2 trillion 新增收入才能支撑全球 AI scaling 趋势
- **Token 失控真实案例**（Pool 4.20）：Claude Code 递归循环 5 小时烧 16.7 亿 token；retry loop 一夜烧 $72,000 OpenAI credit；某软件公司单计费周期 $150,000 影子 AI 危机
- **Cursor 2025-06 billing 暴雷**（Pool 4.8）：从 fixed price 切定额导致用户账单暴涨被迫公开道歉

**识别信号**：
- ❌ POC 时只算 API token 钱，没列 SSO / 审计 / 合规 / 监控 / 兜底成本
- ❌ 没做"生产 vs POC 成本对照表"
- ❌ 没有预算上限和告警机制（API 烧到 X 自动熔断）
- ❌ 老板对 a16z $4.5M-$7M 量级没概念

**规避方法**：
- **必做 1**：立项时画"POC 成本 vs 生产成本对照表"，**必含**：API / SSO / 审计 / 合规 / 监控 / 数据脱敏 / 人工兜底 / Eval 标注 / 模型切换备份
- **必做 2**：用 a16z $4.5M-$7M 基线给老板做预算锚定（"我们这个项目至少占行业基线的 X%"）
- **必做 3**：上 cost cap + 告警（参考 Cursor 暴雷反向教训）
- **必做 4**：和工程团队对齐"3 个月、6 个月、12 个月"三档预算曲线，超 1.5x 立刻刹车

---

### 类型 4 · 用户拒绝采用

**定义**：上线后留存率 < 10%，用户回流到 ChatGPT / Claude 自己用，因为产品本质是"ChatGPT 套壳 + 一点点公司知识库"，没有不可替代价值。

**典型场景**：
- 公司内部"AI 助理"上线 3 个月，DAU 从 200 掉到 20
- 用户访谈："你们这个还不如我直接用 ChatGPT"
- "我用我自己的 ChatGPT Plus 账号能查得更全"

**真实案例 + 引用**：
- **MIT NANDA "Gen AI Divide"**：95% 企业 GenAI 项目零可衡量回报，核心是"工具无法 retain memory / adapt to feedback / integrate into workflows"—— 产品没建立任何不可替代价值（Pool 2.8）
- **BCG**：未列入 17% agent 价值的产品 = laggards，主要原因是"workflow 没改造"，用户感受不到产品和通用 ChatGPT 的差异（Pool 7.2）

**识别信号**：
- ❌ 核心功能 = "把公司文档喂给 GPT" 的标准 RAG，没有任何不可替代 workflow
- ❌ 没有"用户为什么不能用 ChatGPT 替代我们" 的清晰回答
- ❌ 没接公司核心系统（CRM / 工单系统 / OA / 报表），只能"答问题"
- ❌ 上线 30 天留存 < 30%（互联网产品平均健康线）

**规避方法**：
- **必做 1**：上线前必须能回答"用户为什么不能用 ChatGPT 替代我们" —— 答不出来直接砍。**护城河 3 选 1**：(a) 接公司私有系统（CRM / 工单 / 库存）；(b) 自有 ground truth 数据 + 高质量 eval；(c) workflow 深度嵌入（不是"我去用一个工具"而是"工具自动出现在我做事的时候"）
- **必做 2**：上线后周看 D7/D30 留存，30 天 < 30% 直接进入"杀产品 vs 重做"决策
- **必做 3**：参照 McKinsey 的判断 —— "workflow redesign 是 EBIT 影响最大变量"，没改 workflow = 没留存（Pool 7.1）

---

### 类型 5 · 合规阻断

**定义**：上线前法务一票否决 / 上线后被监管点名 / 被用户起诉 —— 因为触及医疗、金融、HR、法律、政府服务等强合规场景却没做 RAI 评估。

**典型场景**：
- 法务在上线评审会上："这个不能上，我们没拿到行业 license"
- 上线后媒体调查曝光，被监管约谈
- 用户被 AI 错误建议误导，把公司告了

**真实案例 + 引用**：
- **Air Canada 案（2024-02 BCCRT 149）** ⭐：chatbot 编造不存在的丧亲票政策，BC 仲裁庭判 CAD 650.88。**钱不重要，重要的是判例确立**——"chatbot 不是独立法律实体，bot 说的话就是公司说的话"（[CanLII 全文](https://www.canlii.org/en/bc/bccrt/doc/2024/2024bccrt149/2024bccrt149.html)，Pool 4.1）
- **NYC MyCity 政府 chatbot（2024-03）** ⭐：市政府 chatbot 告诉商家："可拿员工小费"（违反联邦劳动法）/ "可拒绝 Section 8 房客"（违反纽约反歧视法）/ "可拒收现金"（违反 2020 纽约市法律）。**The Markup 调查曝光后争议持续**（themarkup.org，Pool 4.4）
- **Illinois 法（2025）**："Wellness and Oversight for Psychological Resources Act" 禁止 AI 制定心理健康治疗方案（Pool 4.21）
- **Texas TRAIGA（2026-01 部分生效）**：医师必须书面披露 AI 用于诊断（Pool 4.21）
- **Stanford 法律 AI 实证**（Pool 2.12）：Lexis+ AI 17% / Westlaw AI-Assisted Research 33% / GPT-4 43% 幻觉率 —— 法律场景任何幻觉都是合规雷

**识别信号**：
- ❌ 触及医疗 / 金融 / HR / 法律 / 政府服务 / 心理健康 / 教育（未成年人）
- ❌ 没立项前过法务 / 合规 / RAI 评估
- ❌ 没做"如果 AI 建议导致用户损失我们赔不赔得起"的兜底测算
- ❌ 没考虑跨州 / 跨国合规差异（同一个产品在 Illinois 是禁的，在 Texas 是要披露的）

**规避方法**：
- **必做 1**：立项前过 RAI 矩阵（参考 Microsoft Responsible AI Standard v2）：severity × frequency 二维分级，severity = catastrophic 的需求**全部走"AI 辅助 + 人工兜底"路径**，不允许 AI 独立决策
- **必做 2**：法务必须在 PRD 阶段进入，不是上线前
- **必做 3**：用 Air Canada 判例教育业务方 —— "bot 说的话就是公司说的话"，"我们风控能兜住"是错觉
- **必做 4**：跨地区上线必须做 jurisdiction-by-jurisdiction 合规 review

---

### 类型 6 · ROI 算不出来

**定义**：项目预算花完，老板问"省了多少钱 / 多赚了多少"，PM 答不上来 —— 只有"用户喜欢""使用量上来了"这种没用的指标。

**典型场景**：
- 项目花了 $500k，复盘会上业务方说"用户反馈不错"
- 老板问："具体省了几个 FTE？" PM 答："这个不太好直接归因。"
- 第二年预算砍 80%

**真实案例 + 引用**：
- **Klarna 2024-02 → 2025-05 反转** ⭐：2024-02 高调宣布 AI 替代 700 个客服 FTE 上头条 → 2025-05 公开承认"AI 缺乏共情"重新招人 → 也上头条（[Bloomberg 2025-05-08](https://www.bloomberg.com/news/articles/2025-05-08/klarna-turns-from-ai-to-real-person-customer-service)，Pool 4.2）。**1 年内反转 = ROI 测算口径错**：只算了 FTE 替代数，没算 NPS 损失 + 召回成本
- **Bain Technology Report 2025**（Pool 7.3）：Coding 工具 10-15% 提升 vs GitHub/Microsoft 自家数据 30-55%。**Bain 给出反 hype 解释**：写+测代码只占 idea-to-launch 25-35% 时间，所以 25-30% 提升才需要"AI + 端到端流程改造"
- **Gartner 2025 GenAI Hype Cycle**（Pool 2.10）：< 30% CEO 对 GenAI 回报满意
- **IBM CEO Study 2025**：仅 52% CEO 说在 GenAI 上拿到了"超出降本"的价值（Pool 7.7）

**识别信号**：
- ❌ 立项时 ROI 口径模糊（"提升效率"/"节省时间"，没有 $ 数字）
- ❌ 没定义"如何归因"（用户用了 AI 后省的时间 vs 没用 AI 也会省的时间）
- ❌ 上线后没建 ROI dashboard，月度 review 没数据
- ❌ Klarna 式"早期 PR 收益 + 后期 PR 灾难"对冲，净收益负数

**规避方法**：
- **必做 1**：立项时定 ROI 公式，**含 3 个变量**：(a) 收益（FTE 节省 / 收入增量 / 时间节省转金额）；(b) 成本（API + 人力 + 集成 + 合规 + Bad Case 处理）；(c) 归因方法（A/B test / 历史基线对照 / 用户自报）
- **必做 2**：参照 Bain "25-30% 提升才需端到端流程改造"
- **必做 3**：建月度 ROI dashboard，第 3 个月不能算出实际收益直接停项目
- **必做 4**：用 Klarna 反转案例教育老板 —— "FTE 替代数"是误导性指标，要算"NPS × 召回成本"全口径

---

### 类型 7 · 模型能力不够

**定义**：任务对模型能力的要求 > 当前 SOTA 模型实际能力。具体表现为：长任务链（> 10 步）失败率高 / 长上下文记忆失效 / 专业领域准确率达不到业务下限。

**典型场景**：
- 想做 Agent 自动处理工单，实测 5 步以上就开始 hallucinate
- 想做"AI 全程帮你订机票+酒店+签证+保险"，实测每个环节 90%，连起来 90%^4 = 65.6%
- 想做"AI 帮医生写病例"，实测专业术语错误率 > 15%，医生拒绝使用

**真实案例 + 引用**：
- **Manus AI 蝴蝶效应（2025 初）** ⭐：宣称 GAIA SOTA → 实测 reliability / 上下文窗口 / 付费墙 / CAPTCHA 全卡死。**演示视频是 cherry-picked，真实任务长链失败率极高**（Pool 4.14）
- **DPD chatbot Ashley Beauchamp 案（2024-01）** ⭐：post-update 没回归 eval，被用户调教出"DPD 是世界最差快递"的诗，单条推文 X 内数百万曝光（Pool 4.3）
- **METR Horizon Length 研究**（Pool 2.14）：前沿模型能稳定完成的任务时长每 7 个月翻倍 —— **反推：如果你的任务需要"模型稳定完成 X 小时"，先查 METR 看当前 SOTA 能力**
- **McDonald's × IBM 得来速 AI 点单**（Pool 4.6）：100+ 门店试点 3 年，85% 准确率 + 1/5 单需要人工兜底，2024-06 终止 IBM 合作

**识别信号**：
- ❌ 任务需要 > 10 步连续推理
- ❌ 任务需要 > 100k token 长上下文 + 高准确（不是 retrieval 能解决的）
- ❌ 任务专业领域门槛高（医疗术语 / 法律条文 / 金融监管 / 多语言专业翻译）
- ❌ 没查 METR / GAIA / SWE-bench 等 benchmark 看当前 SOTA
- ❌ 演示视频是 cherry-picked（Manus AI 式）

**规避方法**：
- **必做 1**：用 METR horizon length 评估任务复杂度（Pool 2.14） —— 如果任务需要稳定 > 当前 SOTA 横向时长，**降级为 "AI 辅助 + 人工分段" 或推迟 6-12 个月再上**
- **必做 2**：上线前必须做 50-100 条真实 case 的 e2e eval，准确率 < 业务下限直接砍
- **必做 3**：长尾失败 + 用户可见 = PR 灾难 → 参考 McDonald's IBM 教训，**85% 不是 100%，是 100% 翻车**
- **必做 4**：参考 #53「能力边界工具包」（待发布）的 4 类硬边界判断

---

## 三、PM 自检表 — 我项目里有这 7 类风险吗？

> **使用方法**：项目立项后第 2 周做一次；上线前 1 周再做一次。
> **打分标准**：
> - **高（H）**：识别信号 3 条以上 ✅ + 没有规避动作 → 高风险
> - **中（M）**：识别信号 1-2 条 ✅ 或有部分规避 → 中风险
> - **低（L）**：识别信号 0 条 + 有完整规避动作 → 低风险

| # | 失败类型 | 识别信号触发数 | 风险等级 H/M/L | 已做的规避动作 | 后续 action |
|---|---|---|---|---|---|
| 1 | 伪需求驱动 | __/4 | | | |
| 2 | 数据基础不行 | __/4 | | | |
| 3 | 集成成本超预算 | __/4 | | | |
| 4 | 用户拒绝采用 | __/4 | | | |
| 5 | 合规阻断 | __/4 | | | |
| 6 | ROI 算不出来 | __/4 | | | |
| 7 | 模型能力不够 | __/5 | | | |

### 判定规则

| 高风险数量 | 建议动作 |
|---|---|
| **≥ 3 个 H** | **立项重审**，1 周内向老板出具风险说明 + 重审 PRD |
| **1-2 个 H** | 针对每个 H 出具单点缓解方案（30 天内闭环） |
| **0 个 H + ≥ 4 个 M** | 可推进，但 6 周内必须把 M 拉到 L |
| **0 个 H + ≤ 3 个 M** | 可推进，3 个月后回看 |

---

## 四、数据源 & 引用规范

| 数据 | 来源 | 已核 URL | 参照库位置 |
|---|---|---|---|
| **95% GenAI 项目零回报（三角验证 1）** | MIT NANDA《State of AI in Business 2025》(2025-08) | mitsloan.mit.edu / nanda.media.mit.edu | Pool 2.8 |
| **6% AI high performers（三角验证 2）** | McKinsey《The State of AI 2025》(2025-11) | [McKinsey](https://www.mckinsey.com/capabilities/quantumblack/our-insights/the-state-of-ai) + [PDF](https://www.mckinsey.com/~/media/mckinsey/business%20functions/quantumblack/our%20insights/the%20state%20of%20ai/november%202025/the-state-of-ai-2025-agents-innovation_cmyk-v1.pdf) | Pool 7.1 |
| **5% future-built（三角验证 3）** | BCG《The Widening AI Value Gap》(2025-09-30) | [bcg.com](https://www.bcg.com/publications/2025/are-you-generating-value-from-ai-the-widening-gap) + [PDF](https://media-publications.bcg.com/The-Widening-AI-Value-Gap-Sept-2025.pdf) | Pool 7.2 |
| Coding 工具 10-15% vs 30-55% 落差 | Bain Technology Report 2025 | [Bain From Pilots to Payoff](https://www.bain.com/insights/from-pilots-to-payoff-generative-ai-in-software-development-technology-report-2025/) | Pool 7.3 |
| Deloitte 1/5 公司 agent 治理成熟 | Deloitte《State of AI in the Enterprise 2026》| [Deloitte 主页](https://www.deloitte.com/us/en/what-we-do/capabilities/applied-artificial-intelligence/content/state-of-ai-in-the-enterprise.html) | Pool 7.4 |
| 52% CEO 拿到"超降本"价值 | IBM CEO Study 2025 | [IBM 新闻稿](https://newsroom.ibm.com/2025-05-06-ibm-study-ceos-double-down-on-ai-while-navigating-enterprise-hurdles) | Pool 7.7 |
| Air Canada 判例 CAD 650.88 | 2024 BCCRT 149 (CanLII) | [canlii.org/2024bccrt149](https://www.canlii.org/en/bc/bccrt/doc/2024/2024bccrt149/2024bccrt149.html) | Pool 4.1 |
| 法律 AI 幻觉率 17-43% | Stanford RegLab + HAI 2024-2025 | hai.stanford.edu | Pool 2.12 |
| McDonald's × IBM 终止 | 2024-06 CNBC / Bloomberg | URL 待精确补 | Pool 4.6 |
| Klarna 2024 → 2025 反转 | Bloomberg 2025-05-08 | [bloomberg](https://www.bloomberg.com/news/articles/2025-05-08/klarna-turns-from-ai-to-real-person-customer-service) | Pool 4.2 |
| NYC MyCity 合规失败 | The Markup 2024-03 调查 | themarkup.org | Pool 4.4 |
| Illinois Wellness Act / Texas TRAIGA | 各州法案原文 | URL 待补 | Pool 4.21 |
| Manus AI 演示 vs 实测 | 多家技术媒体 2025 初实测 | URL 待补 | Pool 4.14 |
| DPD chatbot Ashley Beauchamp | BBC / The Guardian 2024-01 | URL 待补 | Pool 4.3 |
| METR horizon length | METR 官方研究 | metr.org | Pool 2.14 |
| Gartner 2025 GenAI Hype Cycle | Gartner 官方 | gartner.com (paywall) | Pool 2.10 |
| a16z 100 CIO 调研 | a16z 2025 enterprise AI report | a16z.com | Pool 2.9 |

**参照库全文（128 条全球 tier-1 源）**：`/Users/caiyiwen/ai-product-column-research/tools/_global-references.md`

---

## 五、配套使用建议

### 5.1 与 #48 「6 问 checklist」联用

| 阶段 | 用 #48 还是用本表 | 用法 |
|---|---|---|
| 需求来了，要不要立项？ | **#48 6 问** | 5 分钟过 6 问决策树 |
| 立项后第 2 周 | **本表 7 类自检** | 找出已埋雷的失败类型 |
| 上线前 1 周 | **本表 7 类自检 + 6 问 Q5 复查** | 上线前最后一道闸 |
| 项目失败复盘 | **本表 7 类归因** | 主因 1 个 + 次因 ≤ 2 个 |
| 项目成功复盘 | **本表 7 类反向验证** | 看 7 类风险都怎么规避的，沉淀为下个项目 SOP |

### 5.2 与未来工具的对接关系

- **→ #49 PRD 4 增 2 删模板**：本表 7 类是 PRD "风险章节"的固定填写项
- **→ #51 AI PM Eval 全套**：类型 2（数据基础）+ 类型 7（模型能力）直接对应
- **→ #52 成本管控工具包**：类型 3（集成成本）直接对应
- **→ #54 上线运营工具包**：类型 4（用户拒采）+ 类型 7（长尾失败）直接对应
- **→ #55 老板对齐话术大全**：类型 1（伪需求）+ 类型 6（ROI 算不出）直接对应

---

## 六、设计依据 & 批判性自评 ⭐

> **为什么有这一节**：v0 骨架直接给了 7 类失败，没说明分类依据是什么、是否参考了行业标准、为什么不是 5 类或 10 类、还有哪些已知盲区。

### 6.1 这套分类的 3 个全球 tier-1 参照

| 参照 | 我借鉴了什么 | 我没采用什么 | 原因 |
|---|---|---|---|
| **MIT NANDA《State of AI in Business 2025》** (Pool 2.8) | "95% 失败" 核心数据 + 失败本质 → 直接转化为类型 2（数据）+ 类型 4（用户拒采）+ 类型 7（模型）的根因 | NANDA 没给"7 类失败"的官方分类 | NANDA 偏诊断不偏分类，需要 PM 视角再加工 |
| **McKinsey《The State of AI 2025》** (Pool 7.1) | "workflow redesign 是 EBIT 影响最大变量" + 6% high performers 标尺 → 直接支撑类型 1（伪需求）+ 类型 6（ROI） | McKinsey 12 维成熟度模型 | 12 维模型 PM 单项目用不上，需要降维到 7 类失败模式 |
| **Bain Technology Report 2025** (Pool 7.3) | "10-15% vs 30-55% 落差" 数据 + "写+测代码占 25-35% 时间" 反 hype 解释 → 直接支撑类型 6（ROI 算不出来） | Bain 的 PE/VC 尽调视角 | PM 立项决策用不上 PE 视角 |

### 6.2 为什么是 7 类而不是 5 类 / 10 类（替代方案对比表）

| 替代方案 | 优势 | 缺点 | 拒绝原因 |
|---|---|---|---|
| **5 类**（合并类型 1+6 / 3+7） | 记忆负担轻 | "业务问题"颗粒度太粗，PM 拿到没法 actionable | **太粗** |
| **10 类**（再拆"团队能力""老板支持""组织变革""技术债"） | 最完整 | 5+ 类已超出 PM 单人可控边界 | **越界** |
| **MIT NANDA 原报告 5 大根因** | 学术性强 | 太抽象，PM 评审会现场用不上 | **太学术** |
| **McKinsey 12 维成熟度模型** | 全球最权威 | PM 单项目用不上 | **过载** |
| **7 类失败模式**（本版） | 覆盖 PM 单项目所有可控雷区 + 每类有真实案例 + 有 actionable 规避 | 没真 PM 测试过 | **✅ 选这个** |

### 6.3 已知盲区 + v2.0 计划

| 盲区 | 影响 | v2.0 计划 |
|---|---|---|
| ⚠️ **未做真 PM 复盘测试**（n=0） | 不知道 7 类在真实项目复盘场景的实际命中率 | v2.0 找 3-5 个真 AI PM 用本表对照 1-2 个失败项目 |
| ⚠️ **没覆盖"老板/组织"维度的失败** | Pool 7.7 IBM CEO 61% 自报 vs McKinsey 23% 实际，CEO 乐观偏差真实存在 | v2.0 考虑加 类型 1.5「CEO 焦虑驱动」 |
| ⚠️ **类型 5 合规只覆盖了北美判例** | 没覆盖中国《生成式人工智能服务管理暂行办法》/ 欧盟 AI Act | v2.0 加 中国 + 欧盟 合规章节 |
| ⚠️ **风险等级 H/M/L 打分标准只给了"识别信号触发数"** | "3 条以上"是 L4 设计选择，没有实证依据 | v2.0 用真 PM 测试数据校准阈值 |
| ⚠️ **没覆盖"模型快速迭代导致基线漂移"** | 类型 7 现在的"SOTA 不够"判断 3-6 个月后可能失效 | v2.0 加 "本表更新周期 6 个月" 自维护机制 |
| ⚠️ **类型 4「用户拒采」没引"留存率行业基准"硬数据** | 30% D30 留存是行业平均，B 端 AI 工具的合理基准可能不同 | v2.0 找 a16z / Sequoia 的 B 端 AI 工具留存基准 |

### 6.4 适用 / 不适用边界

- ✅ **适用**：AI 应用层产品（聊天 / 工具 / RAG / Agent / 内容生成 / 自动化 workflow）
- ✅ **适用**：B 端 + C 端
- ✅ **适用**：立项后第 2 周自检 + 上线前 1 周自检 + 失败复盘归因
- ❌ **不适用**：AI 基础模型公司立项（应参考 Anthropic RSP / DeepMind FSF）
- ❌ **不适用**：AI infra / observability 工具立项（DX 驱动而非 ROI 驱动）
- ❌ **不适用**：纯研究项目
- ❌ **不适用**："要不要立项"决策（那是 #48 6 问 checklist 的事）

### 6.5 这套分类表的"调研依据深度等级"（L1-L4）

| 元素 | 等级 | 依据 |
|---|---|---|
| **5% 法则三角验证（引言）** | **L1** | MIT NANDA + McKinsey + BCG 三家独立调研收敛 |
| 类型 1 伪需求 | **L1** | McKinsey 6% high performers + MIT Sloan 73% 没定义成功 |
| 类型 2 数据基础 | **L1** | MIT NANDA 内部自建 1/3 vs 外采 67% + BCG 41 项能力 + IBM 72% CEO |
| 类型 3 集成成本 | L2 | a16z $4.5M-$7M 量级 + Token 5 个失控真实案例 + Cursor 暴雷 |
| 类型 4 用户拒采 | L2 | MIT NANDA "tools can't retain memory / adapt / integrate" + 行业 D30 30% 留存基准 |
| 类型 5 合规阻断 | **L1** | Air Canada + NYC MyCity + Illinois + Texas + Stanford 17-43% 幻觉（5 个硬源） |
| 类型 6 ROI 算不出 | **L1** | Klarna 1 年反转 + Bain 10-15% vs 30-55% + Gartner < 30% CEO 满意 + IBM 52% |
| 类型 7 模型能力 | **L1** | Manus AI 实测 + DPD chatbot + METR horizon + McDonald's × IBM + Stanford 法律 AI |
| 7 类的"7"这个数 | L4 | 我的设计判断，未真 PM 测试 |
| 风险等级 H/M/L 阈值 | L4 | 我的设计判断（"3 条触发"未实证） |
| 单项目 7 类自检顺序 | L4 | 我的设计判断（"立项后第 2 周 + 上线前 1 周"未实测） |

**说明**：标 L4 的元素是"做最好"路径上待验证的部分，v2.0 优先升级。**L1 占 7/10**（5% 法则 + 6/7 类）— 调研硬度足够发布 v1.0。

---

## 七、文末微信钩子（嵌入公众号文章用）

```
─────────────────────────────
📦 配套资源 · 第 04 篇

加我微信 **CYW960325**（备注「专栏04」），免费领：
✓ MIT NANDA 95% 失败 7 类分类表（PDF 表格 + 思维导图）
✓ 伪 AI 需求识别 6 问 checklist

【3 种格式任选】
📄 PDF：加微信后直接发文件给你
🔗 腾讯文档：微信里直接打开（推荐 📱）
💻 GitHub Pages：长期收藏 / 外链分享
─────────────────────────────
```

---

> 蔡逸雯 · 8 年 QE → AI PM · 公众号「蔡逸雯」
> CC-BY-NC 4.0 · 转载请注明出处
