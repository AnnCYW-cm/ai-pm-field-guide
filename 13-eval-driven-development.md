# 13 · Eval-Driven Development——让评估集驱动整个开发流程

> 第一季《AI 时代 PM 工作流重构》· 第 13 篇 · 第三部分 PRD（专栏硬通货）
> 预估字数：5000

---

第十二个"不以为然"——

**90% 的团队还在「先写代码后补 eval」**。

不是工程师懒。是大多数团队**以为"eval 是上线前的验收动作"**——结果代码写到一半发现"什么算做完了"没人说得清，PM 和工程师互相甩锅 3 周。

读完这一篇你会知道——**EDD（Eval-Driven Development）不是测试方法的改变，是开发哲学的改变**。

第 12 篇讲了"操作层"——怎么写 Eval 章节。
**这一篇讲"哲学层"——怎么用 Eval 驱动整个开发流程**。

---

## 上半篇 · workflow

### EDD 三步走

#### Step 1：先定义 eval（不是先写代码）

传统流程：写 PRD → 写代码 → 测试 → 上线
EDD 流程：**写 PRD → 写 eval → 写代码 → 跑 eval → 上线**

**eval 在代码之前**。

**Anthropic 官方建议**（写进了文档级别的背书）：

> "We recommend practicing eval-driven development: **build evals to define planned capabilities before agents can fulfill them**, then iterate until the agent performs well."

翻译过来：先写 eval 定义"做完了是什么样"——然后让 agent / 模型迭代到达标。

这个顺序的反共识在于——**eval 是设计工具，不是验证工具**。

#### Step 2：用 eval 定义「做完了」

EDD 的核心是用 eval 倒逼 PM 想清楚需求。

**如果 PM 写不出 eval——说明 PM 没想清楚"什么是好"**。

例：
- 模糊需求："让 AI 客服更聪明"
- EDD 反问："eval 维度是什么？通过线是多少？"
- PM 被迫想清楚："工单解决率 ≥ 90% / 平均轮次 ≤ 5 / 用户满意度 ≥ 4.2"
- **现在这才是一个可执行的需求**

EDD 把"模糊的产品想法"变成"可测量的工程目标"。

#### Step 3：用 eval 驱动迭代

代码写完 → 跑 eval → 没达标 → 改 prompt / 改架构 / 改模型 → 跑 eval → 达标 → 上线

**关键差异**：传统是"按需求实现"，EDD 是「**按 eval 收敛**」。

工程师不需要 PM 频繁打扰说"这个 case 不对"——他自己跑 eval 就知道。
PM 不需要工程师反复问"这个改完算不算好"——eval 通过线说了算。

整个开发流程**异步化**——PM 写 eval、工程师改实现、CI 跑 eval 给反馈。

### EDD 在团队里的落地

```
PM ─────► 写 PRD + eval 集（"什么是做完了"）
   │
   ├─► AI Engineer ─► 选模型 / 写 prompt / 集成工具
   │      │
   │      └─► 跑 eval（CI 自动）
   │            │
   │            ├─► 通过 → 进入下一阶段
   │            └─► 不通过 → 改实现 → 重跑 eval
   │
   └─► Eval 工程师 ─► 维护 eval 集 / 写 LLM-as-judge / 训练 grader
          │
          └─► 持续扩展 eval（新 bad case → 新 eval case）
```

**三角协作**：PM-AI Engineer-Eval 工程师替代传统 PM-RD-QA。

详见第 25 篇 AI Native 团队搭建——但这里先记住一个核心：**Eval 工程师正在成为独立工种**。Anthropic / OpenAI 在公开招 Evals 相关 EM，base 区间到 $300K+。Netflix 招 "Software Engineer L4/L5, LLM Evaluation & Infrastructure"。**国内还在用"AI 测试工程师"代称，但本质是同一件事**。

### EDD 不适用的场景

EDD 不是银弹。3 类场景不适用：

#### 不适用 1：极早期探索
能力边界还没摸清。这时候你不知道写什么 eval——因为你都不知道模型能做什么。

**应对**：先做 1 周「能力探针」（详见第 3 篇），跑模型边界。摸清楚之后再写 eval。

#### 不适用 2：纯创意场景
比如"让 AI 写一首打动人的诗"——eval 标准本质是主观的。

**应对**：用 A/B 测试 + 用户反馈代替自动 eval。但**核心约束**（不能写黄、不能写暴力、押韵正确）必须有 eval。

#### 不适用 3：上线前临时补
"我们快上线了，先把 eval 补一下"——这不是 EDD，是 eval 事后补丁。

**真正的 EDD 是 eval 在代码之前**。事后补丁是 evals as documentation，不是 evals as development。

---

## EDD 三步走流程图

```
      PM 想做一个 AI 功能
              │
              ▼
   ┌─── Step 1：写 Eval ───┐
   │  - 评估维度 3-5 个    │
   │  - case 数 20-50 起步 │
   │  - 通过线设清楚       │
   └──────────┬─────────────┘
              │
              ▼
       PM 写不出 eval？
       ├─ 是 → 需求没想清楚，回去想
       └─ 否 → 继续
              │
              ▼
   ┌─── Step 2：设计能力 ───┐
   │  - 工程师选模型/路径    │
   │  - 写第一版 prompt     │
   └──────────┬─────────────┘
              │
              ▼
   ┌─── Step 3：跑 Eval ───┐
   │  - CI 自动跑          │
   │  - 通过 → 上线        │
   │  - 不通过 → 改实现    │
   └─────────────────────────┘
```

---

## EDD vs TDD 对照表

| 维度 | TDD | EDD |
|------|-----|-----|
| 测什么 | 代码功能（确定性）| 模型能力（概率性）|
| 通过标准 | 全部 pass / fail | 通过率 ≥ X%（分布）|
| Eval 形态 | 单元测试代码 | YAML / JSONL + grader |
| 失败原因 | 代码 bug | prompt 不对 / 模型不行 / 数据偏 |
| 修复方法 | 改代码 | 改 prompt / 换模型 / 补数据 |
| 迭代节奏 | 写代码 → 写测试 → 跑 | 写 eval → 写实现 → 跑 |
| 验证未知 | TDD 验证已知逻辑 | EDD 定义未知能力 |

**最关键差异**：**TDD 是验证已知，Eval 是定义未知**。

TDD 假设"我知道代码该做什么，写测试验证它真的做了"。
EDD 假设"我不知道模型能做到什么程度，写 eval 定义我希望它做到什么"。

---

## 下半篇 · engineering reality

### EDD 的工程现实：eval 是「活的」

很多团队第一次做 EDD 时把 eval 当一次性产物——上线前写完，上线后不管。

**这是把 EDD 做成"上线前补 eval"——那不是 EDD，是事后补丁**。

真正的 EDD：eval 跟随产品演化、持续维护。

每次新 bad case 出现 → 补进 eval 集 → 下次发版时跑回归。
每次模型升级 → 跑 eval 验证不退化 → 决定要不要切换。
每次 prompt 改动 → CI 跑 eval → 自动判断是否合并。

Hamel Husain "Field Guide to Rapidly Improving AI Products" 给的工业级 SOP：

> "每改一次至少手看 20-50 条 trace；写自定义数据查看器（不要用 dashboard）；错误聚类→定义失败模式；每个失败模式写一条 eval；把 eval 集做成 CI 卡口。"

### QA 思维倒置：EDD 和传统 QA 的根本区别

**8 年做软件质量工程的视角看**——

EDD 其实是 QA 思维的**倒置版本**。

| 维度 | 传统 QA | EDD（QA 思维倒置）|
|------|--------|------------------|
| 测什么 | 已知逻辑（验证代码正确）| 未知能力（定义模型表现）|
| 何时写 | 代码之后 | **代码之前** |
| 写给谁 | QA 自己 | **PM + 工程师 + Eval 工程师**共用 |
| 目标 | 找 bug | **倒逼需求想清楚** |
| 反馈对象 | 工程师 | **PM 自己** |

传统 QA："你写错了"——指着工程师说。
EDD："你想清楚了吗？"——指着 PM 自己说。

**EDD 把 QA 从"挑刺者"变成"需求收敛者"**。

这是为什么 Anthropic 把 Eval 团队定位为"**bridge model capability and product experience**"——产品和研究团队之间的桥梁，不是事后审查者。

### 把 EDD 做成「事后补丁」的常见模式

业内反复出现的失败模式——

团队接受了 EDD 概念，但落地变形：
- 第 1 周：PM 写需求 → 工程师开发
- 第 4 周：上线压力大，开始写 eval
- 第 5 周：跑 eval 发现 60% case 通不过
- 第 6 周：紧急改 prompt → 改 case → 再跑 → 再改

**这不是 EDD，是"eval as documentation"**——eval 只是上线前补的文档，不是开发驱动力。

正确的 EDD：第 1 周 PM 写 eval，第 2 周工程师按 eval 开发，**第 3 周如果 eval 通过率不达标 → 是工程师改、不是 PM 改**。

---

## Hamel 「EDD 不是新发明」的反共识

EDD 这个术语的源头——

**Hamel Husain（2024-10）**：

> "**EDD was always front and center pre-generative AI. Ex: nobody cares about your fraud/churn/forecasting model if it's not accurate. This is missing with most LLM products. But the best practices and playbooks are there.**"

翻译：**EDD 在生成式 AI 之前就是 ML 圈核心常识**。没人会关心一个不准的欺诈/流失模型。LLM 产品圈把这事丢了，但最佳实践本来就在。

**关键定性**：EDD 不是新词，是从传统 ML 工程移植到 LLM 产品的旧实践。"新"的只是 LLM 圈忘了。

---

## BMAD / Spec-Driven Development 的精华

EDD 不是唯一的 AI 开发方法论。还有两个值得了解：

### BMAD-METHOD

⚠️ 重要订正：BMAD 全称是 "**Breakthrough Method of Agile AI-Driven Development**"（bmad-code-org/BMAD-METHOD GitHub repo 官方 README）。

核心实践：
- 把 LLM 拆成多个专业化 Agent 角色（Architect / PM / Developer）
- 每个角色有受限上下文
- Developer Agent 被定义为 "obedient craftsman"——发现需求与架构冲突时**必须 halt and report**

**与 EDD 的关系**：BMAD 偏「多 Agent 协作流程」，EDD 偏「质量保障」。可以组合使用——BMAD 拆角色 → 每个角色用 EDD 收敛。

### Spec-Driven Development（GitHub Spec Kit）

2025-09 开源的方法论：

> "Specifications become executable, directly generating working implementations rather than just guiding them."

流程：`/specify` → `/plan` → `/tasks` → `/analyze` → 由 Claude Code / Copilot / Gemini CLI 执行。

**与 EDD 的关系**：Spec-Driven 偏「代码生成」，EDD 偏「质量评估」。**三者组合**：
- BMAD 拆角色
- Spec Kit 写规格
- EDD 验质量

这是 2026 年最先进的 AI 开发方法论组合。

---

## 给你的可执行清单

#### 动作 1：你下一个项目按 EDD 三步走顺序做
- Step 1 先写 eval（不是写 PRD）
- Step 2 工程师按 eval 设计实现
- Step 3 CI 跑 eval 驱动迭代

#### 动作 2：每个新 bad case 立刻补进 eval 集
- 不要"等下次再补"
- 当天补完，下次 release 跑

#### 动作 3：把 eval 集做成 CI 卡口
- PR 自动跑 eval
- 分数低于基线 → block 合并
- 这是工程化的 EDD

#### 动作 4：用 EDD 把"模糊需求"逼出来
- 业务方说"让 AI 更聪明" → 反问"eval 维度是什么"
- 业务方说"用户满意度提升" → 反问"通过线是多少"
- 写不出 eval = 需求没想清楚

---

## 反共识金句

- **"Hamel Husain 一句话戳穿真相：'EDD 不是新发明，是 LLM 圈忘了的 ML 老规矩。没人会关心一个不准的欺诈模型——但 LLM 产品圈居然容忍。'"**
- **"EDD 跟 TDD 的根本差异：TDD 测确定性（pass/fail），EDD 测概率分布。把 LLM 当函数来测——这就是入门即翻车的根因。"**
- **"QA 思维没消失，它被倒置了——传统 QA 指着工程师说'你错了'，EDD 指着 PM 自己说'你想清楚了吗'。"**

---

## 写在最后

这一篇讲了 EDD 哲学。下一篇我们回到操作层，讲 PRD 第 6 章——**Bad Case 分级与降级策略**。

Bad Case 不是上线后处理，是 PRD 阶段就要分级和写降级策略。**Microsoft Responsible AI Standard v2 + Anthropic ASL 四级 + OpenAI Model Spec 三层——3 套业内标准都拆开**。

下一篇见。

---

> **本文配套资产**：EDD 三步走流程图 + EDD vs TDD 对照表 + BMAD/Spec-Driven 组合指南（付费读者解锁）
> **下一篇预告**：14 · Bad Case 分级与降级策略写进 PRD
> **反馈 / 加入读者群**：欢迎在公众号「蔡逸雯」留言
