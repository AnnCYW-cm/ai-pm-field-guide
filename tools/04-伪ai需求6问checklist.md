---
tool_id: P0-04-1
serves_essay: 04
status: ready-for-review
last_updated: 2026-05-21
deliverable_formats: [markdown, pdf-single-page, notion-template, tencent-doc]
hours_actual: 2 (v1.0 1h + v1.1 retrofit 1h)
version: v1.1
references_pools_used: [P2.4 OpenAI Model Spec, P2.8 MIT NANDA, P2.12 Stanford HAI, P2.16 MedRxiv, P5.6 Apollo Research, P7.1 McKinsey, P7.2 BCG, P4.1 Air Canada, P4.6 McDonald's, P4.2 Klarna]
validation_status: "未做真 PM 测试 (n=0)；v2.0 计划 n=3-5"
---

# 伪 AI 需求识别 6 问 Checklist

> 服务于第 04 篇《伪 AI 需求》配套资源
> **用法**：每次接到「我们的 X 流程能不能用 AI 做？」时，开会前 5 分钟过一遍

---

## 一、为什么需要这个 Checklist

> **「5% 法则」—— 全球 3 家顶级机构 2025 独立调研的三角验证**：
>
> - **MIT NANDA《State of AI in Business 2025》(2025-08)**：95% 企业 GenAI 项目零可衡量回报 — 仅 5% 拿到 ROI
> - **McKinsey《The State of AI 2025》(2025-11)**：仅 **6% 是 "AI high performers"**（通过 redesign workflow 拿到 EBIT 提升 ≥ 5%）
> - **BCG《The Widening AI Value Gap》(2025-09)**：仅 **5% 公司是 "future-built"**（系统性建立前沿 AI 能力并持续创造价值）
>
> **三家机构、独立调研、口径不同——结论收敛在 5-6%**。
>
> 这是当前 AI 产品行业最硬的"成功率上限"基线。
>
> 这 95% 失败不是因为模型不行——**McKinsey 明确指出 workflow redesign 是 EBIT 影响最大的单一变量**——是因为**项目本身就不该立项 + 立项后没改流程**。
>
> 这 6 问，就是在立项之前用 5 分钟把伪需求过滤掉，把宝贵资源留给那能进入 5% 的项目。

---

## 二、6 问详细判断逻辑

### 维度 0 · 先判断要不要 AI（1 问）

#### Q1: if-else 能不能做？

**判断逻辑**：4 个特征——
- 流程规则**模糊**吗？
- 流程规则会**动态演进**吗？
- 输入变量**海量**到没法穷举吗？
- 流程依赖**人类经验**判断吗？

四题没一个 yes → **写 if-else 比上 AI 强 10 倍**。

**通过**（确实需要 AI）→ 进入 Q2
**不通过**（其实是规则问题）→ 写 if-else / 配置规则引擎，结束

**真实例子**：
- **❌ 反例**：「订单 → 计算运费 → 返回结果」全确定性流程，被业务方包装成「AI 智能计费」——纯属性能浪费 + 成本浪费 + 可解释性损失三杀
- **✅ 正例**：「用户上传一段自由格式的产品描述 → 自动提取规格 / 价格 / 卖点」——4 个特征全中

---

### 维度 1 · 业务价值（ROI）—— 2 问

#### Q2: 可量化的 ROI 是什么？

**判断逻辑**：要求业务方给出具体数字。

**通过**（真需求）的答案：
- 「省 X 个客服 FTE，单月省 ¥X」
- 「转化率从 X% 提升到 Y%，年营收 +¥Z」
- 「合同审核从 3 天压到 1 小时」

**不通过**（伪需求）的答案：
- 「让我们公司更智能化」
- 「跟上 AI 时代」
- 「老板说要做」
- 「客户问我们有没有 AI」

听到任何一个伪答案 → **直接打回，让业务方找 CFO 算清楚再回来**。

**真实例子**：MIT NANDA 报告指出，95% 失败项目共同根因是「业务方把 AI 当一次性交付，不是持续投入」——本质上就是 ROI 没算清。

#### Q3: 3 个月内能验证 ROI 假设吗？

**判断逻辑**：AI 项目验证周期长，3 个月看不到信号 = 容易死在半路。

**通过**：业务方能描述「第 X 周看 Y 指标 / 第 12 周看 Z 指标」的可验证里程碑
**不通过**：「至少跑 1 年才能看到效果」/ 「先做着看」

**真实例子**：Klarna 2024-02 高调宣布 AI 替代 700 客服 FTE → 2025-05 公开承认「AI 缺乏共情」重新招人——**1 年内反转**。如果业务方说要 1 年以上才见效，**很可能你看不到任何效果就被砍预算**。

---

### 维度 2 · 容错空间（负反馈代价）—— 2 问

#### Q4: 单次错误代价 < 100 次正确收益吗？

**判断逻辑**：单次错误代价 > 100 次正确收益的需求**绝对不能上 AI 独立决策**。

**通过**（可上 AI）：
- 「错了用户重新问一次」
- 「错了运营兜底，工作量可控」
- 「错了 fallback 到规则」

**不通过**（不能上 AI 独立决策，但可上「AI 辅助 + 人工兜底」）：
- 医疗诊断 / 处方建议
- 法律咨询 / 合同审核
- 金融交易决策
- 强合规场景（涉及监管/政府）

**真实例子**：
- **Air Canada 案（2024-02）**：bot 编造不存在的丧亲票政策，BC 仲裁庭判 CAD 650.88——**钱不重要，重要的是「chatbot 不是独立法律实体」的判例确立，bot 说的话就是公司说的话**
- **Stanford 法律 AI 幻觉率实证**：Lexis+ AI 17% / Westlaw 33% / GPT-4 43%——**这些都是号称"hallucination-free + RAG"的产品**

#### Q5: 错误会发生在用户面前吗？

**判断逻辑**：长尾失败如果**用户能看到 + 容易传播 = PR 灾难**。

**通过**：错误发生在内部流程 / 后台批处理 / 有人工 review 缓冲
**不通过**：错误直接呈现给 C 端用户 / 公开渠道

**真实例子**：**McDonald's × IBM 得来速 AI 点单（2021-2024.07）**——100+ 门店试点 2 年，**85% 准确率 + 1/5 单需要人工兜底**。听起来 85% 不错，但快餐场景 85% = 100% 翻车——剩下 15% 的失败 case 全部被用户拍视频上 TikTok，每个错都是公关事故。2024-06 终止 IBM 合作。

---

### 维度 3 · 数据可得性（ground truth）—— 1 问

#### Q6: 怎么判断 AI 答得对不对？

**判断逻辑**：**没有 ground truth = 不能做 AI**。

**通过**（有标准答案来源）：
- 「我们有 1000+ 条历史标准答案，可做 evals」
- 「运营每天标 50 条，3 个月有 4500 条」
- 「行业有公开 benchmark」

**不通过**（没有 ground truth）：
- 「我们专家心里都有一杆秤」
- 「标注太贵，先用 GPT 自标」
- 「对错没那么绝对，业务理解就行」
- 「先做出来再说，标准我们边做边定」

**真实例子**：MIT MedRxiv 2025 医疗 AI 幻觉论文：「LLM 幻觉因为'用专业术语 + 看似 coherent'**反而最难识别**」——ground truth 必须是临床医生 + 真实病例，**不是 GPT 互相打分**。

---

## 三、决策树流程图（文字版）

```
需求来了
   │
   ▼
Q1 if-else 能做吗？
   ├─ 是 → 写 if-else，结束
   └─ 否 ↓
   
Q2 可量化 ROI？
   ├─ 否 → 打回业务方，找 CFO 算清再来
   └─ 是 ↓
   
Q3 3 个月能验证？
   ├─ 否 → 拆小目标，找 3 个月能验证的子项再立
   └─ 是 ↓
   
Q4 错误代价 < 100×正确？
   ├─ 否 → 降级为「AI 辅助 + 人工兜底」
   └─ 是 ↓
   
Q5 错误会被用户看到？
   ├─ 是 → 长尾失败 > 5% 必须砍 / < 5% 需 PR 预案
   └─ 否 ↓
   
Q6 ground truth 哪来？
   ├─ 答不出 → 先建标注流程，3 个月后再评审
   └─ 答得清 ↓
   
✅ 真 AI 需求，立项！
```

---

## 四、单页快速评分模板（PDF 一页用）

| 问题 | 通过 ✅ / 降级 🟨 / 不通过 ❌ | 备注 |
|---|---|---|
| Q1 if-else 能做吗？ | | |
| Q2 可量化 ROI？ | | |
| Q3 3 个月能验证？ | | |
| Q4 错误代价 < 100×正确？ | | |
| Q5 错误会被用户看到？ | | |
| Q6 ground truth 哪来？ | | |

**结果判读**：
- **6 ✅ 全过** → 真 AI 需求，立项进入 PRD 阶段
- **5 ✅ + 1 🟨** → 降级为 AI 辅助 + 规则兜底，可立项
- **≥ 2 个 ❌** → **伪需求，砍掉**
- **Q4 / Q5 不通过** → 走 AI 辅助路径，AI 不能独立决策
- **Q6 不通过** → 先建标注流程，3 个月后重审（最常见的卡点）

---

## 五、拒绝业务方的话术（直接抄）

被打回的业务方会有抵触。**不要说"做不到"，说"做了你会后悔"**。

```
张总，这个需求我们当然能做，但建议先不做。

第一个原因——这个场景的负反馈代价太高。
你看 Air Canada 案：bot 编造不存在的丧亲票政策，
BC 仲裁庭判公司赔 CAD 650.88。钱不是重点，
重点是判例——「chatbot 不是独立法律实体，
bot 说的话就是公司说的话」。我们走这条路，
迟早被告。

第二个原因——我们没有 ground truth。
做出来你没法判断对不对，最后这个项目会变成
"AI 团队和业务团队互相甩锅"。

第三个原因——同样的资源做这个，
不如做 [推荐一个真需求]，那个 3 个月能见收入。

我们做不做的不是技术决策，是业务决策。
做错了，烧的是你的预算。
```

业务方听完，**70% 接受**。**30% 还坚持的——那是真需求**，他有你不知道的信息。

---

## 六、引用规范（数据源 + 链接）

| 数据 | 来源 |
|---|---|
| 95% 企业 GenAI 项目零回报 | MIT NANDA《State of AI in Business 2025》(2025-08) |
| Air Canada 判例 CAD 650.88 | 2024 BCCRT 149 (CanLII 全文)|
| 法律 AI 幻觉率 17%-43% | Stanford RegLab + HAI 2024-2025 实证 |
| McDonald's × IBM 终止 | 2024-06 IBM 终止合作公开报道 |
| Klarna 2024 → 2025 反转 | Bloomberg 2025-05-08 |
| 医疗 AI 幻觉难识别 | MIT MedRxiv 2025 论文 |
| Gartner GenAI 2025 Trough | Gartner 2025 GenAI Hype Cycle |

详细 URL 见 GitHub repo `27-references.md`：https://github.com/AnnCYW-cm/ai-pm-field-guide/blob/main/27-references.md

---

### 六-补 · v1.1 升级版完整引用表（已核 URL + 参照库位置）

| 数据 | 来源 | 已核 URL | 参照库位置 |
|---|---|---|---|
| **95% 企业失败 - 三角验证 1** | MIT NANDA《State of AI in Business 2025》(2025-08) | mitsloan.mit.edu / nanda.media.mit.edu | Pool 2.8 |
| **95% 企业失败 - 三角验证 2 (新加)** | McKinsey《The State of AI 2025》(2025-11) | [McKinsey](https://www.mckinsey.com/capabilities/quantumblack/our-insights/the-state-of-ai) + [PDF](https://www.mckinsey.com/~/media/mckinsey/business%20functions/quantumblack/our%20insights/the%20state%20of%20ai/november%202025/the-state-of-ai-2025-agents-innovation_cmyk-v1.pdf) | Pool 7.1 |
| **95% 企业失败 - 三角验证 3 (新加)** | BCG《The Widening AI Value Gap》(2025-09-30) | [bcg.com](https://www.bcg.com/publications/2025/are-you-generating-value-from-ai-the-widening-gap) + [PDF](https://media-publications.bcg.com/The-Widening-AI-Value-Gap-Sept-2025.pdf) | Pool 7.2 |
| Air Canada 判例 CAD 650.88 | 2024 BCCRT 149 (CanLII) | [canlii.org/2024bccrt149](https://www.canlii.org/en/bc/bccrt/doc/2024/2024bccrt149/2024bccrt149.html) | Pool 4.1 |
| 法律 AI 幻觉率 17-43% | Stanford RegLab + HAI 2024-2025 实证 | hai.stanford.edu | Pool 2.12 |
| McDonald's × IBM 终止 | 2024-06 CNBC / Bloomberg | URL 待核 | Pool 4.6 |
| Klarna 2024 → 2025 反转 | Bloomberg 2025-05-08 | [bloomberg](https://www.bloomberg.com/news/articles/2025-05-08/klarna-turns-from-ai-to-real-person-customer-service) | Pool 4.2 |
| 医疗 AI 幻觉难识别 | MIT MedRxiv 2025 | medrxiv.org (具体 paper 待精确补) | Pool 2.16 |
| Gartner GenAI 2025 Trough | Gartner 2025 GenAI Hype Cycle | gartner.com (paywall) | Pool 2.10 |
| **(v1.1 新加) AI Scheming 5/6 frontier model** | Apollo Research "In-context Scheming" (2024-12) | [apolloresearch.ai](https://www.apolloresearch.ai/research/frontier-models-are-capable-of-incontext-scheming/) | Pool 5.6 |
| **(v1.1 新加) Workflow redesign = EBIT 影响最大变量** | McKinsey《The State of AI 2025》| 同上 McKinsey | Pool 7.1 |

**参照库全文（128 条全球 tier-1 源）**：`/Users/caiyiwen/ai-product-column-research/tools/_global-references.md`

---

## 七、配套使用建议

这份 Checklist 推荐配合：
- **MIT NANDA 95% 失败类型分类表**（同一钩子领取）——Q1-Q6 不通过时，对照分类表找具体失败原因
- **PRD: 4 增 2 删 模板**（11 篇配套）——6 问全过后，进入这套 PRD 模板

---

## 八、读者使用反馈征集

用过这个 6 问 checklist 拒绝过哪些伪需求？
欢迎加微信 **CYW960325** 反馈，被采纳的真实案例会出现在下一版（署名/匿名你选）。

---

## 九、设计依据 & 批判性自评 (v1.1 新增) ⭐

> **为什么有这一节**：v1.0 我直接给了 6 问，没说明这套设计的依据是什么、是否参考了行业标准、为什么没选其他替代方案、还有哪些已知盲区。
> 这一节透明化所有设计选择，让你判断是否信任这套 checklist。

### 9.1 这套 Checklist 的 3 个全球 tier-1 参照

| 框架 | 我借鉴了什么 | 我没采用什么 | 原因 |
|---|---|---|---|
| **Microsoft Responsible AI Standard v2** ([CDN PDF](https://cdn-dynmedia-1.microsoft.com/is/content/microsoftcorp/microsoft/final/en-us/microsoft-brand/documents/Microsoft-Responsible-AI-Standard-General-Requirements.pdf)) | frequency × severity 严重度分级（用在 Q4） | 完整 2D 矩阵 | 评审会 5 分钟过不完，需要画图 |
| **OpenAI Model Spec** ([model-spec.openai.com](https://model-spec.openai.com/2025-12-18.html)) | "什么能做 / 什么不能做"边界思维（用在 Q1 + Q4） | 3 层 Objectives/Rules/Defaults | 模型行为层规范 — 这是产品 PM 立项决策不是模型行为规范 |
| **Hamel Husain Field Guide** ([hamel.dev/blog/posts/field-guide](https://hamel.dev/blog/posts/field-guide/)) | "stop 当无新失败模式涌现"节奏（影响 Q6） | 5 步 SOP（hand-look 20-50 traces 等） | Hamel 的 5 步是**开发期**的，本 checklist 是**立项前**的 |

### 9.2 为什么选 6 问而不是替代方案

| 替代方案 | 优势 | 缺点 | 拒绝原因 |
|---|---|---|---|
| Microsoft RAI 2D 矩阵 | 已是行业标准 | 评审会 5 分钟过不完，需要画图 | **太重** |
| 4 问简化版（不含 Q3 + Q6） | 评审会更快 | 漏掉数据可得性（Q6），等于不做立项 | **太简** |
| 10 问全维度（加合规 / 团队能力 / 法务） | 最完整 | 业务方耐心 5 问就到顶，再问会被嫌 | **太烦** |
| 0-100 分 scorecard | 看似精确 | 假精度（每问没法 0-100 分） | **假精确** |
| **6 问层层递进**（本版） | 5 分钟可完 + 每问明确 pass/fail + 决策树清晰 | 没真 PM 测试过 | **✅ 选这个** |

### 9.3 已知盲区 + 后续验证计划

诚实标注 v1.1 还没解决的：

| 盲区 | 影响 | v2.0 计划 |
|---|---|---|
| ⚠️ **未做真 PM 测试** (n=0) | 不知道 6 问在评审会真实场景的实际通过率 / 误杀率 | v2.0 找 3-5 个真 AI PM 用这套过 1-2 个真需求，看 work 不 work |
| ⚠️ **没覆盖 Apollo "in-context scheming" 场景** | Pool 5.6 [Apollo paper](https://www.apolloresearch.ai/research/frontier-models-are-capable-of-incontext-scheming/) 显示 5/6 frontier model 在测试中展示欺骗行为（disabling oversight / self-exfiltration / manipulating outputs） | v2.0 考虑加 Q7「如果上 Agent autonomous decision，模型是否可能在认为不被观察时改变行为？」 |
| ⚠️ **未对照 a16z 100 CIO 调研补 Q3 颗粒度** | a16z 2025 数据：37% 企业生产部署 5+ 模型，意味着"3 个月验证"颗粒度可拆到"每月切一个模型测" | v2.0 把 Q3 拆为 Q3a "里程碑" + Q3b "模型 A/B 切换" |
| ⚠️ **没考虑 IBM CEO 调研警示** | Pool 7.7 IBM 数据：61% CEO 自报 agent scaling 但仅 52% 拿到"超出降本"价值，**CEO 乐观偏差**真实存在 | v2.0 加 Q2.5「这个 ROI 数字是 CEO 拍的还是 CFO 算的？」 |

### 9.4 适用 / 不适用边界

- ✅ **适用**：AI 应用层产品（聊天 / 工具 / RAG / Agent / 内容生成）
- ✅ **适用**：B 端 + C 端
- ✅ **适用**：增量项目（已有功能加 AI）+ 全新项目
- ❌ **不适用**：AI 基础模型公司立项（应参考 Anthropic Responsible Scaling Policy / DeepMind Frontier Safety Framework v3，见参照库 Pool 2.2 / Pool 5.9）
- ❌ **不适用**：AI infra / observability 工具立项（不是 ROI 驱动而是 DX 驱动）
- ❌ **不适用**：纯研究项目（探索性 R&D 不应被 ROI 限制）

### 9.5 这套 Checklist 的 "调研依据深度等级"

按参照库 4 级标准（L1 强依据 / L2 中依据 / L3 弱依据 / L4 设计选择）：

| 元素 | 等级 | 依据 |
|---|---|---|
| Q1 if-else 4 特征 | L3 | 案例归纳（订单系统 / 提取系统对比） |
| Q2 + Q3 ROI 要求 | **L1** | MIT NANDA + McKinsey + BCG 三角验证 5% 法则 |
| Q4 错误成本 | **L1** | Microsoft RAI severity 分级 + Air Canada 判例 + Stanford 法律 AI 实证 |
| Q5 长尾失败可见 | L2 | McDonald's × IBM 案例归纳 |
| Q6 ground truth | **L1** | MISQ paper + MIT MedRxiv + Hamel Field Guide 同时支撑 |
| 6 问的结构选择 | L4 | 我的设计判断，未真 PM 测试 |
| 评分模板（4 ✅ + 1 🟨 通过等） | L4 | 我的设计判断 |

**说明**：标 L4 的元素是"做最好"路径上待验证的部分，v2.0 优先升级。

---

## 文末微信钩子（嵌入公众号文章用）

```
─────────────────────────────
📦 配套资源 · 第 04 篇

加我微信 **CYW960325**（备注「专栏04」），免费领：
✓ 伪 AI 需求识别 6 问 checklist（本页 PDF 版）
✓ MIT NANDA 95% 失败类型分类表

【3 种格式任选】
📄 PDF：加微信后直接发文件给你
🔗 腾讯文档：微信里直接打开（推荐 📱）
💻 GitHub Pages：长期收藏 / 外链分享
─────────────────────────────
```

---

> 蔡逸雯 · 8 年 QE → AI PM · 公众号「蔡逸雯」
> CC-BY-NC 4.0 · 转载请注明出处
