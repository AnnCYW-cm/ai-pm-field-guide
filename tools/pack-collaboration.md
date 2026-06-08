---
tool_id: P1-55-1
serves_essays: [23, 24]
status: ready-for-review
last_updated: 2026-05-21
deliverable_formats: [markdown, pdf-multi-page, notion-template, tencent-doc]
hours_actual: 0.75
version: v1.0
references_pools_used:
  - Pool 1.3 Cat Wu (Anthropic, Head of Product for Claude Code)
  - Pool 1.4 Mike Krieger (Anthropic CPO)
  - Pool 1.6 Aparna Chennapragada (Microsoft CPO)
  - Pool 1.8 Marty Cagan (SVPG)
  - Pool 2.1 OpenAI Model Spec
  - Pool 2.4 Microsoft Responsible AI Standard v2
  - Pool 2.9 a16z 100 CIO Survey 2025
  - Pool 4.1 Air Canada
  - Pool 4.2 Klarna 反转
  - Pool 4.6 McDonald's × IBM
  - Pool 6.1-6.10 风投视角
  - Pool 7.1 McKinsey "State of AI 2025" (2025-11)
  - Pool 7.2 BCG "Widening AI Value Gap" (2025-09)
  - Pool 7.7 IBM Institute "CEO AI Study 2025"
  - Pool 9.3 Stratechery 2026
  - Pool 9.4 Pragmatic Engineer "AI Tooling 2026"
validation_status: "v1.0 未做真 PM 协作场景测试；v2.0 计划 n=3-5 真 PM × 真工程师配对实测"
---

# AI PM 协作话术大全

> 服务于第 23 篇《和工程师的新协作语言》+ 第 24 篇《和老板的新对齐语言》配套
>
> **用法**：评审会、Eval 评审、上线 GO/NOGO、Bad Case 复盘、月度老板汇报——开会前 3 分钟翻一遍。

---

## 零、为什么有这份工具

> **2026 工程师视角硬数据 — Pragmatic Engineer "AI Tooling 2026" Survey**（n=数千开发者）：
> - **95% 工程师每周用 AI 工具**
> - **75% 工程师 ≥ 一半工作用 AI**
> - **55% 工程师 regularly 用 agent**
> - **Staff+ engineer 用 agent 比例 63.5%**
> - **Claude Code 8 个月内从 0 到 #1**（46% 选为"最爱"，Cursor 19%，Copilot 9%）
>
> 工程师早就不是"等 PM 给需求"的角色。**PM 如果还用「按钮跳转」语言对话——会被嫌弃**。

> **2026 老板视角硬数据 — McKinsey "State of AI 2025"**（2025-11）：
> - **仅 6% 组织属于 "AI high performers"**（EBIT 影响 ≥ 5%）
> - **39% 组织报告任何 EBIT 影响**
> - **AI high performers 比其他人 2.8 倍可能做 "fundamental workflow redesign"**（55% vs 20%）
> - **workflow redesign 是 EBIT 影响的最强单一相关变量**
>
> **PM 跟老板对齐的本质——不是降预期，是给老板一套「为什么我们能进 6%」的判断框架**。

---

# 模块 A · 4 场景 PM × 工程师协作话术

## 场景 1：需求评审会（让工程师理解非确定性 AI）

### 1.1 工程师陷阱

| 工程师说的话 | 真实潜台词 | 不会接的后果 |
|---|---|---|
| 「这个需求太模糊」 | "你没说输入输出 / 没说成功标准" | 排期推 1 周，当成"研究项目" |
| 「LLM 不保证输出格式」 | "你以为我能 100% 控制 LLM？" | 上线后 JSON 解析失败 |
| 「demo 1 天，生产 3 个月」 | "你看到的 demo ≠ 生产" | 老板期待 1 天上 |
| 「成本你算过吗」 | "你只考虑功能没算边际成本" | LLM 账单爆 10 倍 |
| 「这个边界 case 我没法覆盖」 | "得用 eval 跑 1000 条" | 通过率塌方 |

### 1.2 PM 模板话术（5 要素全的版本）

**❌ 旧版**：「能不能给我做一个智能助手」

**✅ 新版**：

> 「我要做一个营销文案生成器。我用 5 要素给你说清楚——
>
> **【输入约束】**：JSON `{产品名, 卖点[3], 目标受众}`。产品名 ≤ 50 字
>
> **【输出约束】**：3 条小红书风格文案，每条 ≤ 100 字 + 1 hashtag。返回 JSON。**format error 必须 < 0.5%**
>
> **【成功标准 / Eval】**：50 条 eval case（飞书链接），含 30 常规 + 10 corner + 10 adversarial。**通过率 ≥ 85% = 上线门槛**
>
> **【性能 / 成本】**：P99 ≤ 5 秒，单次成本 ≤ ¥0.3。**任一不达标 = NOGO**
>
> **【Bad case 分级】**：4 级——
> - L4 公关风险 → 必须 100% 拦截
> - L3 错误事实 → 必须 < 1%
> - L2 风格偏差 → 可接受 ≤ 10%
> - L1 格式微瑕 → 可接受 ≤ 20%
>
> 你判断技术可行性 + 排期。**我不关心 prompt 怎么写、用哪个模型——那是你的决策**。」

### 1.3 引用 tier-1 数据（让工程师服气）

| 引用 | 怎么用 |
|---|---|
| OpenAI 2025-04-29 全量回滚 GPT-4o | "OpenAI 这种体量都因为 sycophancy 翻车——他们自己说'行为问题没成为 blocking gate'。**eval 严一点是给自己的保险**" |
| Pragmatic Engineer 2026：55% engineer 用 agent / Staff+ 63.5% | "我知道你在用 Claude Code agent。我不管你怎么 prompt——我把**业务边界**写清楚" |
| MIT NANDA 95% 失败率 | "95% 失败的根因不是模型不行，是**业务标准没说清**。我把标准说清是为了进那 5%" |

### 1.4 不要做的 3 件事
1. **不要说"我看 ChatGPT 能做"**——demo ≠ 生产
2. **不要在评审会现场改 PRD**——工程师听到是"PRD 不稳定"
3. **不要说"按钮跳转 + 加个 AI"**——立刻判断"PM 没想清楚"

---

## 场景 2：Eval 结果分歧（数据 vs 经验）

### 2.1 工程师陷阱

| 工程师说 | 潜台词 | 后果 |
|---|---|---|
| 「通过率 92%，可以上线」 | "你别再拖" | 那 8% 全是核心场景 → 30% 用户受影响 |
| 「LLM 自己的局限」 | "我已经试了 3 个 prompt 都不行" | corner case 累积成主流 bad case |
| 「LLM judge 给 4.2 分」 | "我自评了，省时间" | judge 偏差 → 自欺欺人 |
| 「prod 流量占比小」 | "我看不出 head 还是 tail" | 高价值用户撞到投诉 |
| 「修了一个 prompt，95% 了」 | "我没跑 regression" | "修 A 坏 B" |

### 2.2 PM 模板话术（4 维度分布逼问）

**❌ 旧版**：「Eval 92%，可以上线了」

**✅ 新版**：

> 「92% 是均值——**我要看 4 个分布**：
>
> **分布 1：场景分布**——那 8% 集中在哪个细分场景？
> - 集中在 "B 端 SaaS 长卖点"（占 5%）→ **可灰度上线**
> - 集中在 "C 端美妆短卖点"（占 40%）→ **NOGO**
>
> **分布 2：严重度分布**——失败里 L3/L4 占比？
> - L3/L4 < 1% → 业务可承受
> - L3/L4 > 1% → 必须 fix
>
> **分布 3：用户分布**——哪些 user_id segment 撞到？
> - 新用户尝鲜 → 流失影响小
> - 付费用户 → 直接退款 + 公关
>
> **分布 4：regression 检查**——这次修复有没让历史 case 退化？
> - 历史 100 条 eval：**退化 > 5% = 修复失败，回滚**
>
> 4 个分布都过 → GO。任何一个不过 → 不是 92% 的问题，是分布的问题。」

### 2.3 LLM judge vs 人工 judge 分歧追问

> 「LLM judge 我同意用——**但 3 个校验**：
> 1. **judge prompt 抄业务标准？** 让我看一下
> 2. **judge 偏差校准过？** 抽 50 条 LLM vs 人工对比，**Pearson 相关 ≥ 0.7** 才能信
> 3. **judge 用的模型 ≠ 被评模型**——同模型自评分会虚高」

### 2.4 引用 tier-1 数据

| 引用 | 怎么用 |
|---|---|
| OpenAI 4-29 回滚 | "OpenAI 当时也是 eval 总分通过——但 sycophancy 维度没单独看分布" |
| Hamel Field Guide | "Hamel 说 eval 必须 hand-look 20-50 traces，不能只看 dashboard" |
| Stanford 法律 AI 17-43% 幻觉 | "号称 hallucination-free + RAG 的产品都有 17-43% 幻觉——**没分布数据的 92% 没意义**" |

---

## 场景 3：上线 GO-NOGO（PM 拒绝带 P0 风险上线）

### 3.1 工程师陷阱

| 工程师说 | 潜台词 | 后果 |
|---|---|---|
| 「老板催，我准备 ship」 | "PM 顶一下" | 带 P0 上线翻车 PM 背锅 |
| 「红队 eval 没跑但功能 eval 过了」 | "我赶时间" | 被恶意用户攻破 |
| 「成本超 50%，但功能完整」 | "我没法压成本" | LLM 账单爆 → 项目腰斩 |
| 「regression 退化 7%，都是边缘 case」 | "我不想花 3 天 fix" | 老用户感受变差 → NPS 跌 |

### 3.2 PM 模板话术（5 大类 eval 结构化 NOGO）

**❌ 旧版**：「老板催，今天上」

**✅ 新版**：

> 「对照 5 大类 pre-launch eval checklist：
>
> | 类别 | 状态 | 数据 | GO/NOGO |
> |---|---|---|---|
> | **类别 1：核心功能 eval** | ✅ | 通过率 92%，分布健康 | GO |
> | **类别 2：性能 eval** | ✅ | P50 1.2s / P99 4.8s | GO |
> | **类别 3：成本 eval** | ⚠️ | 单次 ¥0.45（超 50%） | 灰度 GO，需 CFO 签 |
> | **类别 4：对抗 / 红队** | ❌ | **未跑** | **NOGO** |
> | **类别 5：regression** | ❌ | **退化 7%（> 5% 阈值）** | **NOGO** |
>
> **结论：NOGO**。
>
> 我去跟老板沟通，给他看 3 个数据：
> 1. **OpenAI 4-29 全量回滚** — 行为问题没作为 blocking gate
> 2. **Air Canada CAD 650.88 判例** — chatbot 说的话就是公司说的话
> 3. **MIT NANDA / McKinsey / BCG 三家收敛在 5-6% 成功率**
>
> 老板会同意延 3 天。**我去顶**——你别撤 PR。」

### 3.3 跟老板的"延期话术"

> 「张总，延 3 天上线。**不是技术问题，是风险问题**——
> - 对抗 eval 还没跑——Air Canada 一个判例改变全球航司 chatbot 标准
> - regression 退化 7%——老用户会感受变差
> - OpenAI 4-29 全量回滚——他们这么大公司翻车一次都改了发版流程
>
> **3 天延期，换 0 风险上线**。」

### 3.4 引用 tier-1 数据

| 引用 | 怎么用 |
|---|---|
| OpenAI 4-29 全量回滚 | NOGO 决策的"权威背书" |
| Air Canada CAD 650.88 | "翻车的法律代价"——比技术辩解更有说服力 |
| McKinsey 6% high performer + workflow redesign 最强相关 | "我们要进 6%——不能赶时间砸自己" |
| BCG 5% future-built | 三角验证 5% 上限 |

---

## 场景 4：Bad Case 紧急处理

### 4.1 工程师陷阱

| 工程师说 | 潜台词 | 后果 |
|---|---|---|
| 「改一下 prompt 就好」 | "PM 别管细节" | "修 A 坏 B" 其他场景退化 |
| 「LLM 自己的局限」 | "我累了，我想搪塞" | 同类反复出现 |
| 「占比小，下周修」 | "我手头一堆事" | L4 被错判为低优 → 公关炸 |
| 「加个关键词过滤」 | "我用规则把这条拦了" | 漏拦相似 case 反复来 |

### 4.2 PM 模板话术（5 类 bad case 归类版）

**❌ 旧版**：「赶紧改 prompt 修复」

**✅ 新版**：

> **第一步：归类（30 秒判断）**
>
> | 类型 | 现象 | 修哪一层 |
> |---|---|---|
> | hallucination | 编造事实 | **加 RAG grounding**（不是改 prompt） |
> | refusal | 该答不答 | 调 safety filter / system prompt 边界 |
> | format error | JSON 解析失败 | structured output / JSON schema 校验 |
> | off-topic | 跑题 | 改 system prompt 边界 + input classifier |
> | safety violation | 违规内容 | 加 content filter + input/output moderation |
>
> **第二步：评估严重度**
> - L4 公关风险 → **立刻触发降级到规则**，不等修
> - L3 错误事实 → 4 小时内 hotfix
> - L2 风格偏差 → 当天修 + regression
> - L1 格式微瑕 → 下周迭代
>
> **第三步：修复后强制 regression**
> - 跑历史 100 条 eval
> - **退化 > 5% = 修复失败，回滚**
>
> 这个 case 归 hallucination（编造卖点）——L3——路径：**加 RAG grounding + 4 小时内修 + regression**。**不要改 system prompt**——会影响其他场景。」

### 4.3 L4 紧急降级话术（PM 必须 5 分钟内说）

> 「L4 bad case 触发——执行降级 SOP：
> 1. **立刻切到规则兜底**（不是修，是绕开）
> 2. **保留完整 trace + screenshot + user_id**
> 3. **5 分钟内通知 CEO + 法务 + 公关**
> 4. **24 小时内出复盘**——5W1H + 根因 + 修复 + regression
> 5. **修复后 shadow eval 24 小时**才能放回流量
>
> 工程师专心修。我去对外。」

### 4.4 引用 tier-1 数据

| 引用 | 怎么用 |
|---|---|
| Air Canada CAD 650.88 | L4 hallucination 不及时降级的代价 |
| McDonald's × IBM 终止 | "85% = 100% 翻车"——长尾失败 TikTok 化 |
| Klarna 反转（2024-02 → 2025-05） | bad case 累积到一年就反转 |
| Apollo Research "in-context scheming" | "5/6 frontier model 测试中欺骗"——L4 不能仅靠 prompt 修 |

---

# 模块 B · PM 5 字段 trace 速查表

> **为什么 5 字段不是 50**：Cat Wu 核心方法论 "**Sentiment loop > Dashboard**"——PM 看 trace 不是读懂技术日志，是训练"业务 vs AI 输出"对齐感。5 字段是 PM 视角最小可行集。

## 5 字段速查表

| 字段 | 怎么读 | 异常信号 | 处置建议 |
|---|---|---|---|
| **`input`** | ① 是否真实业务场景 ② 长度/格式/语言符合预期 ③ 是否恶意 injection | 单词/emoji（试探）/ 超长 / 含 "ignore previous instructions" / 小语种 | • 异常 > 5% → 加 input classifier<br>• prompt injection → 加防御 + content filter<br>• 小语种 → 评估是否支持 |
| **`output`** | ① 准确性 ② 完整性 ③ 格式 | hallucination / refusal / format error / off-topic / safety violation | 5 类 bad case 归类 → 修哪一层 |
| **`latency`** | ① 首 token TTFT ② 总耗时 ③ P50/P95/P99 | P99 > 用户耐心（C 端 ≤ 5s / B 端 ≤ 15s）/ 首 token > 2s / 同 input 波动 > 3x | • 加 streaming<br>• 加 caching<br>• cascade 简单分支用小模型 |
| **`cost`** | ① 单次成本 ② 单用户单日累计 ③ ARR 比例（vs a16z 基线）| 单次 > 业务上限 / 单用户单日 > ¥10（脚本攻击） / 月成本/ARR > 行业基线 | • per-user hard cap<br>• cascade<br>• prompt caching<br>• 长度优化 |
| **`user_id`** | ① 新用户还是老用户 ② 付费还是免费 ③ 同 ID 是否反复撞同类 | 付费用户撞 L3/L4 / 新用户首次撞 / 同 ID 24h 撞 3+ 次 | • 付费撞 → 退款 + PM 跟进<br>• 新用户撞 → A/B 测 onboarding<br>• 反复撞 → 主动联系 |

## 加分项 3 个（PM 进阶看）

| 字段 | 看什么 |
|---|---|
| `system_prompt` | 当前生效的 prompt 全文（工程师的活） |
| `model` | 用的什么模型（工程师选型，PM 看了也不能改） |
| `retrieval` | RAG 检索到了哪些文档 |

## PM 看 trace 的「30 秒判断法」

每条 trace 看完 30 秒内回答 3 问：
1. **结果用户满意吗？**（0-5 分主观打分）
2. **不满意——哪一类 bad case？**（5 类归类）
3. **孤立 case 还是同类反复？**（找 trend）

凑够 20-30 条同类 → 找工程师讨论修复方向。

## 看 trace 频率约定

| 时机 | PM 密度 | 工程师密度 |
|---|---|---|
| 上线前 1 周 | 每天 50 条 | 每天 100 条 |
| 上线灰度 | 每天 20-30 条 | 每天 50-100 条 |
| 上线稳定 | 每天 10-20 条 | 报警驱动 |
| Bad case 紧急 | 立刻全量看 | 立刻看技术栈相关 |

---

# 模块 C · PM vs 工程师实验边界表 + 半懂自查

## C.1 实验边界总表

**核心原则**：PM 跑**业务相关 + Claude Code prototype**；工程师跑**技术实现 + 批量 eval + prompt 工程**。边界划清——**协作摩擦 80% → 20%**。

### 立项 / 评审阶段
| 实验 | PM | 工程师 | 一起 |
|---|---|---|---|
| 评估"能不能做" | ✅（Claude Code 跑 prototype）| | |
| 写 PRD / spec | ✅ | | |
| 估排期 / 工作量 | | ✅ | |
| 选模型 / 架构 | | ✅ | |

### Eval 设计阶段
| 实验 | PM | 工程师 | 一起 |
|---|---|---|---|
| 写 eval case（业务标准） | ✅ | | |
| 写 LLM judge prompt | | | ✅（PM 出标准，工程师写） |
| 跑 batch eval | | ✅ | |
| 校准 LLM judge vs 人工 | | | ✅ |
| 看 eval 分布 | ✅（业务视角） | ✅（技术视角） | |

### Prompt / 模型工程
| 实验 | PM | 工程师 | 一起 |
|---|---|---|---|
| 写 system prompt | | ✅ | |
| 调参数 | | ✅ | |
| 模型 A/B | | ✅ | |
| Fine-tune | | ✅ | |
| RAG 调优 | | ✅ | |
| Agent 工具配置 | | | ✅（PM 出工具清单，工程师配实现） |

### 上线阶段
| 实验 | PM | 工程师 | 一起 |
|---|---|---|---|
| Pre-launch eval（类别 1 + 4 业务部分） | ✅ | | |
| Pre-launch eval（类别 2/3/5） | | ✅ | |
| 灰度决策（业务影响） | ✅ | | |
| 灰度技术配置 | | ✅ | |
| Shadow eval | | ✅ | |
| 红队测试 | | | ✅（PM 出红线，工程师写脚本） |

### 上线后运营
| 实验 | PM | 工程师 | 一起 |
|---|---|---|---|
| 看 trace（业务角度，5 字段） | ✅ | | |
| 看 trace（技术，调 prompt） | | ✅ | |
| Bad case 归类（5 类） | | | ✅ |
| Bad case 修复（哪一层） | | ✅ | |
| L4 紧急降级决策 | ✅ | | |
| 降级技术执行 | | ✅ | |
| 月度成本给 CFO 算账 | ✅ | | |
| 成本技术优化 | | ✅ | |
| 老板汇报 | ✅ | | |

## C.2 PM 半懂自查（防"半懂 = 自信瞎指挥"事故）

**核心命题**："**全不懂**"工程师会兜底。"**半懂**" PM 自信瞎指挥——最危险。

### 自查 1：看到 demo 时
- [ ] 我看到的是 demo 还是生产？（demo 可能 cherry-picked）
- [ ] 这个 demo 背后用了什么 infra？（RAG / tool use / reasoning / agent）
- [ ] 我们公司有这些 infra 吗？没有要建多久？
- [ ] 这个 demo 在长尾 case 表现怎样？

**事故警示**：第 23 篇事故 1——"PM 看 ChatGPT 能做要求自己产品也能做，3 周后被迫推翻重做"

### 自查 2：想说"改 prompt"时
- [ ] 我归类了吗？是 hallucination / refusal / format / off-topic / safety 哪一类？
- [ ] 修 prompt 是这一类的正确修法？（hallucination 应该加 RAG）
- [ ] 我做了 regression 计划吗？
- [ ] 工程师说"改了会影响其他场景"——我问了"影响哪些"吗？

**事故警示**：第 23 篇事故 2——"PM 半懂 prompt 是'指令'，不懂 prompt 是'系统级配置'，强行改 prompt 后 5 个场景退化"

### 自查 3：看到通过率时
- [ ] 只看到均值还是分布？
- [ ] 失败 case 集中在哪个场景？占总流量多少？
- [ ] L1-L4 严重度分布？
- [ ] 哪些 user_id segment 撞到？
- [ ] regression 跑了吗？退化率多少？

**事故警示**：第 23 篇事故 3——"PM 看 95% 通过率上线，结果那 5% 全是核心 case 影响 30% 用户"

### 自查 4：说"我看竞品做到了"时
- [ ] 竞品做的是 demo 还是生产？
- [ ] 竞品真实指标（通过率 / 成本 / 延迟）我知道吗？
- [ ] 竞品背后团队规模 / 训练数据 / infra 我们有吗？
- [ ] 这个能力对我们的业务真的有 ROI 吗？还是 FOMO？

### 自查 5：被工程师说"做不到"时
- [ ] 具体原因是什么？（基础模型局限 / infra 缺 / 时间不够 / 不值得做）
- [ ] 是技术硬限制还是 trade-off？
- [ ] 如果 trade-off，能接受降级方案吗？
- [ ] 我有没有跟工程师一起做 FMEA？

## C.3 PM 必须懂 vs 不需要懂

| 必须懂 | 不需要懂 |
|---|---|
| 4 个高频场景话术 | Prompt 具体写法 |
| 5 字段 trace + 30 秒判断 | Eval 框架代码实现 |
| Bad case 5 类归类 | 模型训练原理 |
| 4 级严重度 | RAG 向量检索算法 |
| 4 类降级策略 | 模型推理优化 |
| Pre-launch 5 大类 eval | LLM attention 机制 |
| 5 数字老板汇报 | Tokenizer 实现 |
| 行业基线（McKinsey 6% / a16z $4.5M-$7M / Pragmatic Engineer 95%） | 各家模型 benchmark 细节 |

**核心**：懂"协作场景需要的概念"，不需要懂"工程实现的细节"。**懂概念是为了能说对话；懂细节是越界**。

---

# 模块 D · 3 焦虑识别 + 4 套对齐话术 + 5 数月报

## D.1 老板 3 焦虑识别

### 焦虑 1：FOMO（怕错过）

**典型表现**：
- [ ] 早会经常说"竞品都在做 AI"
- [ ] 转发"AI 颠覆 XXX 行业"文章
- [ ] 问"要不要做大模型 / 自研模型"
- [ ] 对 demo 兴奋度 > ROI 数据
- [ ] 要求"3 个月内必须有 AI 标签产品上线"

**真正担心**：被时代抛下、估值跟不上。
**误诊代价**：PM 误诊为 ROI → 算账 → 老板觉得"格局小"。

### 焦虑 2：ROI 焦虑

**典型表现**：
- [ ] 每月看 LLM 账单问"为什么这么贵"
- [ ] 问"投了 3 个月，ROI 在哪"
- [ ] 要求"换便宜模型 / DeepSeek / 开源"
- [ ] 对成本敏感 > 功能数据
- [ ] 问"每 active user 的边际成本"

**真正担心**：财务责任、董事会汇报、现金流。
**误诊代价**：PM 误诊为 FOMO → 讲战略 → 老板觉得"财务感差"。

### 焦虑 3：失控焦虑

**典型表现**：
- [ ] 问"AI 答错了怎么办"
- [ ] 提到"会不会成下一个 Air Canada"
- [ ] 要求"能不能审核 AI 每个输出"
- [ ] 对公关 / 法律风险敏感升高
- [ ] 要求"AI 上线前法务必须签字"

**真正担心**：公关风险、法律责任、品牌伤害。
**误诊代价**：PM 不重视控制 → L4 翻车老板炸。

### 三焦虑复合识别

| 老板说 | 主导焦虑 |
|---|---|
| "竞品都做 Agent 了，我们 ROI 怎样" | FOMO（ROI 是借口） |
| "ROI 没看到，能换便宜模型吗" | ROI |
| "Air Canada 那判例，我们会不会出事" | 失控 |
| "竞品做了 Agent，翻车怎么办" | FOMO + 失控（FOMO 主导） |
| "投了这么多钱，翻车了董事会怎么交代" | 失控 + ROI（失控主导） |

**核心**：听老板"先说什么"判断主导——人会先说最担心的。

## D.2 4 套对齐话术

### 话术 1：引用全球 tier-1 数据（对 FOMO + ROI）

> 「张总，3 个 2025 最新数据——
>
> **McKinsey《State of AI 2025》(2025-11)**：
> - 仅 **6% 是 "AI high performers"**（EBIT ≥ 5%）
> - **39% 报告任何 EBIT 影响**——其余 61% 说 AI 没带来财务影响
> - **AI high performers 比其他人 2.8 倍可能做 workflow redesign**（55% vs 20%）
> - **workflow redesign 是 EBIT 最强单一相关变量**
>
> **a16z 100 CIO 调研（2025）**：
> - 企业 LLM 年均 **$4.5M → $7M**（+56%）
> - **37% 企业同时跑 5+ 模型**
>
> **Pragmatic Engineer 2026 AI Tooling 调研**：
> - **95% engineer 每周用 AI**
> - **75% engineer ≥ 一半工作用 AI**
> - **Claude Code 8 个月从 0 到 #1**
>
> 三个数据 3 件事：
> 1. AI 过了 hype 期——95% engineer 在用，不用就是落后（破 FOMO）
> 2. 但 ROI 兑现率只有 6%——盲目花钱进不了 6%（破"烧钱就有效"）
> 3. 进入 6% 关键不是模型多牛，是 **workflow redesign**——这是我们要做的
>
> 我们做的就是 workflow redesign——给你 demo。」

### 话术 2：引用真实案例（对失控 + ROI）

> 「张总，AI 翻车 / 反转 3 笔账——
>
> **案例 1：Air Canada CAD 650.88（2024 BCCRT 149）**
> - chatbot 编造丧亲票政策
> - BC 仲裁庭判赔 CAD 650.88（约 ¥3400）
> - 钱不是关键——**判例**：「chatbot 不是独立法律实体，bot 说的话就是公司说的话」
>
> **案例 2：Klarna 反转（2024-02 → 2025-05）**
> - 2024-02 AI 替代 700 客服，估值狂涨
> - 2025-05 承认"AI 缺乏共情"重新招人
> - 一年内反转，CEO 公开道歉
>
> **案例 3：McDonald's × IBM 终止（2021-2024.06）**
> - 100+ 门店试点 2 年
> - **85% 准确率 + 1/5 单需人工**——快餐场景 = 100% 翻车
> - 每个错都被拍 TikTok
>
> 我们怎么避免？**做了产品 RAI 矩阵 [展示]**——按"频率 × 严重度"评估每个 AI 能力。
> 我们按矩阵做产品设计——**翻车风险压在可承受范围**。」

### 话术 3：引用咨询机构三角验证（对所有焦虑）

> 「张总，AI 项目成功率的三角验证——
>
> | 机构 | 时间 | 结论 |
> |---|---|---|
> | **MIT NANDA** | 2025-08 | 95% 企业 GenAI 零回报 |
> | **McKinsey** | 2025-11 | 仅 6% "AI high performers" |
> | **BCG** | 2025-09 | 仅 5% "future-built" |
>
> **三家机构、独立调研、口径不同——结论收敛 5-6%**。
>
> **进入 6% 的路径**（McKinsey）：
> 1. Fundamental workflow redesign
> 2. 从 CEO 开始 owning
> 3. 持续投入而非一次性交付
> 4. eval + redesign 双轮驱动
>
> 我们对照——
> - ✅ workflow redesign：重新设计了 [X 流程]
> - ✅ CEO owning：你每月看 5 数月报
> - ✅ 持续投入：第二季度预算 ¥X
> - ✅ eval + redesign：5 大类 pre-launch eval + 月度 redesign 复盘
>
> 我们的成功率上限不是 6%——比 6% 高，因为我们做了正确的事。」

### 话术 4：引用顶级技术 podcast / blog（对 FOMO）

> 「张总，引几个你也读的源——
>
> **Stratechery (Ben Thompson) 2026**：
> - "Agents Over Bubbles"——AI 不是 bubble，agent 是真正 inflection
> - 3 inflection：**ChatGPT moment → o1 moment → Opus 4.5 moment（agent triggered by agent）**
> - "Microsoft and Software Survival"——Copilot 15M paying customers，但只是 M365 小部分——**per-seat licensing 被 agent 打破**
>
> **Pragmatic Engineer 2026 AI Tooling**：
> - **75% engineer ≥ 一半工作用 AI**——这不是 hype 是现实
> - Staff+ 63.5% 用 agent——越资深越用
> - 大公司 Copilot 56% / 小公司 Claude Code 75%
>
> **结论**：
> 1. AI 不是 bubble，agent 是真 inflection——**不上船会落后**
> 2. 但 inflection 的赢家不是最早跳的——**是 workflow 改造最深的**
> 3. 我们公司的节奏对的——**做 agent 之前先把 prompt + eval + 5 字段监控做扎实**
>
> 我每周给你转 Stratechery / Pragmatic Engineer 的 3 句话精华版。这样我们用同一套信息源对齐战略。」

## D.3 5 数月报模板

```
─────────────────────────────
[产品名] AI 月报 · YYYY-MM
─────────────────────────────

📊 5 数字（vs 上月 / vs 行业基线）

1️⃣ MAU
   X 万（vs 上月 +Y% / vs 行业 [+/-]）
   
2️⃣ 月度 LLM 成本 / ARR
   X%（vs 上月 / vs a16z 基线 [偏低/中/偏高]）
   
3️⃣ Bad Case 率（按 4 级）
   L4 公关：N 次（必须 = 0）
   L3 错误事实：X%（目标 < 1%）
   L2 风格偏差：X%（目标 < 10%）
   L1 格式微瑕：X%（目标 < 20%）
   
4️⃣ Eval 通过率
   核心 eval：X%（目标 > 85%）
   对抗 eval：X%（目标 > 95%）
   regression：退化 X%（必须 < 5%）
   
5️⃣ 用户满意度
   NPS：X 分
   付费留存：X%

🎯 本月解读（1 句）

📅 下月规划（1 句）

⚠️ 风险预警（如有）

🔬 业内对标（季度更新）
[例子：根据 McKinsey 2025-11，AI high performers EBIT ≥ 5%。
我们目前业务影响 [X%]，对标 [接近/进入] 该区间。]
─────────────────────────────
```

**5 个数字的依据**：

| 数字 | 对应焦虑 | 引用基线 |
|---|---|---|
| MAU | FOMO | "竞品 MAU / 我们 MAU" |
| 月成本/ARR | ROI | a16z 100 CIO $4.5M-$7M |
| Bad Case 4 级 | 失控 | Microsoft RAI v2 |
| Eval 通过率 | 全部 | OpenAI 4-29 回滚 → 5 大类 |
| 用户满意度 | FOMO + ROI | Cat Wu "sentiment loop" |

**关键**：5 个数字 + 行业基线 = 让老板**自己判断**位置——不是 PM 告诉老板"我们做得好"。

## D.4 老板 7 高频问题 + 标准答案

| 老板问 | PM 答（升级版） |
|---|---|
| 「什么时候上线」 | 「灰度 [日期]，全量 [日期]。5 大类 eval 全过才放量——任一不达标 NOGO」 |
| 「竞品做到了，我们能做到吗」 | 「竞品 demo 还是生产？demo 距生产差 10 倍——下周给你对标报告」 |
| 「ROI 怎么算」 | 「短期：[X]；中期：[Y]；长期：[Z]。McKinsey 6% EBIT ≥ 5%——我们对照走」 |
| 「成本能降吗」 | 「可以。3 路径：cascade / prompt caching / 长度优化。预计降 30-50%」 |
| 「翻车了怎么办」 | 「4 级 bad case 分级 + 4 种降级 + 5 分钟回滚 SOP。Air Canada 我们做了 RAI 矩阵」 |
| 「要不要做 Agent」 | 「3 件事先做：5 字段 trace + 5 类 bad case 归类 + 4 级降级 SOP。Pragmatic Engineer Staff+ 63.5% 用 agent，但 setup 没做好就上 = 灾难」 |
| 「要不要自研模型」 | 「不要。Anthropic Research 占 1/3 多在做模型层——这是 Anthropic 的活。我们是应用层，资源放 workflow redesign + 监控 + eval」 |

---

# 模块 E · 设计依据 & 批判性自评

## E.1 6 个 tier-1 参照

| 参照 | 借鉴 | 没采用 | 原因 |
|---|---|---|---|
| Cat Wu Product Note | "Prototypes over PRDs" / "Sentiment loop > Dashboard" | 完整 Anthropic 流程 | 在 to-B/to-C 公司用不动 |
| Mike Krieger | "PM 必须自己跑 Claude Code prototype" | Krieger 对产品组织全套观点 | 组织议题留给第 25 篇 |
| Aparna Chennapragada | "AI at Work" + per-seat 被 agent 打破 | Microsoft 内部组织 | 不公开 |
| Marty Cagan Empowered Teams | "PM 不是 ticket taker" | 完整 Empowered Teams 框架 | 太重 |
| Microsoft RAI v2 | "频率 × 严重度" 2D 矩阵 | 完整 RAI 流程 | 评审会画完整矩阵太烦 |
| OpenAI Model Spec | "做 / 不做"边界思维 | 3 层 Objectives/Rules/Defaults | 协作话术不是模型规范 |

## E.2 替代方案对比

| 替代 | 优势 | 缺点 | 拒绝原因 |
|---|---|---|---|
| 完整 RAI 流程文档 | 工业标准 | 评审会 5 分钟过不完 | **太重** |
| 单一"30 个万能话术" | 评审会快 | 工程师一听就识别"模板话"反感 | **机械** |
| Hard-coded PRD 模板 | 标准化 | 不灵活 | **不通用** |
| 心法（无具体话术） | 灵活 | PM 没经验用不出来 | **空** |
| **场景化话术 + 引用数据 + 半懂自查**（本版） | 工程师服气 + 防半懂事故 | 未做真协作场景测试 | **✅ 选这个** |

## E.3 已知盲区

| 盲区 | 影响 | v2.0 计划 |
|---|---|---|
| ⚠️ 未做真 PM × 真工程师协作测试 | 不知道 4 场景话术的"被接受率" | n=3-5 真 PM 跑 1-2 个真场景 |
| ⚠️ 未做真 PM × 真老板对齐测试 | 不知道 4 套对齐话术老板真听不听 | n=2-3 真 CEO 听 PM 用 |
| ⚠️ 场景覆盖不全 | 漏 corner case（工程师跑路 / PM 多项目分配 / AI 跟非 AI 优先级冲突） | v2.0 扩到 6-8 场景 |
| ⚠️ 没考虑跨规模差异 | 大公司 Copilot 56% / 小公司 Claude Code 75%——节奏不同 | v2.0 拆"创业公司版 vs 大厂版" |
| ⚠️ 没区分 AI 应用层 vs 基础模型层 PM | Anthropic / OpenAI 的 PM 跟应用层 PM 协作语言不同 | 默认应用层，v2.0 加基础模型层附录 |

## E.4 适用 / 不适用边界

- ✅ AI 应用层 PM × 工程师协作（聊天 / 工具 / RAG / Agent）
- ✅ B 端 + C 端
- ✅ 创业公司（5-50 人）+ 中型公司（50-500 人）
- ⚠️ 大厂（10K+）—— 话术只适用 1-1，不适用跨部门
- ❌ AI 基础模型公司 PM
- ❌ AI infra / observability 工具 PM
- ❌ 纯研究型团队

## E.5 调研依据深度等级

| 元素 | 等级 | 依据 |
|---|---|---|
| 场景 1 评审会 5 要素 | L2 | OpenAI Model Spec + Cagan 案例归纳 |
| 场景 2 4 维度分布逼问 | **L1** | Hamel Field Guide + Stanford 17-43% 实证 |
| 场景 3 5 大类 eval NOGO | **L1** | OpenAI 4-29 回滚 + Microsoft RAI v2 |
| 场景 4 5 类 bad case 归类 | **L1** | Air Canada + McDonald's + Klarna |
| 模块 B 5 字段 trace | **L1** | Cat Wu sentiment loop + Hamel hand-look |
| 模块 C 实验边界表 | L2 | Cat Wu + Krieger + Cagan 归纳 |
| 模块 C 半懂自查 5 条 | L3 | 设计判断（基于第 23 篇事故 1-3） |
| 模块 D 3 焦虑识别 | L2 | 实战归纳 + Stratechery 老板信息源 |
| 模块 D 话术 1（3 数据） | **L1** | McKinsey + a16z + Pragmatic Engineer 三独立 |
| 模块 D 话术 2（3 案例） | **L1** | Air Canada + Klarna + McDonald's |
| 模块 D 话术 3（三角验证） | **L1** | MIT NANDA + McKinsey + BCG |
| 模块 D 话术 4（Stratechery + Pragmatic Engineer） | **L1** | 2026 一手 |
| 模块 D 5 数月报模板 | L4 | 设计判断 + Cat Wu sentiment loop |

## E.6 反共识金句

- **"半懂比不懂更危险——不懂工程师会兜底，半懂 PM 自信瞎指挥"**
- **"PM 不需要会写 prompt——但必须在 4 个高频协作场景里说对话"**
- **"老板不缺预期管理，老板缺判断框架"**
- **"AI 时代的 PM 核心能力不是会用 AI——是知道 AI 在哪里做不到"**
- **"对齐 ≠ 妥协——对齐是用行业标准让老板自己看懂不确定性"**
- **"95% engineer 每周用 AI（Pragmatic Engineer 2026）——还在用'按钮跳转'对话的 PM 已经被工程师拉黑"**
- **"6% 进入 EBIT high performer 的关键不是模型多牛——是 workflow redesign（McKinsey 2025-11）"**

---

## 文末微信钩子

```
─────────────────────────────
📦 配套资源 · 第 23 + 24 篇 合订

加我微信 **CYW960325**（备注「专栏23-24」），免费领：
✓ 4 场景 PM × 工程师协作话术
✓ PM 5 字段 trace 速查
✓ PM vs 工程师实验边界表
✓ 3 焦虑识别 + 4 套对齐话术
✓ 5 数月报模板

【3 种格式任选】
📄 PDF / 🔗 腾讯文档 / 💻 GitHub Pages
─────────────────────────────
```

---

> 蔡逸雯 · 8 年 QE → AI PM · 公众号「蔡逸雯」
> CC-BY-NC 4.0 · 转载请注明出处
