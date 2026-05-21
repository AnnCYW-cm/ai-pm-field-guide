# 25 · AI Native 团队的真实形态——3 种主流组织模式

> 第一季《AI 时代 PM 工作流重构》· 第 25 篇 · 第七部分 组织
> 预估字数：5000

---

第二十四个"不以为然"——

**90% 的老板想用 AI 「替代员工」**。

不是老板贪婪。是大多数老板 **以为"AI Native = 用 AI 替代人 = 砍人省成本"**——结果照着 Klarna 走，先冻招 + 让客服自然流失，再 2025 年公开承认"AI 缺乏共情"重新招人，**估值反而吓掉一截**。

读完这一篇你会知道——**AI Native 不是"AI 替代人"，是「人 × AI = 5-10 倍产能」的新组织形态**。业内 3 种主流模式各有适用场景。

**这一篇是 B 端漏斗的核心**——你公司老板看完会主动找你聊。

---

## 上半篇 · workflow

### 业内 3 种 AI Native 组织模式

#### 模式 1：Anthropic / OpenAI 的「Research-heavy」结构

**特征**：
- 公司 35% 是 Research 人员
- 65% 是 Engineering + Product
- 几乎没有"传统 BD / 销售 / 运营"角色（人均 ARR 极高）

**Anthropic 公开口径（2025）**：
- 公司规模快速扩张中（数千人量级，具体口径以官方为准）
- CEO Dario 在公开访谈里提到 Research 团队占比约 1/3 以上
- 剩余大头是 Engineering + Product + GTM
- 人均 ARR 极高（业内顶级）

**适用场景**：模型公司 / 前沿 AI 研究

**不适用**：99% 的应用层公司

#### 模式 2：Notion / Cursor 的「精英 Eng-heavy」结构

**特征**：
- 工程师占公司 50%+
- PM 团队精干（每 10-20 工程师 1 PM）
- 独立 Eval 团队（新角色！）
- 营销 / 增长团队小但 PLG（Product-Led Growth）

**Notion 公开口径**：
- 核心 AI 团队人数较少（~100 工程师规模团队中的一小部分专攻 AI）
- 独立 Eval 团队（业内最早设立的样板之一）
- PLG 驱动，营销团队极小
- 用 dual-track eval（regression + frontier）让特定 workflow 提速近 10 倍（来自 Notion × Braintrust 案例）

**Cursor 公开口径（2025-Q3 快照）**：
- 工程团队约 100 人量级
- ARR 已到 $1B 量级（持续扩张中）
- 人均 ARR 远高于传统 SaaS

**适用场景**：AI 应用层 SaaS / 开发者工具

**核心打法**：PLG + 高质量产品 + 工程极致

#### 模式 3：Lovable / 极小团队的「Founder-led + AI」结构

**特征**：
- 5-20 人总团队
- 创始人 + 顶尖工程师 + 1-2 PM
- 重度依赖 AI 工具（Claude Code / Cursor）做开发
- 用户运营靠社区 + KOL

**Lovable 公开口径（2025-Q3 快照）**：
- 当时约 18 人公司，~$17M ARR
- 人均 ARR 接近 $100 万（不输 Anthropic 早期）
- 创始人 Anton Osika 公开说"我们的 PM 数量是 0，工程师都在做 PM 的事"
- 注：Lovable 增长极快，团队规模和 ARR 半年内可能翻几倍——以最新口径为准

**Microsoft 公开口径**：
- 内部工程师全员铺 Copilot
- Satya Nadella 在 2025-04 财报会公开说 "as much as 30% of our code is now written by AI"

**适用场景**：早期 startup / 独立开发者 / 小型 AI 产品

**核心打法**：极致少人 + 极致 AI 杠杆

---

## 老板真正该问的问题

不是"我要砍多少人"——是"**我要建什么样的人**"。

### 应该转型的 4 类角色

#### 角色 1：传统初级 PM → AI PM

- 原来工作：写 PRD / 跑用研 / 推进项目
- 新工作：写 spec + eval case / 看 trace / 跑 prompt 实验

#### 角色 2：传统软件工程师 → AI Engineer

- 原来工作：写代码 / 修 bug
- 新工作：写代码 + 用 AI 写代码 + 写 eval + 做 prompt 工程

#### 角色 3：QA / 测试 → Evaluator

- 原来工作：手工测试 / 自动化测试
- 新工作：设计 eval 集 / 做 LLM judge 对齐 / 标注 bad case

#### 角色 4：客服 / 运营 → AI 训练师

- 原来工作：回答用户 / 标记问题
- 新工作：标 bad case / 维护 RAG 知识库 / 调 prompt

### 真正应该砍的 1 类角色

只有 1 类——**纯重复劳动型岗位**。

例：
- 数据录入（已被 OCR + LLM 替代）
- 简单分类（已被 LLM 替代）
- 模板化生成（已被 LLM 替代）

但这类岗位**总数不多**——通常占公司 5%-10%。

### 真正应该新增的 3 类角色

#### 新角色 1：Eval Engineer / Evaluator

**职责**：
- 设计 eval 集
- 维护 LLM judge
- 跟踪 bad case 分布

**Notion 已设独立团队**——这是业内最有共识的新角色。

#### 新角色 2：Prompt Engineer / AI Engineer

**职责**：
- 写 system prompt
- 设计 few-shot examples
- 优化 RAG / tool use 架构

**比例**：每 3-5 工程师配 1 个

#### 新角色 3：AI Ops / LLMOps

**职责**：
- 维护监控 dashboard
- 配置 hard cap / 灰度
- 应对 bad case 紧急事件

**比例**：每 50 工程师配 1 个

---

## 下半篇 · engineering reality

### Klarna 教训的真正含义

**2024-02**：Klarna CEO Siemiatkowski 公开宣布 "AI replaced the equivalent of 700 customer service agents."（注：Klarna 是用 hiring freeze + 自然流失让人员下降，不是一次性砍 700 人）

**2025**：CEO 公开承认"AI 缺乏共情，复杂问题处理不了"，**重新开放招聘，转 hybrid 模型**。

这个事件的真正含义不是"AI 不行"——是「**AI Native 不等于减员**」。

Klarna 的 AI Native 转型本可以这样做：
- 不要冻结招聘
- 让客服每人用 AI 工具，**产能提升 3-5 倍**
- 实际效果：同样人数服务 3-5 倍需求量
- 业务扩张时，**比竞品更快**

**实际做法（争议）**：招聘冻结 + 自然流失 → 客户体验下降 → 重新招人 → 上市前公关压力

**更稳的做法**：保留客服 → 武装 AI 工具 → 产能 3-5 倍 → 业务扩张时优势

### 「AI 替代人」vs「AI 武装人」的本质区别

| 维度 | AI 替代人 | AI 武装人 |
|------|---------|---------|
| 团队规模 | 减员 50%+ | 不减或少减 |
| 短期成本 | 显著降低 | 持平或略升 |
| 长期产能 | 显著降低（30%-50%）| 显著提升（3-5 倍）|
| 客户体验 | 风险大（Klarna / DPD）| 提升 |
| 法律风险 | 高（Air Canada）| 低 |
| 公关风险 | 高 | 低 |
| 业务扩张速度 | 慢（需要重新招人）| 快（用现有人扩张 5 倍）|

**反共识真相**：**AI Native 的核心打法是用 AI 让团队产能爆炸式提升**——不是省人，是**让 100 人干 500 人的活**。

### Anthropic Cat Wu 的 Product Note 核心观点

Anthropic 产品负责人 Cat Wu 在 2025 年 Product Note 公开说：

> "**Prototypes over PRDs**"
>
> "**Spec-first**"
>
> "**Daily user sentiment loop**"

翻译过来——
- 不要写 PRD，直接做 prototype（用 Claude Code 做）
- 不要写需求文档，写 spec（输入 / 输出 / 评估标准）
- 每天看用户 sentiment（不要等数据）

**这就是 AI Native PM 的工作方式**——和传统 PM 完全不同。

---

## 老板的转型路线图

帮老板理解"我们公司怎么变"——给他一条可执行的路线图：

### 第 1 阶段（1-3 月）：试点

- 选 1 个团队（如客服）做 AI 武装
- 不裁人，让团队用 AI 工具
- 观察产能变化 + 客户满意度变化

### 第 2 阶段（3-6 月）：扩展

- 把试点经验推到 2-3 个团队
- 新招 1 个 Eval Engineer
- 新招 1 个 Prompt Engineer
- 让 PM 和工程师都开始用 Claude Code / Cursor

### 第 3 阶段（6-12 月）：组织重塑

- 招 AI Ops 负责整体监控
- 把 QA 团队转型为 Evaluator
- 业务扩张时**优先用 AI 提产能**，不是新招人

### 第 4 阶段（12-18 月）：成熟

- 整个公司形成"人 × AI = 5-10 倍产能"的运行模式
- 人均 ARR 显著高于竞品
- 业务扩张快于行业

**关键**：整个路线图**没有"砍人"步骤**——这是 PM 帮老板看清的核心。

---

### AI Native 团队的下一个形态——Agent Ops 而非 Human Ops

上面 3 种模式 + 4 阶段路线图是**当下**的 AI Native——人 × AI = 5-10 倍产能。但要诚实跟读者讲一件事——**12-24 个月后会出现第 4 种模式：PM 不再管人，PM 管理一组 Agent**。

业内 2026 年已经在跑的信号——

**AgentOps 正在成为标准企业职能**。IBM、Red Hat、UiPath、Salesforce 在 2025-2026 全部把 AgentOps 写进官方文档——"DevOps 让软件可靠，MLOps 让模型可生产，AgentOps 让 agentic AI 可信"。

**Salesforce Agentforce Operations** 2026 年正式推出——直接把 back-office 流程交给"specialized agent 编队"，宣传语是 "without ripping and replacing existing systems"——意味着大公司不再讨论"是否换组织结构"，而是**在现有组织上叠一层 agent 编队**。

**"humans move up the stack"** 已经是业内共识口径。人留在 orchestration / strategy / exception handling 三层——**执行层 100% 由 agent 完成**。

**这不是裁员，是 PM 管理半径从 6 人放大到 6 agent + 6 人**——人没少，每个人的杠杆变大。这和本篇前面 5 数据点（AI 武装人 ≠ 裁员）完全一致，只是从「同岗位 + AI 工具」升级到「同人 + Agent 团队」。

这意味着第 4 种模式：**PM 的下属不是 4 个工程师 + 2 个设计师，是 6 个 specialist agent + 1 个 lead agent + 1 个 grader**。1-on-1 变成 trace review，OKR 变成 agent rubric。

这一篇 3 种模式 + 4 阶段先看清。但读者心里要带一条——**老板未来 18 个月真正会问的不是"AI 武装人"，是"我们什么时候开始招 AgentOps Lead"**。这一问题答得上来的 PM——下一轮 B 端 inbound 你就是 default 答案。

---

## 业内 5 个数据点（佐证 AI Native = 武装人）

### 数据点 1：Microsoft 工程师全员 Copilot

Satya Nadella 在 2025-04 财报会公开说 "as much as 30% of our code is now written by AI"——但 Microsoft **没有因此裁员**。

### 数据点 2：Notion AI 团队提速近 10 倍

核心 AI 团队人数较少 + dual-track eval，特定 workflow 提速近 10 倍（来自 Notion × Braintrust 案例）——**核心打法是产能爆炸而非人海战术**。

### 数据点 3：Lovable 18 人量级做出 $17M ARR（2025-Q3）

不是因为"AI 替代人"——是因为"AI 让每个人产能数十倍"。**小团队就能做到的事，过去需要数百人**。

### 数据点 4：Klarna 反向案例

招聘冻结 + 自然流失 → 客户体验下降 → 重新招人——证明"减员模式"在生产环境不可持续。

### 数据点 5：Cursor 100 人量级撑起 $1B ARR

人均 ARR 远高于传统 SaaS——**Cursor 不是"用 AI 替代人"，是"用 AI 让 100 人干上千人的活"**。

---

## 质量工程视角看 AI Native 团队 = 系统级生产力升级

**8 年做软件质量工程的视角**——

任何工业革命的本质都是「**生产力升级**」，不是「**裁员**」。

- 蒸汽机时代：织布工人从 100 人/小时 → 1 人/小时——但纺织业总人数**增长**了（因为需求爆炸）
- 计算机时代：会计从手工算账 → 用 Excel——但财务岗位**增长**了（因为业务复杂度爆炸）
- AI 时代：PM / 工程师 / 运营从手工 → 用 AI——**业务复杂度会再次爆炸**，需要的人**也会增加**

「**AI 替代人**」的逻辑错在哪？——**它假设业务总量不变**。

但 AI 时代业务总量会爆炸——
- 用户预期更高（要 AI 个性化、要实时响应）
- 竞争更激烈（同行都在用 AI）
- 新机会更多（AI 创造的新业务场景）

「**AI Native = AI 武装人 + 业务总量爆炸性扩张**」——这才是真相。

PM 必须帮老板看清这件事——**老板砍人 = 老板的公司被砍**。

---

## 给你的可执行清单

#### 动作 1：算清楚你公司的 AI Native 形态
- 你属于 Anthropic / Notion / Lovable 哪种模式
- 不要乱抄

#### 动作 2：给老板做"4 阶段转型路线图"
- 试点 / 扩展 / 重塑 / 成熟
- 强调"没有砍人步骤"

#### 动作 3：识别公司应该转型的 4 类岗位
- 初级 PM / 工程师 / QA / 运营
- 配套培训计划

#### 动作 4：识别 3 类新增岗位
- Eval Engineer / Prompt Engineer / AI Ops
- 给老板招聘 JD

#### 动作 5：保护要砍的人
- 只有"纯重复劳动型"该砍
- 其他人都应该转型而不是砍

---

## 反共识金句

- **"AI Native 不是 AI 替代人——是 AI 让一个人能干十个人的事。"**
- **"老板减员 = 老板的公司被减——Klarna 是教科书反面案例。"**
- **"Lovable 18 人量级做出 $17M ARR——不是因为 AI 替代了几百人，是因为 18 人 + AI = 几百人的产能。"**

---

## 写在最后

这一篇是组织段的核心——B 端漏斗的发动机。

老板看完这一篇会想——"我们公司怎么转型？"——这时候你的咨询 inbound 就来了。

下一篇是**整个第一季的终章**——

第 26 篇讲——**AI 时代 PM 的成长路径**。

从 0-2 年到 5-8 年到 8+ 年——每个阶段 PM 该做什么 / 该懂什么 / 该往哪个方向走。

也是给整个第一季 26 篇做收束——回到第 1 篇讲的"3 个范式变化"，看完整闭环。

下一篇见。

---

> **本文配套资产**：AI Native 3 种模式自检 + 老板 4 阶段转型路线图 + 新岗位 JD 模板（付费读者解锁）
> **下一篇预告**：26 · AI 时代 PM 的成长路径——终章
> **反馈 / 加入读者群**：欢迎在公众号「蔡逸雯」留言
