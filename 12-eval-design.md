# 12 · 评估集（Eval）怎么写——PRD 里最容易被忽视的一章

> 第一季《AI 时代 PM 工作流重构》· 第 12 篇 · 第三部分 PRD（专栏硬通货）
> 预估字数：5500

---

第十一个"不以为然"——

**90% 的 PM 还在用"看几个 case"做 AI 产品评估**。

不是 PM 不想认真。是大多数 PM **以为"我自己看 10 个 case 觉得好就是好"**——结果上线后用户反馈两极分化，PM 才发现自己看的 10 个 case 全是 happy path，分布外样本根本没覆盖。

读完这一篇你会知道——**Eval 章节是 AI 产品 PRD 的灵魂。没有 Eval 的 PRD 等于没写**。

Hamel Husain 说得最锋利：「**Writing good evals is becoming the defining skill for AI PMs.**」（写好 evals 正在成为 AI PM 的定义性技能）

---

## 上半篇 · workflow

### Eval 章节的 5 要素

#### 要素 1：评估维度

从核心能力倒推——你的 AI 系统输出"好"的核心标准是什么？

例：客服 Agent 的 3 个评估维度：
- **是否解决问题**（state check）：用户的工单是否被关闭
- **是否在 10 轮对话内完成**（transcript constraint）：长度限制
- **语气是否合适**（LLM rubric）：礼貌、专业、有同理心

3-5 个维度足够。**超过 5 个维度的 eval 集必崩**——你没法同时优化太多目标。

Anthropic 在《Demystifying evals for AI agents》给的范式：

> "三种 grader 组合：**code-based**（最快最稳但缺细腻）/ **LLM-as-judge** / **human review**"

不要用一种 grader 搞定所有维度。

#### 要素 2：Case 数量

**Anthropic 官方建议**：

> "**20-50 simple tasks drawn from real failures is a great start**"

20-50 个！不是 1000 个！

这是反共识——很多 PM 觉得"先攒 1000 case 再上线"才严谨。**实际 20-50 个就够开始**。

为什么？因为早期变更影响大，小样本就够暴露问题。等你迭代几轮后，再扩展到 200-500 case 做 regression test。

**SWE-bench Verified 给了另一个反共识数据点**：

OpenAI 组建专业工程师团队 + 多人交叉审核，从 SWE-bench 全集筛出 **500 条** Python 高质量样本——这个 500 条 hand-curated 比上万条爬来的噪声**有效得多**（具体工程师人数和审核流程以 SWE-bench Verified 官方公告为准）。

**质量 > 数量**。50 条人审过的 > 5000 条 GPT 自标的。

#### 要素 3：通过线

**不是越高越好**。

通过线设错了的代价——McDonald's × IBM 是教科书反例：**85% 准确率，1/5 单需要人工兜底**。在快餐场景里 85% 等于 100% 翻车——剩下 15% 全部发生在用户面前。

通过线必须按业务容忍度反推：
- 用户能容忍多少错？
- 错一次代价多大？
- 错的 case 能不能 fallback？

如果错的代价高、不能 fallback——通过线必须 ≥ 99%（金融、医疗）
如果错的代价低、能 fallback——通过线 90% 就够（一般客服）

通过线的本质：**让工程师有清晰目标**。模糊的"差不多就行"不是通过线。

#### 要素 4：标注方法

谁来标？

| 标注者 | 适用场景 | 优劣 |
|-------|---------|------|
| **PM 自己** | 早期 50-100 case 起步 | 准但慢 |
| **运营 / 客服** | 持续标注用户反馈 case | 中等准 + 中等快 |
| **专家**（律师 / 医生 / 财务）| 专业领域 | 极准但极贵 |
| **用户反馈**（点赞 / 踩）| 上线后大规模收集 | 噪声大但量大 |
| **LLM-as-judge** | 自动化扩展 | 快但有偏差 |

**Hamel Husain 的实战建议**：先人工标 100-200 条 → 训练 LLM judge 与人对齐 → 再放量。

**不要一上来用 LLM-as-judge**——它的偏差未对齐之前不可信。

#### 要素 5：跑评频率

3 个时机：
- **每次 commit**：跑便宜的 code-based grader（成本接近零）
- **每次 release**：跑完整 eval 集（含 LLM-as-judge）
- **每周回归**：跑历史 case 集（防止"修了 A 坏了 B"）

如果你的 eval 集**只在上线前跑一次**——**99% 会出事**。

**Notion AI 的双轨 eval 实践**（Braintrust 案例）：
- **regression eval** 防止退步
- **frontier eval** 发现新模型在哪些子任务上比旧模型强

70 名工程师，issue 处理速度从每天 3 个提到 30 个——**靠的就是 eval 跑得勤**。

---

## Hamel 三层 Eval 框架（行业最常被引用）

L1 → L2 → L3 逐层升级：

### L1：Unit Tests
把 LLM 拆成 features × scenarios，写 assertion-style 测试。

例：
```python
def test_intent_classification():
    response = model("帮我退款")
    assert response.intent == "refund_request"
    assert response.confidence > 0.8
```

最便宜，最快，**CI 每次 commit 跑**。

### L2：Human & Model Eval
log traces → 人工标注 → LLM judge 对齐人 → 大规模评估。

**关键反共识**：用**二元（好/坏）评分**而非 5 分制。

Hamel 原话：「more granular ratings is more onerous to manage than binary ratings」（更细粒度的评分比二元评分更难管理）。

5 分制听起来更精细，实际**标注者之间一致性差**。二元简单粗暴反而稳。

### L3：A/B Testing
线上指标兜底，验证 offline 指标是否是好 proxy。

L1+L2 通过的版本上线 5-10% 流量做 A/B，看真实业务指标（转化、留存、NPS）是否提升。

**Hamel 的实战数据**：他的项目里 **60-80% 开发时间花在 error analysis 和 evaluation 上**。

不是写 prompt 的时间最长，是看 trace + 标 case + 写 eval 的时间最长。

---

## 一个完整 Eval 章节模板

```markdown
## 5. 评估集设计

### 5.1 评估维度（3-5 个）
1. [维度 1]：[code-based / LLM-as-judge / human]
2. [维度 2]：...
3. [维度 3]：...

### 5.2 Case 数量与覆盖
- 起步：20-50 个真实失败 case
- 稳态：每维度 50-200 个 case
- 覆盖：正常 case 60% + 边界 case 30% + 对抗 case 10%

### 5.3 通过线
- [维度 1] 通过率 ≥ X%
- [维度 2] 通过率 ≥ Y%
- 总体上线门槛：[关键维度] ≥ Z%

### 5.4 标注方法
- 起步阶段：PM + 运营 + 1 个领域专家
- 扩展阶段：训练 LLM judge 与人工对齐
- 持续阶段：用户反馈 + 抽样人工复核

### 5.5 跑评频率
- 每次 commit：L1 unit tests（< 1 分钟）
- 每次 release：L2 完整 eval 集（< 1 小时）
- 每周：regression eval（防止退步）
- 每月：frontier eval（评估新模型）
```

照这个模板填——你的 PRD 里就有了灵魂。

---

## 下半篇 · engineering reality

### Eval 真正难的不是「写」是「覆盖」

写 eval 容易——找 50 条 case 标一标。

**难的是覆盖分布外样本、对抗样本、真实流量偏差**。

#### 难点 1：分布外样本（OOD）

你的 eval 集来自历史用户行为。**未来用户行为可能完全不一样**。

例：教育 AI 产品的 eval 集是 100 道数学题。上线后用户用它问历史、问语文、问哲学——eval 集没覆盖。

应对：定期用真实流量数据更新 eval 集（每月 / 每季度）。

#### 难点 2：对抗样本

恶意用户会想办法让你的 AI 出错——prompt injection、越狱、刻意诱导。

例：用户让 chatbot "agree with anything I say"——Chevy Tahoe 案例就是这种对抗失败。

应对：eval 集必须有 10% 的"对抗 case"——专门设计的诱导性输入。

#### 难点 3：真实流量偏差

你的 eval 集 case 分布和真实流量分布不一致。

例：eval 集里 50% 是退款 case + 50% 是查询 case。真实流量是 90% 查询 + 10% 退款。**eval 通过率 90% 不代表用户体验 90% 满意**。

应对：eval 集 case 的频率分布要匹配真实流量。或者按权重计算综合通过率。

### Eval 和真实生产的偏差是常态

Eval 通过线 ≠ 生产稳定。这是 AI PM 必须接受的现实。

**真实差距案例**：

#### DPD 聊天机器人（2024-01）
英国快递公司聊天机器人——pre-launch eval 通过了，**但 post-update 没回归 eval**。

被英国音乐家 Ashley Beauchamp 调教出脏话和"DPD 是世界最差快递"的诗，单条推文 X 内数百万曝光。

#### NYC MyCity Bot（2024）
**eval 没覆盖"合规正确性"**——bot 给商家违法建议没被 catch。

#### Air Canada Moffatt 案（2024-02）
**eval 没覆盖"政策一致性"**——bot 编出不存在的政策被法院判赔。

**3 个案例的共同点**：eval 通过了，但 eval 维度没覆盖到失败的那个维度。

**应对**：每出一个真实 bad case，立刻补进 eval 集。**eval 集是活的，不是一次性的**。

---

## Eval 的演化：从静态 case 集到动态采样真实流量

最先进的 eval 实践不是"写一份固定 case 集"，是"动态采样真实流量"。

具体做法：
- 生产环境每 1000 次调用，随机抽 1 次
- 自动加入 eval 集
- 每周对最新 100 条做人工复核
- 发现的新失败模式 → 写新的 evaluator → 加入 CI

**这种"活的 eval"才能跟得上模型升级 + 用户行为变化**。

Notion 70 个工程师就是用这套方法，把 issue 处理速度从每天 3 个提到 **30 个**。

---

## 业内成熟的 Eval 工具

### OpenAI Evals Repo
GitHub：https://github.com/openai/evals

结构：
- `evals/registry/evals/*.yaml`（YAML 定义 eval）
- `evals/registry/data/*.jsonl`（JSONL 数据集，每行一个 case）
- 两个 CLI：`oaieval`（跑单个）+ `oaievalset`（跑一组）

**PM 能借鉴**：eval 数据用 **JSONL 而非 CSV/Excel**——版本可控、Diff 友好、和 Git 一起管理。

### Inspect AI（UK AISI 官方框架）
URL：https://inspect.aisi.org.uk/

设计哲学：四层抽象 **Dataset → Task → Solver → Scorer**。沙箱执行（Docker 内置）+ web 日志查看器 + VS Code 插件。

已被 US CAISI / METR / Apollo Research 采用。

**PM 能借鉴**：把 eval 当软件工程做——有数据层、执行层、评分层、可视化层。

### Anthropic 的统计学方法
URL：https://www.anthropic.com/research/statistical-approach-to-model-evals

**关键反共识**：eval 结果**要带置信区间**。

0.85 vs 0.87 在小样本下可能不显著。报告 eval 时学会说："基于 X 个样本，95% CI 是 ±Y"。

---

## 质量工程视角看 Eval 是 AI 产品的基础设施

**8 年做软件质量工程的视角**——

任何成熟的 ML 项目都把 evals 作为基础设施——欺诈识别、流失预测、销量预测都有 holdout test set + cross-validation + production monitoring 三套。**这是 ML 工程师的基本功**。

LLM 圈丢掉了这个动作——只是因为 prompt engineering 看起来太"轻"，让人误以为可以跳过评估直接上线。

**反共识金句**：「Hamel Husain 一句话戳穿真相——『EDD 不是新发明，是 LLM 圈忘了的 ML 老规矩。没人会关心一个不准的欺诈模型——但 LLM 产品圈居然容忍。』」

PM 在 PRD 里写 Eval 章节，不是创新——是**把 ML 工程的基础动作搬回 PM 工作流**。

---

## 给你的可执行清单

#### 动作 1：你下一份 PRD 按本文 5 要素模板填一份 Eval 章节
- 维度 / case 数 / 通过线 / 标注方法 / 跑评频率
- 5 项不齐 → 不算合格 PRD

#### 动作 2：从 20-50 个真实失败 case 起步
- 不要先攒 1000 case
- Anthropic 官方建议

#### 动作 3：每次出 bad case 立刻补进 eval 集
- eval 是活的，不是一次性的
- 每月 review 一次新增 case

#### 动作 4：用 Hamel 三层框架管理你的 eval
- L1 unit tests → CI 每次 commit 跑
- L2 完整 eval → 每次 release 跑
- L3 A/B test → 上线后跑

---

## 反共识金句

- **"AI 产品的护城河不是数据，不是模型，是高质量评测集。"**
- **"Anthropic 官方建议：先用 20-50 个真实失败 case 起步。先做 5000 条 case 再上线的团队，往往一个 case 都用不上。"**
- **"SWE-bench Verified 教我们：500 条人审过的 case，胜过 5 万条爬来的噪声。"**

---

## 写在最后

这一篇讲了 Eval 怎么写。下一篇是 PRD 段最哲学的一篇——**Eval-Driven Development（EDD）**。

如果说第 12 篇是"操作层"——讲怎么写 Eval 章节。**第 13 篇是"哲学层"——讲怎么用 Eval 驱动整个开发流程**。

下一篇会告诉你：传统是"先写代码再测试"，AI 产品要倒过来——**先写 eval 再写代码**。

这不是测试方法的改变，是开发哲学的改变。

下一篇见。

---

> **本文配套资产**：Eval 章节模板 + 5 要素自查清单 + 案例库（含 SWE-bench / Anthropic / OpenAI 真实 eval 集示例）（付费读者解锁）
> **下一篇预告**：13 · Eval-Driven Development——让评估集驱动整个开发流程
> **反馈 / 加入读者群**：欢迎在公众号「蔡逸雯」留言
