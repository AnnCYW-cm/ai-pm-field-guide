---
tool_id: P1-pack-growth
serves_essays: [01, 25, 26]
status: ready-for-review
last_updated: 2026-05-21
version: v1.0
deliverable_formats: [markdown, pdf, notion-template]
hours_actual: 18.9 (Agent 调研 + 写作)
references_pools_used: [P1.7 Sachin Rekhi, P1.8 Marty Cagan, P1.10 Anton Osika, P1.11 Lenny, P2.13 Stanford HAI Index, P4.15 Humane AI Pin, P4.17 Cursor, P4.18 Lovable, P5.4 Stuart Russell, P5.5 Bengio, P5.8 5 经典论文, P6.1-6.10 风投视角, P9.1 Latent Space, P9.6 Acquired, P9.9 No Priors, P9.10 AIE WF, P10.1-10.6 国际 PM 社区]
validation_status: "未做真 PM 测试 (n=0)；v2.0 计划 n=3-5"
notes: "覆盖第 01/25/26 篇 - 6 塌陷点 / 3 团队模型 / 6 维成长路线图"
---

# AI PM 成长包 v1.0

> 覆盖原稿：第 01 篇（6 个塌陷点） / 第 25 篇（AI Native 团队） / 第 26 篇（PM 成长路径终章）
> 使用对象：传统 PM 转 AI PM / AI Native 团队搭建 / PM 个人成长自检

---

## 工具说明

3 张可直接打印贴墙的自检表 + 1 张 6 维能力路线图 + 1 套必读资源清单。

读完原稿 01/25/26 三篇后，做 4 件事：
1. **6 塌陷点自查**——你目前踩了几个坑（模块 A）
2. **AI Native 团队对照**——你的公司属于哪种模式（模块 B）
3. **6 维能力自评**——你目前在 Apprentice / Journeyman / Master 哪一段（模块 C）
4. **每周精读 1 篇必读**——按附录的清单滚动学习

**设计原则**：不教你"AI PM 应该是什么"，只问你"你现在踩在哪、缺什么、下一步走哪"。

---

# 模块 A · 第 01 篇配套：6 个塌陷点自查表

## 塌陷点 1：用户访谈拿不到真需求

**症状**：
- 访谈记录全是"我希望 AI 能像 Jarvis 一样懂我"——但用户不为这个付费
- 用户描述的"理想场景"和你产品能交付的"概率分布"对不上
- 访谈 20 人，得出 20 个不同方向——拿不出 1 条收敛的需求

**识别信号（5 项打分 · 中 ≥3 就是塌陷）**：
- [ ] 你访谈用户时，问的还是"你希望 AI 能做什么"
- [ ] 你没有把 ChatGPT / Claude 拿到访谈现场让用户实际跑
- [ ] 用户提到的需求 ≥50% 来自科幻片 / 友商演示视频
- [ ] 你没有区分 "pre-experience expectation" 和 "post-experience evaluation"
- [ ] 访谈结束后无法给出"用户实际愿意付钱的 3 个具体场景"

**修复路径**：
- **短期**：访谈现场带 ChatGPT 让用户**当场使用 10 分钟**再问；Teresa Torres "Continuous Discovery" 聚焦"上周你实际做了什么"
- **中期**：引入 Marty Cagan 4 风险框架（价值 / 可用性 / 可行性 / 商业可行性）；建 "expectation gap log"——差距 > 50% 的需求直接 kill

**真实案例**：**Humane AI Pin**——融资 $2.3 亿，2025-02 卖给 HP 仅 $1.16 亿。**根因**：访谈采到的是科幻预期（"我想要 Her 里的那种 AI"），不是付费意愿。

---

## 塌陷点 2：PRD 写不下去

**症状**：
- 打开 Word 写到"完成定义"光标停 20 分钟
- 写到"页面跳转"——AI 产品根本没"页面"
- 写到"验收标准"写"用户满意度 > 80%"——自己都觉得空

**识别信号**：
- [ ] PRD 模板里没有 "Eval 集" 章节
- [ ] PRD 模板里没有 "Bad Case 分级" 章节
- [ ] PRD 模板里没有 "Token 成本预算" 章节
- [ ] 写完 PRD 没用 Claude Code 跑通 prototype
- [ ] PRD 还在用"功能列表"而非"能力 + rubric"

**修复路径**：
1. **抛弃传统 PRD 模板**——参照 Anthropic Mike Krieger 的 "Product Note"（3-4 段：用户意图 / 期望结果 / 具体指标）+ 两个 context 文件
2. **加 3 个新章节**：Eval 集 / Bad Case 4 级 / Token 成本预算
3. **试一次 BMAD-METHOD** 拆 Architect / PM / Developer 三个 agent
4. **学 GitHub Spec Kit** 的 `/specify` → `/plan` → `/tasks` → `/analyze`

**真实案例**：**Aparna Chennapragada（Microsoft CPO）**——"**Prompt sets are the new PRDs**"。PRD 这种"给人看的文档"形态本身在 AI 产品上失效。

---

## 塌陷点 3：技术评审被反问"评估集呢"，答不上来

**症状**：
- 工程师问"你的 golden set 在哪"——你拿不出文件
- 工程师问"通过线是多少"——你说"差不多就行"
- 评审会 2 小时，最后没人画押"什么算做完了"

**识别信号**：
- [ ] 没准备过 "golden set"（≥50 条人工标注的输入-期望输出对）
- [ ] 不知道 LLM-as-Judge 怎么搭、怎么对齐
- [ ] 没区分 regression eval 和 frontier eval
- [ ] 没设置过 4 类 metrics（accuracy / latency / cost / safety）
- [ ] 不会算 95% 置信区间

**修复路径**：
- **起步**：Hamel Husain & Shreya Shankar 的 Maven 课（业内最被引用）
- **进阶**：Inspect AI 4 层抽象（Dataset → Task → Solver → Scorer）+ SWE-bench Verified 500 条 hand-curated

**真实案例**：Hamel 在 Lenny Newsletter 核心观点："**Writing good evals is becoming the defining skill for AI PMs**"。

---

## 塌陷点 4：老板问"这功能成本多少"，token 账算不出来

**症状**：
- 老板问"每月烧多少钱"——你说"应该不贵"
- CFO 拿账单来——比预估高 5-10 倍
- 灰度推全 3 周后，老板找你"我们的毛利怎么是负的"

**识别信号**：
- [ ] 不知道 input token 和 output token 的价格倍数关系
- [ ] 没算过 retry 失败带来的成本翻倍
- [ ] 不知道 multi-turn 对话 input 是"二次方膨胀"还是线性
- [ ] 没设置过 per-user hard cap
- [ ] 看不懂 prompt caching 节省的成本明细

**修复路径**：
- 学 ICONIQ 2025：AI 产品毛利 2024=41% / 2025=45% / 2026=52% 的爬升路径
- 看 a16z 2025：企业 LLM 年均 $4.5M → $7M（+56%）
- 学 Vellum per-user hard cap + Finout 成本分析

**真实案例**：**Cursor 2025-06 billing 暴雷**——老用户从 "$20/月心智模型" 突然变成 $200-$400 overage，Hacker News 晒 "$350 in a week"。**任何 AI PM 都该背下来这个案例**——不仅算 token 成本，还算"用户预期成本 vs 账单实际成本"的落差。

---

## 塌陷点 5：上线后 bad case 出现，不知道该修 prompt 还是改产品

**症状**：
- 第 3 天 bad case 来了，你改 prompt
- 第 7 天 Y 场景翻车——上周明明跑得好好的
- 改 prompt 改 3 轮越改越糟

**识别信号**：
- [ ] 脑子里没有 "failure taxonomy"（5 类失败模式）
- [ ] 修 bad case 第一反应都是"改 prompt"
- [ ] 没建过 regression eval set
- [ ] 不会判断 retrieval 漏文档 / prompt injection / 业务设计 / 模型能力 四类
- [ ] 处理过的真实 bad case ≤50 个

**5 类失败模式（Hamel）**：
1. **Hallucination**（幻觉）→ 加 RAG / grounding
2. **Refusal**（拒答）→ 改 prompt / 调 safety threshold
3. **Drift**（漂移）→ 改产品设计
4. **Format breaking**（格式崩）→ structured output
5. **Safety violation**（违规）→ 加 filter + 改 system prompt

**真实案例**：**OpenAI GPT-4o sycophancy 事件（2025-04-25 → 4-29）**——4 天内全量回滚。OpenAI 自己 postmortem 承认：**"sycophancy 没有作为 blocking 项进入发版评估"**。只看了 helpfulness，没看 harmfulness 的回归。

---

## 塌陷点 6：复盘会上无法判断"是模型问题还是设计问题"

**症状**：
- 数据不好看，没人能拿出归因
- 工程师说"模型还不行"
- 设计师说"用户路径有问题"
- 老板问"为什么我们的 AI 不如 ChatGPT"——你无言以对

**识别信号**：
- [ ] 不知道"模型问题"和"设计问题"的判断分界线
- [ ] 没做过 ablation study
- [ ] 没看过 trace 找根因
- [ ] 复盘会上只能说"留存低 / 转化低"——拿不出"为什么"
- [ ] 没读过 Apollo Research / Redwood Research / METR 的 AI 失败论文

**判断分界 4 步法**：
1. 看 trace——同一类 bad case 抽 10 条，看模型输出
2. 判断输出本身对不对——对，是设计问题；错，进入第 3 步
3. 看 input 是否完整——不完整，是 retrieval / context 问题；完整，进入第 4 步
4. 看是否换 SOTA 模型能改善——能，是模型能力问题；不能，是任务设计本身不可行

**真实案例**：**Klarna AI 替代 700 客服反转（2024-02 → 2025-05）**——一年内反转。真相：**任务设计错**——客服复杂场景需要 empathy + 跨系统决策，不是 LLM 当下的能力区。

---

## A.7 6 塌陷点综合自检卡

```
┌────────────────────────────────────────────────┐
│  AI PM 6 塌陷点自检卡（v1.0）                  │
│                                                │
│  □ 1. 用户访谈拿到的是科幻预期还是付费意愿？   │
│  □ 2. PRD 里有 Eval / Bad Case / Token 章节？  │
│  □ 3. 评审时能拿出 golden set + 通过线？       │
│  □ 4. 老板问成本 30 秒内能给出量级估算？       │
│  □ 5. 上线后 bad case 能分类 4 选 1 修复？     │
│  □ 6. 复盘会能用 4 步法判断模型 vs 设计问题？  │
│                                                │
│  打 3 个 ✅ 以下：先读专栏第 1-15 篇           │
│  打 4-5 个 ✅：读 16-26 篇 + 做 100 个 bad case│
│  打 6 个 ✅：直接做 senior AI PM / 转咨询      │
└────────────────────────────────────────────────┘
```

---

# 模块 B · 第 25 篇配套：AI Native 团队 3 种主流模型

## B.1 模式 1 · Anthropic 模式：PM/Designer/Eng 同岗 + 全员 Claude Code

```
┌────────────────────────────────────────────┐
│       Anthropic 模式（~2000 人）           │
│                                            │
│  Research 35%  |  Eng 45%  |  P/D 15%    │
│  ~700 人       |  ~900 人  |  ~300 人     │
│                                            │
│  GTM / Sales / Ops 极少                    │
│  销售 quota carrier 数十人                 │
│  服务数十万企业客户                        │
│                                            │
│  关键特征：                                │
│  • PM/Designer/Eng 三岗同用 Claude Code   │
│  • Boris Cherny 100% 代码由 Claude Code 写│
│  • Mike Krieger PRD 压缩到 3 段 Product Note│
│  • Cat Wu: "Prototypes over PRDs"         │
└────────────────────────────────────────────┘
```

**适用**：
- ✅ 模型公司 / 前沿 AI 研究
- ✅ Series C+ 且有 talent density 招 PhD
- ❌ 99% 应用层公司（养不起 35% Research）
- ❌ ToC 高流量产品

**中国本地化**：
1. **不要追 35% Research 比例**——人才密度不足，硬凑反而稀释
2. **保留"全员用 Claude Code / Cursor / Trae"**——这是最容易复制的部分
3. **保留 "Product Note over PRD"**——文化层面变化最值钱
4. **国内参考**：智谱清言、MiniMax 海螺

**一句话**：精髓不是 "35% Research"，是 "**所有岗位都把 LLM 当成默认工作环境**"——这个文化中国团队可以学。

## B.2 模式 2 · Cursor 模式：小团队高人均 ARR

```
┌────────────────────────────────────────────┐
│      Cursor 模式（~100 工程师团队）        │
│      撑起 $1B 量级 ARR（2025-Q3）          │
│                                            │
│  Eng 50%+  |  PM 团队  |  Eval 团队        │
│  ~50 人    |  5-10 PM  |  独立 5-10 人    │
│                                            │
│  关键特征：                                │
│  • 每 10-20 工程师 1 PM                   │
│  • 独立 Eval 团队（新角色！）             │
│  • 营销小，靠 PLG（Product-Led Growth）   │
│  • Notion 已设独立 Eval 团队为业内样板    │
└────────────────────────────────────────────┘
```

**适用**：
- ✅ AI 应用层 SaaS（开发者工具 / 写作工具）
- ✅ 已验证 PMF，准备 10 → 100 人
- ❌ ToB SLG 传统企业软件
- ❌ 重度合规行业

**中国本地化**：
1. **PM 配比照搬**：每 10-20 工程师 1 PM——和硅谷一致
2. **独立 Eval 团队最值得设**——中国普遍缺 Eval 文化，先设先有竞争力
3. **PLG 在中国比硅谷难**——补"用户运营 / 社区运营"（每 50 工程师 1 个）
4. **国内参考**：豆包工程团队、海螺 PM、Trae、Manus 早期

**关键 trade-off**：中国团队比 Cursor 多 1 个角色——**关系型销售 / KA 经理**（因为中国 ToB 不是 PLG only）

**一句话**：精髓是 "**少 PM 多 Eng + 独立 Eval + PLG**"——3 条中国团队都能学，第 3 条要补销售。

## B.3 模式 3 · Lovable 模式：18 人 → 146 人，全员工程师，PM = 0

```
2025-Q3 快照（18 人，$17M ARR）：
  18 人 = 全员工程师 + 创始人
  PM 数量：0
  Anton Osika: "工程师都在做 PM 的事"

2026-02 快照（146 人，$400M ARR）：
  人均 ARR ≈ $2.7M
  仍然以工程师为主
  仍然几乎零付费广告

2026-Q2 ~517 人（持续扩张）
```

**适用**：
- ✅ 早期 startup（1-30 人，PMF 探索期）
- ✅ 独立开发者 / 小型 AI 产品
- ✅ 工程师创始人主导
- ❌ ToB 大客户场景
- ❌ 强合规行业

**中国本地化**——**99% 学错了**：

**学错的姿势**：
- "我也不招 PM"——但创始人没有 Anton Osika 的工程能力
- "我也用 Claude Code"——但团队水平不够，AI 写出的代码反而拖累
- "我也搞社区"——但创始人 X / Twitter 不活跃

**学对的姿势**：
1. **必要条件**：创始人本人**既是工程师又是产品决策者**
2. **AI 工具熟练度**：团队人均 Claude Code 月使用 ≥ 40 小时
3. **公开输出**：创始人 + 早期员工持续在小红书 / 即刻 / X 公开输出
4. **国内参考**：Manus 早期、Trickle 早期、部分独立开发者出海团队

**最致命的认知错误**——不是 "PM = 0"，是 "**没有人做产品决策**"。Lovable 的真相是 Anton 一个人兼任 PM。

**一句话**：不是"省 PM"，是 "**创始人 + 顶尖工程师，每个人都能做 PM 决策**"——99% 中国团队达不到这个 talent density。

## B.4 3 种模式横向对比

| 维度 | Anthropic | Cursor | Lovable |
|---|---|---|---|
| 团队规模 | 500-数千人 | 50-200 人 | 5-150 人 |
| PM 角色 | 同岗化（PM = mini-Eng） | 精干 1:10-20 | 0（创始人兼任） |
| Eval 团队 | 与 Research 融合 | **独立团队** | 工程师兼任 |
| 增长打法 | 模型壁垒 + 企业大单 | **PLG + 自然增长** | 社区 + KOL + 零付费 |
| 适用阶段 | Series C+ / 模型公司 | 应用层 SaaS PMF 后 | 早期 / 独立开发者 |
| 中国本地化难度 | ⭐⭐⭐⭐⭐ 极难 | ⭐⭐⭐ 中 | ⭐⭐⭐⭐ 难（看创始人） |
| 人均 ARR 标杆 | 业内顶级 | $5-10M | $2-3M（Lovable 2026） |

## B.5 选模式 5 问决策树

```
Q1：你的核心壁垒是 model 还是 product？
├─ Model → Anthropic 模式
└─ Product → 进 Q2

Q2：你的增长打法是 PLG 还是 SLG？
├─ PLG → 进 Q3
└─ SLG → 不是 AI Native，是传统 SaaS

Q3：你现在团队人数？
├─ <30 人 → Lovable 模式
├─ 30-200 人 → Cursor 模式
└─ >200 人 → Cursor 模式扩展版（仿 Notion）

Q4：你的创始人是工程师吗？
├─ 是，本人写代码 → Lovable 可行
└─ 否 → 即使 <30 人也要补 1 个工程联创做 CTO

Q5：你所在行业有强合规要求吗？
├─ 有（医疗 / 金融 / 法律）→ 上述 3 种不直接适用，
│   需要额外加 Eval 团队 + Compliance 团队，至少照 Cursor 起步
└─ 没有 → 按 Q1-Q4 走
```

---

# 模块 C · 第 26 篇配套：PM 成长路径 6 维路线图

## 6 维能力设计依据

- **维度 1（Vibe Coding）**：Anthropic Boris Cherny / Sachin Rekhi 核心——PM 不会 Vibe Coding 等于半残
- **维度 2（Eval）**：Hamel "defining skill for AI PMs"
- **维度 3（成本）**：Cursor 2025-06 billing 暴雷之后的硬通货
- **维度 4（合规）**：Stuart Russell / Bengio 框架下 PM 的合规决策
- **维度 5（协作）**：Mike Krieger / Cat Wu / Aparna 强调的"三方对话"
- **维度 6（行业判断）**：靠订阅 Latent Space / Stratechery 持续校准

**3 段位灵感**：Sachin Rekhi **AI Prototyping Mastery Ladder**（Apprentice / Journeyman / Master）

## C.1 维度 1：Vibe Coding 实战

| 段位 | 标志 |
|---|---|
| Apprentice（0-6 月）| 会用 ChatGPT / Claude Q&A；能跑 Cursor / Claude Code 教程 demo；能用 v0 / Bolt / Lovable 做 toy prototype |
| Journeyman（6 月-2 年）| 30 分钟内验证一个需求；能区分 Cursor / Claude Code / Lovable / Bolt / v0 / Replit / Trae 适用场景；能用 BMAD / Spec Kit 写 spec |
| Master（2 年+）| 独立做出可上线的 internal tool；能写 spec 让 sub-agent 编队跑 6 小时；能用 Claude Code 做 codebase 重构；能做 Vibe Coding 横评 |

**参考标杆**：Dennis Yang (Chime PM)——markdown 写 PRD → 终端 `claude` → 20 分钟跑出可点击 prototype → Slack 录屏

## C.2 维度 2：Eval 设计与执行

| 段位 | 标志 |
|---|---|
| Apprentice | 知道 "Eval 集" 是什么；能写 10 条 golden set；能跑 OpenAI Evals / promptfoo 教程 |
| Journeyman | 设计 ≥50 条 golden set + 通过线 + judge prompt；搭 LLM-as-Judge 并对齐校准；区分 regression / frontier eval；给 PRD 写 5 维 eval 章节 |
| Master | 搭独立 Eval 团队；用 Anthropic 95% CI 方法；用 Inspect AI 写企业级 eval pipeline；公开输出 eval 方法论 |

**参考标杆**：Hamel Husain / Shreya Shankar

## C.3 维度 3：成本与商业敏感度

| 段位 | 标志 |
|---|---|
| Apprentice | 知道 GPT / Claude 各模型价格；能算单次对话 token 数 |
| Journeyman | 给 CFO 算"月 token 预算 + 单用户成本 + 毛利率"；识别 token 账 5 类漏算；用 Vellum / Finout / Helicone；讲 ICONIQ 数据 |
| Master | 30 分钟内给出新需求成本量级（误差 <30%）；设计 prompt caching 节省 90%；识别 a16z 数据；给 CFO/CEO 做 unit economics 模型 |

## C.4 维度 4：合规与边界设计

| 段位 | 标志 |
|---|---|
| Apprentice | 知道 OpenAI Model Spec / Anthropic RSP；知道 Air Canada / Klarna / DPD / McDonald's 4 案例 |
| Journeyman | 用 Microsoft RAI 2D 矩阵评估；识别 Stanford 法律 AI 17/33/43% 基线；用 PromptArmor / Lakera 红队；写 PRD 合规章节 |
| Master | 讲行业"AI 在医疗/金融/法律边界"；读 Stuart Russell / Bengio 的 Provably Beneficial AI；识别 Apollo / Redwood 研究含义；公开 thought leadership |

## C.5 维度 5：协作语言

| 段位 | 标志 |
|---|---|
| Apprentice | 听懂工程师讲 prompt / RAG / agent / tool use；给老板讲"AI 不是万能"3 个边界 |
| Journeyman | 跟工程师讨论 retrieval 架构 / chunking / re-ranking；给老板做 3 框架对齐（成本/风险/ROI）；给 CFO 算 unit economics；给设计师讲 4 类 antipatterns |
| Master | 给业内大公司做咨询；给 CEO/CFO 演示 "AI Native 4 阶段路线图"；用 Marty Cagan 4 风险跟 leadership 对齐 |

**参考标杆**：Cat Wu / Kevin Weil (OpenAI CPO)

## C.6 维度 6：行业判断力

| 段位 | 标志 |
|---|---|
| Apprentice | 关注 Lenny / Sachin Rekhi / Hamel；知道 Anthropic / OpenAI / Google DeepMind / Cursor / Notion 主要产品 |
| Journeyman | 追踪 Latent Space / Stratechery / Pragmatic Engineer / a16z；区分 Sequoia / a16z / Bessemer 风投框架；用 Stanford HAI Index 数据校准；读 5 篇经典论文 |
| Master | 公开 thought leadership（公众号 ≥10K 粉 / X ≥10K followers）；预测 12-24 个月产品形态变化；给 VC / 媒体做评论；给业内大会做 keynote |

**参考标杆**：Lenny / swyx / Sarah Guo / Pat Grady (Sequoia)

## C.7 6 维路线图综合矩阵

| 维度 | Apprentice | Journeyman | Master | 升级时间 |
|---|---|---|---|---|
| 1. Vibe Coding | 跑教程 | 30 分钟独立验证 | 独立做 internal tool | 0.5 → 2 年 |
| 2. Eval | 10 条 golden set | 50+ set + judge | 企业级 pipeline | 0.5 → 2 年 |
| 3. 成本 | 知道价格 | 30 分钟估算 + 监控 | unit economics 模型 | 1 → 3 年 |
| 4. 合规 | 知道 4 案例 | RAI matrix 评估 | thought leadership | 1 → 3 年 |
| 5. 协作 | 听懂技术词 | 三方对齐 | 给老板咨询 | 1 → 3 年 |
| 6. 行业判断 | 看 Lenny | 追 5 newsletter | 行业预测 + keynote | 2 → 5 年 |

**整体段位映射**（对应原稿 26 篇 L1-L4）：
- **L1 AI 用户级**：6 维都在 Apprentice
- **L2 AI 产品参与者**：6 维有 3 个 ≥ Journeyman
- **L3 AI 产品架构师**：6 维有 5 个 ≥ Journeyman + ≥2 Master
- **L4 AI 时代产品思想者**：6 维有 4 个 Master + 持续公开输出 ≥2 年

## C.8 6 维自检卡

```
┌─────────────────────────────────────────────────┐
│  AI PM 6 维能力自检卡（v1.0）                   │
│                                                 │
│  评分：A=Apprentice / J=Journeyman / M=Master   │
│                                                 │
│  1. Vibe Coding 实战      [  ]                 │
│  2. Eval 设计与执行       [  ]                 │
│  3. 成本与商业敏感度      [  ]                 │
│  4. 合规与边界设计        [  ]                 │
│  5. 协作语言              [  ]                 │
│  6. 行业判断力            [  ]                 │
│                                                 │
│  对照 L1-L4：                                   │
│  6A = L1 / 3J+3A = L2 / 2M+3J+1A = L3 /        │
│  4M+2J + 公开输出 2 年 = L4                    │
│                                                 │
│  每季度自评 1 次——升级最慢的维度优先补       │
└─────────────────────────────────────────────────┘
```

---

# 附录 · AI PM 必读 / 必听 / 必看资源清单

## 附录 1 · 必读 30 篇

### Tier 1（每个 AI PM 必读）
1. Lenny × Hamel & Shreya "Writing Good Evals" 系列
2. Mike Krieger Lenny Podcast "Product Note over PRD"
3. Aparna "Prompt sets are the new PRDs"
4. Cat Wu "Prototypes over PRDs"
5. Sachin Rekhi "AI Prototyping Mastery Ladder"
6. Marty Cagan SVPG 2025 "Product Discovery in AI Era"
7. Boris Cherny "100% of my code is written by Claude Code"
8. Kevin Weil "Rolling Bets" Roadmap
9. Anton Osika (Lovable) "60 days $10M ARR with 15 people"
10. Scrum.org "Definition of Done for AI Agents"

### Tier 2（6 个月内读完）
11. Stanford HAI AI Index Report 2026
12. a16z 2025 企业 LLM 100 CIO 调研
13. MIT NANDA "State of AI in Business 2025"
14. Sequoia "Act o1 + Act Three"
15. Bessemer "Supernovas vs Shooting Stars"
16. a16z AI Canon
17. Conviction (Sarah Guo + Elad Gil) "Software 3.0"
18. Greylock 企业 AI 三层价值论
19. Notion × Braintrust Dual-track Eval
20. OpenAI GPT-4o sycophancy postmortem

### Tier 3（年度精读）
21. Stratechery (Ben Thompson) AI 全年系列
22. swyx (Latent Space) "AI Engineer" 系列
23. Dylan Patel (SemiAnalysis) GPU 经济
24. Pragmatic Engineer AI 工程师工作流
25. Dario Amodei "The Adolescence of Technology"
26. Yoshua Bengio International AI Safety Report 2025
27. Stuart Russell "Human Compatible"
28. Apollo Research 欺骗对齐实证
29. Microsoft Responsible AI Standard v2
30. Partnership on AI Real-Time Failure Detection

## 附录 2 · 必听 Podcast 10 个

| # | Podcast | 主理人 | 适合谁 |
|---|---|---|---|
| 1 | Lenny's Podcast | Lenny Rachitsky | 所有 PM |
| 2 | Latent Space | swyx + Alessio | AI Engineer 视角 |
| 3 | No Priors | Sarah Guo + Elad Gil | VC 视角 |
| 4 | Acquired | Ben Gilbert + David Rosenthal | 公司战略 |
| 5 | Sequoia Training Data | Sequoia 团队 | 模型公司 |
| 6 | 20VC | Harry Stebbings | 融资 / 估值 |
| 7 | Hard Fork | Casey Newton + Kevin Roose | 社会影响 |
| 8 | Stratechery (Sharp Tech) | Ben Thompson | 战略竞争 |
| 9 | The Pragmatic Engineer | Gergely Orosz | 工程实践 |
| 10 | Product Compass | Miqdad Jaffer | AI PRD 实操 |

**听播建议**：每周 3-5 episode（约 8-15 小时），听完写 200 字 take。

## 附录 3 · 必看大会

### 全球 Tier 1
1. **AI Engineer World's Fair**（swyx 主办，年度 1 次旧金山，AI Engineer + AI PM）
2. **mtpcon**（Mind the Product，年度 4 次，全球最大 PM 社区年会）
3. **NeurIPS / ICML / ICLR**（看一手 paper）
4. **Anthropic Build with Claude Conf**
5. **OpenAI DevDay**

### 中国 Tier 1
6. 极客时间 AICon
7. AI 产品经理大会（PMTalk / 起点学院）
8. WAVE SUMMIT（百度飞桨）
9. **WAIC 世界人工智能大会（上海）**——老板对齐风向标
10. Trae / 通义灵码用户大会

## 附录 4 · 必读 5 经典论文

1. **"Attention Is All You Need"**（Vaswani et al., 2017）—— Transformer 起源
2. **"Language Models are Few-Shot Learners"**（GPT-3, Brown et al., 2020）—— LLM 涌现起点
3. **"Chain-of-Thought Prompting"**（Wei et al., 2022）—— CoT 推理范式
4. **"Training language models to follow instructions with human feedback"**（InstructGPT/RLHF, 2022）—— RLHF 对齐
5. **"Constitutional AI: Harmlessness from AI Feedback"**（Bai et al., 2022）—— Anthropic 对齐

**读法**：看摘要 + figures + introduction；配 Karpathy / 3Blue1Brown / Yannic Kilcher 解读视频。

## 附录 5 · 必学课程

### Tier 1
1. **Hamel × Shreya "AI Evals for Engineers and PMs"**（Maven $2000+）
2. **Sachin Rekhi AI Prototyping Mastery**（Reforge $2000/年）
3. **Reforge AI Product Management Track**

### Tier 2
4. Mind the Product Workshops
5. Product School AI PM Certificate
6. First Round Review 长文

### 中国
7. 极客时间 AI PM 实战课
8. 起点学院 AI PM 训练营
9. 三节课 AI 应用 PM 课

---

# 模块 D · 设计依据 & 批判性自评

## D.1 整体设计依据

**3 模块对应原稿 3 篇 + 5 附录是横向延伸**——每篇有清晰"配套清单"+ 30 篇必读 / 10 podcast / 大会 / 论文 / 课程是 PM 持续学习的"地图"。

**反共识设计点**：
1. **6 塌陷点不是"通用 PM 痛点"**——是"传统 PM 转 AI PM specific 路径上的崩塌点"
2. **3 种模式不是"按规模分"**——是"按组织哲学分"
3. **6 维能力不是"PM 通用能力"**——是"AI 时代特有的差异化能力"
4. **3 段位借用 Sachin Rekhi Apprentice/Journeyman/Master**——但 Rekhi 原版 15 个细分技能，本工具浓缩到 6 维

## D.2 数据更新声明（2026-05-21 调研时点）

| 数据点 | 原稿口径 | 2026-05 实际 |
|---|---|---|
| **Lovable 团队规模** | 18 人（2025-Q3） | 146 人（2026-02）→ ~517 人（2026-Q2） |
| **Lovable ARR** | $17M（2025-Q3） | $400M（2026-02） |
| **Lovable 人均 ARR** | ≈$100 万 | ≈$2.7M |
| **Stanford HAI AI Index** | 年度版 | **2026 版已发布**（4 月） |

**Stanford HAI 2026 关键发现**：
- LLM 在 SWE-bench Verified 上从 60% → 接近 100%（一年内）
- 生成式 AI 3 年内全球渗透率 53%（快于 PC / 互联网）
- 企业组织 AI 采纳率 88%
- 22-25 岁初级软件工程师岗位下降 ~20%
- US-China 模型差距收窄到 2.7 个百分点
- 营销 +72% / 软件开发 14-26% / 客服 14-26% 生产力提升

## D.3 批判性自评（已知不足）

### 6 塌陷点的局限
- ❌ 没覆盖 ToB 大客户场景（客户期望管理 / 合同 SLA）
- ❌ 没覆盖 0-1 年新人
- ❌ 没量化"打几个 ✅ 算合格"——A.7 给 3/4-5/6 三档但缺数据阈值

### 3 种 AI Native 模式的局限
- ❌ 没覆盖中国独有的"算法工程师主导"模式（字节 / 阿里 / 腾讯）
- ❌ Anthropic 数据偏旧（~2000 人口径，2026 实际 3000+）
- ❌ 没有"5 年后预测"模式

### 6 维能力路线图的局限
- ❌ 维度划分有重叠（Vibe Coding 和协作语言部分重叠）
- ❌ 缺 "ToC 增长" 维度
- ❌ 段位标志靠主观判断
- ❌ Master 段位"持续公开输出 2 年"门槛过高

### 必读 / 必听 / 必看的局限
- ❌ 30 篇必读偏英文，中文 AI PM 优质内容缺席
- ❌ 必听 podcast 全英文
- ❌ 必看大会偏美国

## D.4 工具包升级路径

### v1.1（2026-08，3 个月后）
- 加 "模式 4：中国大厂算法 + 产品 + 业务模式"
- 加 5 篇中文必读 + 3 个中文 podcast
- 重写"打 ✅ 阈值"基于 100 个 AI PM 调研数据
- 增加 "ToC 增长" 维度作为可选第 7 维

### v2.0（2026-11，6 个月后）
- 加 "AgentOps PM" 章节
- 加 "Context Engineering" 维度
- 重评 Vibe Coding 工具横评

### v3.0（2027 年初）
- 完全重构 6 维 → 可能变 8 维
- 加入 "AGI 临近期 PM 工作流"

## D.5 配套资产清单

**第 01 篇配套**：✅ 6 塌陷点自检（A.7）+ 5 类 bad case 修复对照（A.5）
**第 25 篇配套**：✅ AI Native 3 种模式自检（B.5 决策树）+ 老板 4 阶段转型路线图 + ⏳ 新岗位 JD 模板（待 v1.1）
**第 26 篇配套**：✅ 4 层次 / 6 维自评（C.8）+ ⏳ 4 动作每日打卡（v1.1）+ 26 篇索引 + ⏳ 跳槽议价话术（v1.1）

## D.6 一句话总结

**这个工具包不是 "AI PM 应该知道什么的清单"——是 "AI PM 应该走到哪里的地图"**。

- 模块 A 告诉你**当前在哪**（6 塌陷点）
- 模块 B 告诉你**目标公司在哪种组织**（3 种 AI Native）
- 模块 C 告诉你**3 年后能走到哪**（6 维 × 3 段位）
- 附录告诉你**用什么走**（资源清单）

**反身性原则**：每季度自评一次，每年迭代一版。AI 时代没有"一劳永逸的工具"。

---

## 文末微信钩子

```
─────────────────────────────
📦 配套资源 · 第 01 + 25 + 26 篇 合订

加我微信 **CYW960325**（备注「专栏-成长」），免费领：
✓ 6 塌陷点自检卡（PDF 单页打印版）
✓ AI Native 3 种团队模型决策树
✓ 6 维能力路线图自评 Excel
✓ AI PM 必读 30 篇 + 必听 10 podcast + 必看 5 大会

【3 种格式任选】
📄 PDF / 🔗 腾讯文档 / 💻 GitHub Pages
─────────────────────────────
```

---

> 蔡逸雯 · 8 年 QE → AI PM · 公众号「蔡逸雯」
> 工具版本 v1.0 · 最后更新 2026-05-21
> 下次迭代：2026-08（v1.1，加中文资源 + 模式 4 + ToC 维度）
> CC-BY-NC 4.0 · 转载请注明出处
