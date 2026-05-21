# 20 · AI 产品的监控指标体系——传统 Funnel 之外要看什么

> 第一季《AI 时代 PM 工作流重构》· 第 20 篇 · 第五部分 运营
> 预估字数：5000

---

第十九个"不以为然"——

**90% 的 PM 监控 AI 产品还看传统 funnel**。

不是 PM 不会看指标。是大多数 PM **以为"AI 产品和传统产品都看 DAU / 留存 / 转化"**——结果上线一周指标全绿，第 8 天用户口碑崩——**因为 4 类 AI 特有指标一个都没监控**。

读完这一篇你会知道——**AI 产品的监控除了传统 funnel，必须看 4 类 AI 特有指标**。

---

## 上半篇 · workflow

### 4 类 AI 特有指标

#### 指标 1：质量分布（不是平均分，是分布）

**为什么不能看平均分**？

举个例子。客服 AI 整体满意度 4.2/5——看起来不错。
但拆分布看：
- 30% 用户给 5 分
- 40% 用户给 4 分
- 20% 用户给 3 分
- **10% 用户给 1 分**

那 10% 1 分的用户**会去骂你**。平均分掩盖了这群人。

**怎么监控**：
- 不要监控均值
- 监控分布（用 histogram）
- 重点看"低分尾部"占比

**业内最佳实践**：
- **Datadog LLM Observability** 拆成 factuality / toxicity / relevance 三个分布维度
- **Braintrust** 主打 "eval-driven development with CI/CD gates"，把质量分布嵌入到发布门槛

#### 指标 2：Bad case 比例

**怎么分类计数**：

按失败模式分类（不要合并成一个"错误率"）：
- hallucination（幻觉）：X%
- refusal（拒答）：X%
- format error（格式错误）：X%
- off-topic（偏题）：X%
- safety violation（安全违规）：X%

**Arize 的标准做法**：把 bad case 切成 4-5 类分别打标签计数。

为什么不合并？因为每类失败的修复路径不同：
- hallucination → 改 RAG / 加 grounding
- refusal → 改 prompt / 调 safety filter
- format error → 改 structured output
- off-topic → 改 system prompt 边界
- safety violation → 加 content filter

**合并成一个"错误率"等于丢失诊断信息**。

#### 指标 3：降级触发率

**为什么要监控**：你设计的降级路径（第 14 篇 Bad Case 分级章节）真的被触发了多少次？

健康范围：
- 第 2 级（需告警）：每天 < 10 次
- 第 3 级（需阻断）：每天 < 5 次
- 第 4 级（灾难级）：**每月 < 1 次**

异常情况：
- 第 3 级触发率突然 > 50/天 → 模型可能在退化
- 第 4 级触发率 > 0 → 立刻 postmortem

**Helicone 的做法**：一行 proxy 接入后，原生暴露 "rate-limited / rerouted / fallback to another provider" 三类降级请求标记，可单独看占比。

#### 指标 4：Cost-per-active-user

**为什么要监控**：详见第 9 / 15 篇。

- 单用户月成本（最重要的财务指标）
- 头部 1% 用户消费占比
- 月度 LLM 成本占 ARR

**a16z 2025 企业调研**：企业 LLM 年均花费已从 $4.5M 涨到 $7M——**CFO 开始要求每个 active user 的边际成本可解释**。

**Traceloop 方案**：用 OpenTelemetry 把 user_id 注入 trace，自动关联到 token usage——「**哪个用户的哪个动作触发了哪笔成本**」。

### 各类指标的告警阈值（起步参考值）

| 指标 | 警告阈值 | 严重阈值 |
|------|---------|---------|
| 质量分布低分尾部（≤2 分占比）| > 15% | > 30% |
| Hallucination 率 | > 5% | > 10% |
| Refusal 率 | > 10% | > 20% |
| 第 3 级降级触发率 | > 20/天 | > 100/天 |
| 第 4 级降级触发率 | > 0 | 任何 |
| Cost-per-active-user vs 预算 | > 80% | > 100% |
| P99 延迟 vs SLA | > 80% | > 100% |
| 用户主动转人工率 | > 15% | > 30% |

⚠️ **以上阈值是给团队起步用的 anchor 值，不是业内统一标准**。不同业务场景（客服 / 编程 / 创意 / 医疗）的合理阈值可能差 5-10 倍——**建议团队根据自己的业务调出真实阈值**，专栏给的数字只为打破"没基准"的状态。

阈值不达标——dashboard 立刻 alert，PM 1-2 小时内介入。

### 监控 Dashboard 的最小集

#### 给老板看的版本（5 项）
1. MAU 趋势
2. 用户满意度（NPS 或 5 星均值）
3. 月度 LLM 成本 / ARR 比例
4. 第 4 级 bad case 次数（必须 = 0）
5. 业务核心指标（转化 / 留存）

#### 给团队看的版本（15+ 项）
- 上述 5 项
- 质量分布 histogram
- Bad case 按类型分类计数
- 各级降级触发率
- Cost-per-user 分布
- P50 / P99 延迟
- 头部 1% 用户消费
- Refusal 率 / Hallucination 率
- 用户主动转人工率
- ……

### 指标 review 节奏

**日报**（自动发）：
- 4 类 AI 特有指标的当日数据
- 任何 > 警告阈值的指标 highlight
- 异常的 bad case 例子（5-10 个）

**周报**（PM 写）：
- 4 类指标的周趋势
- 新发现的 bad case 类型
- 本周的发版动作 vs 指标变化关联

**月报**（PM + 业务方一起）：
- 4 类指标的月趋势
- LLM 成本 / ARR 是否健康
- 下月迭代方向

---

## 下半篇 · engineering reality

### 监控的「延迟暴露」问题

**AI 产品的问题往往滞后 2-7 天才暴露**。

为什么？因为：
- bad case 集中在长尾用户身上，需要时间收集
- 用户从遇到问题到反馈，平均 3-5 天
- 模型质量退化是渐进的，不是断崖
- 监控指标的统计学需要样本量

**Anthropic 自家 postmortem**（2025）：

为了降延迟、降 verbosity、改 caching 做了"看似合理"的优化——**HTTP 200、延迟正常、dashboard 全绿**，但实际输出已经回归。

**关键失败点**：用户反馈到 eval 覆盖之间有约 **2 周延迟**——这正是"AI 延迟暴露"的标准窗口（行业普遍 2-7 天）。

### 为什么「平均分」在 AI 产品里没用

举个例子说明。

某 AI 客服整体满意度 4.2/5。

但如果你看分布：
- 70% 用户给 5 分（happy path 正常）
- 25% 用户给 3-4 分（小问题但能用）
- **5% 用户给 1 分**（彻底崩）

这 5% 是谁？通常是：
- 边界 case 用户（特殊需求）
- 高价值客户（要求高）
- 公众人物 / KOL（声音大）

**这 5% 决定用户口碑**——他们会去微博、即刻、小红书骂你。

平均分 4.2 看着很美，**实际产品已经在崩塌的边缘**。

### 业内监控失败案例

#### 案例 1：Google AI Overviews 胶水披萨（2024-05）

基础设施零异常，**但"披萨加胶水"、"每天吃一块石头"在 24 小时内全网爆梗**——失败发生在 content layer，不在 infra layer。

监控了 infra，没监控 content quality。

#### 案例 2：DPD 聊天机器人（2024-01）

系统更新后 AI "全绿"，被英国音乐家 Ashley Beauchamp **调教出脏话和"DPD 是世界最差快递"的诗**，单条推文 X 内数百万曝光后才被强制下线。

监控了系统稳定性，没监控对抗输入的抗性。

---

## AI 监控 SaaS 工具

业内有成熟工具，PM 不需要从零搭：

### Helicone
- 一行 proxy 接入
- 原生支持 cost / latency / failure 监控

### LangSmith
- LangChain 官方
- 适合 RAG / Agent 调试

### Arize
- 企业级 AI observability
- bad case 分类做得最细

### Braintrust
- eval-driven development 全套
- CI/CD 集成

**选择建议**：
- 早期（< 100K 调用/月）：Helicone（便宜简单）
- 中期（100K-10M 调用/月）：LangSmith / Braintrust
- 大规模（> 10M 调用/月）：Arize 企业版

---

## 质量工程视角看 AI 监控 = 概率系统的可观测性

**8 年做软件质量工程的视角**——

传统软件监控的核心是「**可观测性**」（observability）—— logs + metrics + traces 三件套。

AI 产品在此之上**新增一类**——「**分布可观测性**」（distributional observability）。

- 传统：监控"系统在不在响应、响应快不快"（log + metric）
- AI：监控"系统响应的分布在哪、低尾部多少"（distribution + histogram）

「**平均分掩盖低尾部**」的本质是——**用确定性指标监控概率系统，必然漏掉关键失败信号**。

PM 必须懂得"看分布而非看均值"——这是 AI 时代监控的基本动作。

---

## 给你的可执行清单

#### 动作 1：你的产品监控必须有 4 类 AI 特有指标
- 质量分布 / Bad case 比例 / 降级触发率 / Cost-per-user
- 任何一类缺失 → 监控不合格

#### 动作 2：所有指标看分布不看均值
- 用 histogram
- 重点关注低分尾部

#### 动作 3：Bad case 按类分类计数
- hallucination / refusal / format / off-topic / safety
- 5 类分别监控，不合并

#### 动作 4：日报 / 周报 / 月报三层节奏
- 日报自动发
- 周报 PM 写
- 月报 PM + 业务方一起

---

## 反共识金句

- **"AI 产品的 200 OK 是真的 OK，但你的用户已经在骂街了。"**
- **"Dashboard 全绿不代表产品没病，只代表你的监控还停留在 web 时代。"**
- **"通用 eval 是安慰剂，bad case 分类才是听诊器。"**

---

## 写在最后

这一篇讲了监控指标。下一篇讲——**Bad case 管理**。

监控发现 bad case 之后怎么处理？传统 bug 是"修了就好"，**AI bad case 是"修了可能更糟"**。

下一篇讲 Bad Case 管理 5 步 + 修了 A 坏了 B 的真实案例（GPT-4o sycophancy + Gemini 图像 over-tune）+ 优先级框架。

下一篇见。

---

> **本文配套资产**：AI 产品监控 Dashboard 模板 + 4 类指标告警阈值参考 + 工具对比（付费读者解锁）
> **下一篇预告**：21 · Bad Case 管理——从"修 Bug"到"调系统"的思维转变
> **反馈 / 加入读者群**：欢迎在公众号「蔡逸雯」留言
