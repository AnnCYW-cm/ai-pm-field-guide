---
tool_id: P0-17-3
serves_essay: 17
status: ready-for-review
last_updated: 2026-05-21
version: v1.0
deliverable_formats: [markdown, pdf, notion, tencent-doc]
hours_actual: 2.5
references_pools_used: [P1.3 Cat Wu Anthropic Product Note, P1.4 Mike Krieger, P1.5 Boris Cherny 100% Claude Code, P1.7 Sachin Rekhi 3 阶梯, P1.11 Lenny Newsletter, P1.12 Dennis Yang Chime, P9.1 Latent Space, P9.10 AIE WF, P10.2 Reforge AI Product Leadership]
validation_status: "未做真 PM 测试 (n=0)；案例 3 蔡逸雯亲身案例已审改完成（2026-06-08）—— 13 套 AI PM 工具 12-15h 完成"
notes: "案例 3 已补完，第二季度找 3-5 个真 PM 做 v1.1 升级"
---

# PM × Claude Code 工作流 SOP

> 服务于第 17 篇《PM × Claude Code》配套资源 ③
> **用法**：每次启动一个 AI 需求 prototype 前，按这套 SOP 跑一遍；每月对照 3 阶梯自评一次

---

## 一、为什么需要 SOP（不是"装一下 Claude Code"就完事）

**Cat Wu（Anthropic Claude Code Head of Product，Lenny's Podcast 2026-04-23）公开**：

> "Anthropic 产品团队比所有人都快，不是因为我们更聪明——是因为我们**跳过 spec、直接 ship prototype**，让 internal 用户每 5-10 分钟在 Slack 给一条反馈。Claude Code 频道全天 24 小时每 5-10 分钟一条消息。"

**Mike Krieger（Anthropic CPO）"Product Note" 框架**：

> "我们不写传统 PRD——我们写 Product Note：3-4 段把'用户意图 + 期望结果 + 具体指标'交代清楚，然后让 Claude Code 直接出 prototype。"

但绝大多数 PM 装了 Claude Code 之后：
- ❌ 没 context 直接 `claude` 进去聊
- ❌ 一上来就要 code，没要 plan
- ❌ 跑出来的 prototype 没人 review、没人 dogfood、没 eval
- ❌ 每个需求重头开始，没有沉淀成 skill

**结果**：Claude Code 变成"高级 ChatGPT"，PM 杠杆 0 倍。

这套 SOP 解决的问题 = **把 Anthropic 内部工作流压缩成 1 人 PM 也能 follow 的 5 步**。

---

## 二、PM 用 Claude Code 的 5 步标准流程

### Step 1：准备项目上下文（耗时 10 分钟，但能省后续 80% 沟通）

**核心动作**：在工作目录建 2 个 markdown：

```
prototype-xxx/
├── product_area_context.md   # 产品/用户/业务背景
├── code_context.md            # 代码地图（如果改现有 codebase）
└── prd.md                     # Product Note（Step 2 写）
```

**`product_area_context.md` 必含 5 段**：
1. **我们是谁**：公司/产品/团队 1 段
2. **用户是谁**：3 个真实 persona 1 段（不要"目标用户是企业管理者"这种废话）
3. **当前阶段**：产品现在卡在哪里 / 这次要解决什么
4. **不要做什么**：常见误判
5. **成功长什么样**：本次 prototype 验证完，下一步是什么

**Cat Wu 原话**：让 Claude Code 一开始就有"**为什么**"+"**在哪里**"，比给它聪明的 prompt 重要 10 倍。

---

### Step 2：写 Product Note（不是 PRD），3-4 段够了

**Mike Krieger Product Note 框架**：

```markdown
# Product Note: [feature name]

## 用户意图 (Intent)
用户想做什么？为什么现在做？1 段（不超过 80 字）

## 期望结果 (Outcome)
跑通后用户能体验到什么？1 段（不超过 80 字）

## 具体指标 (Metric)
怎么判断这个 prototype 算成功？2-3 条可量化指标。
例：「30 秒内完成 / 准确率 > 80% / 同事看完愿意 demo 给老板」

## 边界 (Out of scope)
明确不做什么——避免 Claude Code 自作主张越界。
```

**关键反共识**：**Product Note ≠ PRD 简化版**
- PRD 是给工程师看的（含技术约束）
- Product Note 是给 **Claude Code + 团队 reviewer** 看的（含意图与结果）

**Cat Wu 原则**："Prototypes over PRDs"——但这不是"不要写东西"，是**用 Product Note 替代 PRD**。

写完之后让 Claude Code 先复述："Read prd.md, summarize your understanding in 5 bullets, don't write any code yet."

---

### Step 3：让 Claude Code 出 prototype（强制 plan 再 code）

**最致命的错误**：直接说 "Build it." → Claude Code 选了一个你不喜欢的技术栈跑完了 → 你要 review 200 行代码才知道不对。

**正确路径**——**强制 plan-then-execute**：

```
1) Read product_area_context.md and prd.md.
2) Tell me your execution plan in 5-10 bullets:
   - what files you'll create
   - what tech stack (specify if there are choices)
   - what's mocked vs real
   - what you're NOT doing
3) WAIT for my confirmation before writing any code.
```

PM 拿到 plan → **5 分钟 review**：
- 技术栈对吗？
- 边界对吗？
- 哪里是 mock？

确认 plan 之后再让它写 code。

**Cat Wu 反复强调**：Anthropic 内部 prototype 速度快不是因为 AI 写得快，是因为 **prototype 之前 reviewer 已经把方向锁死了，AI 不需要返工**。

---

### Step 4：PM 转身做 "Editor-in-Chief"（不是 coder）

**最常见的角色错乱**：PM 跑 Claude Code 跑着跑着开始自己改代码 → 第二天工程师看一脸懵。

**正确角色**——**PM 是主编（Editor-in-Chief），不是写手**：

| Editor-in-Chief 做什么 | 不做什么 |
|---|---|
| ✅ 看 Claude Code 输出，判断方向对不对 | ❌ 自己 debug 代码 |
| ✅ 在每个决策点（架构 / 数据流 / UI 选项）提出修改 | ❌ 自己改 React 组件 |
| ✅ 录屏给团队 dogfood，收反馈再传给 Claude Code | ❌ 自己优化性能 |
| ✅ 标"这里是 mock / 这里是真"边界 | ❌ 替工程师做技术决策 |
| ✅ 决定什么时候 stop / 验证完毕 | ❌ 把代码当生产代码维护 |

**Boris Cherny 公开**：
> "我自己自 2025-11 起 100% 代码由 Claude Code 写，我不手敲——但**每个 commit 我都 review，每个架构决策我都在场**。"

PM 版本的"100% Claude Code"：**100% 代码不你写，但 100% 决策你在场**。

---

### Step 5：留 eval 钩子（没 eval 不算 done）

**伪结束**：prototype 跑起来了 → demo 给老板看 → 进入"开发排期"流程 → 上线之后崩溃。

**真结束**——**prototype 收尾必须留 3 样东西**：

1. **5-10 条 eval set**：让 Claude Code 基于 Product Note 自动生成
2. **录屏 + 边界标注**：录 60 秒 demo，旁白说清"这里是 mock / 这里是真 / 这里准确率 ~80% 不要直接上线"
3. **handoff doc**：1 段交给工程师，说清"哪里要重写 / 哪里可以照搬 / 哪里坑过我"

**Sachin Rekhi 公开方法**（2025-11 X 帖）：
> "我每个 prototype 收尾必跑一遍 eval，否则它就只是 demo，不是 validation。**Demo ≠ Validation**——这是 PM 用 Claude Code 最容易混的两件事。"

---

## 三、Sachin Rekhi 3 阶梯 + 自评问题

| 阶段 | 名称 | 核心能力 | Claude Code 用法 | 周使用次数 |
|---|---|---|---|---|
| **Apprentice** | 学徒 | 能让 Claude Code 跑出 1 个可用 prototype | 单次客户访谈合成 / 1 个静态 prototype / 复现 bad case | < 5 次/周 |
| **Journeyman** | 熟练工 | 能自建 5+ skills 自动化重复工作 | 客户访谈合成 skill / NPS 自治 / release notes 自动化 | 5-15 次/周 |
| **Master** | 大师 | Claude Code 是日常工作流第一入口 | 无 SQL EDA / 产品战略 critique / 全产品周期协作 / sub-agent 编队 | > 15 次/周 |

### 自评 5 问

1. **这周你用 Claude Code 几次？**（< 5 / 5-15 / > 15）
2. **你建了几个可复用的 skill？**（0 / 1-4 / 5+）
3. **你的 prototype 平均出活时间？**（> 1 天 / 30 分钟-3 小时 / < 30 分钟）
4. **你每次跑完留 eval 吗？**（从不 / 偶尔 / 必留）
5. **你能 1 句话说出 Cat Wu 的 Product Note 三要素吗？**（不能 / 能说一半 / 全说得出）

**总分判读**：
- 5 题都在第一档 → **Apprentice**（在学走路，正常）
- 至少 3 题在第二档 → **Journeyman**（开始有杠杆了）
- 4 题以上第三档 → **Master**

**Sachin 自己的话**："I've now migrated nearly all my product work to Claude Code. While AI had already 10x'ed my productivity, Claude Code is giving me at least another 3x." —— X 2025-11

10× × 3× = 30× 杠杆——这就是 Master 段位的真实数据。

---

## 四、3 个真实案例拆解

### 案例 1：Dennis Yang（Chime Principal PM, GenAI）

**来源**：Lenny's Podcast 2025-10 集"Cursor is a much better product manager than I ever was" + ChatPRD blog

**做什么**：markdown 写 PRD → 终端 `claude` → 20 分钟可点击 prototype → Slack 录屏分享

**完整工作流（5 步）**：
1. 在 markdown 里把 PRD 写到「用户故事 + 3 个核心页面 + 数据 schema」颗粒度（约 1-2 页）
2. 在工作目录 `claude` 启动 session，第一句永远是 `Read prd.md, summarize in 5 bullets, don't code yet`
3. 确认方向后 `Now build the smallest React prototype using mock data, run on localhost:3000`
4. 20 分钟内拿到可跑的 `npm run dev`
5. 录屏 60 秒发到 Slack：「**This is validation only, not production**」

**学到的 3 件事**：
- PRD 写得越具体，prototype 出来越快
- PM 自己跑过一遍 demo，才知道哪里 spec 含糊
- 录屏 + 「validation only」标签是必备

**杠杆**：传统流程 2-4 周 → 20 分钟到可点击 demo → 立项决策成本压缩 100×

---

### 案例 2：Sachin Rekhi（前 LinkedIn / Reforge 讲师）—— 最系统

**来源**：Sachin Rekhi X 2025-11 帖 + 2025-11 Claude Code webinar（1500 PM 参加）

**做什么**：自建 13 个 skills 覆盖 strategy / design / execution 全周期

**Sachin 公开的 13 skills 分类**：

| 板块 | Skill | 解决什么 |
|---|---|---|
| **Strategy** | 1. 产品战略 critique | 让 Claude 用 5 个不同视角批判你的战略 draft |
| | 2. 竞品定价矩阵更新 | 自动抓竞品官网 + 更新定价表 |
| | 3. 竞品 teardown 生成 | 一键拆解 1 个竞品的 onboarding / pricing / 核心 flow |
| **Design / Discovery** | 4. 客户访谈 script 生成 | 基于产品阶段自动生成访谈大纲 |
| | 5. 客户访谈合成（端到端）| Whisper 转录 → 单访谈摘要 → 跨访谈 pattern 分析 |
| | 6. NPS 分析自治 | 拉 NPS 原始数据 → 分类 → 出报告 |
| | 7. 数据问题答疑（无 SQL EDA）| 自然语言问 → 自动写 SQL → 出图 |
| | 8. dashboard 生成 | 基于关键指标 + 数据源自动出 dashboard 草稿 |
| **Execution** | 9. 会议管理 | 会议纪要 + action items 提取 |
| | 10. 会议 agenda 起草 | 基于上次纪要 + 当前 sprint 状态出 agenda |
| | 11. Release notes 生成 | 基于 PR/commit 自动出对外 release notes |
| | 12. PRD 草稿（基于 Product Note）| 3 段 Product Note → 完整 PRD |
| | 13. Roadmap update | 基于本周进展更新 roadmap 文档 |

**关键洞察**：
- 不是"用 AI 写一封邮件"，是"**建一个写邮件的 skill**"——一次性 vs 资产
- 每个 skill = 1 个 prompt 模板 + 1 组输入示例 + 1 组输出示例 + 1 个验收标准（4 件套沉淀成 `.md`）

**杠杆**：从"PM 资产是 prompt 笔记" → "PM 资产是个人 skill 库"——可复用、可传承、可团队复制

---

### 案例 3：蔡逸雯 —— 用 Claude Code 写 13 套 AI PM 配套工具

**做什么**：1 个公众号专栏（《AI 时代 PM 工作流重构》26 篇）的全部配套工具——**13 套深度工具 + 1 份 128 源全球参照库**——**累计约 12-15 小时纯工作，分散在 2 周里**（传统单人写需 80-100 小时）

**完整工作流（5 步）**：

1. **建任务清单 + 优先级**（30 分钟）—— 用 TaskCreate 建 13 个 task，按"卡发文 / 边发边补"拆 P0 / P1，明确每个工具覆盖哪些正文
2. **建参照库 v1.3 当基础设施**（3-4 小时）—— 用 5 个 Sub-agent 并行 WebSearch + URL 验证，拉 10 池 128 条全球 tier-1 源（每个工具的引用都从这里出，避免重复调研）
3. **6 个 Sub-agent 并行写工具**（每个 30-60 分钟）—— 主会话给每个 Agent 喂"覆盖哪几篇 + 用参照库哪些 Pool + 标杆样例"，Agent 各自 WebSearch + 写
4. **主会话当编辑总成**（每个工具 10-15 分钟）—— Agent 返回 markdown 不能直接 Write，主会话审改格式 + 落盘 + 跑 TaskUpdate 追踪
5. **持续迭代 v1.0 → v1.1**（按需）—— 自检发现"敷衍"段落 → 用 Sub-agent 单独深挖那一段升级

**学到的 3 件事**：

1. **「Sub-agent 编队」≠「1 个 Agent 跑 13 次」**——并行才有杠杆。串行做 13 次每次 1 小时 = 13 小时；6 个并行各跑 1 小时 = 1 小时
2. **真调研标准在迭代里建立**——v1.1 把池子 5-10 当列表填（敷衍），被自己识破后逼到 v1.3 深度版（具体 paper + arXiv + 数据 + URL）。**没有读者反馈也能自我升级——前提是你愿意被自己批**
3. **主会话不能放手当甩手掌柜**——Agent 写得好不好取决于 PM 喂的 brief 多精准。**Agent 是研究员 / 写作员，主会话是编辑总成——分工才能 scale**

**杠杆对比**：

| 维度 | 传统单人 | Claude Code + Sub-agent |
|---|---|---|
| 时间 | 2 个月全职（每套深度工具 6-8 小时 × 13 = 80-100 小时）| **12-15 小时业余时间，分散在 2 周里** |
| 杠杆来源 | 单线程脑力 | 6 Agent 并行 + 128 源参照库提前建好 |
| 杠杆系数 | 1x | **6-8x** |
| 关键差异 | —— | **PM 升级为「内容策展总编」，Agent 是手下的研究员 + 写作员** |

---

## 五、5 个常见踩坑 + 解法

| # | 踩坑 | 症状 | 解法 |
|---|---|---|---|
| 1 | 不要 plan 直接要 code | 出来的代码方向偏 / 要重写 | 强制 `Tell me execution plan first, WAIT for confirmation` |
| 2 | 长会话 context 污染 | 第 50 轮开始答非所问 / 忘记 prd.md | 50 轮上限，定期 `/clear` 或开新 session |
| 3 | PM 把决策权交出去 | 觉得"AI 说要这样就这样" | 每个架构 / 数据流 / UI 决策点 PM 必须明确 ✅ |
| 4 | 没有 eval 直接上 | prototype 看起来好但生产崩 | **不写 eval 不算 done** |
| 5 | mock data 没标注 | 后续工程师以为是真接口 → 上线后炸 | prototype 收尾必录屏 + 明确说「validation only」 |
| 6（v1.0 新增）| 没建 skill 沉淀 | 同样的工作做了 5 次还是从 0 开始 | 每周末花 30 分钟把本周做 > 2 次的任务沉淀成 1 个 skill `.md` |

---

## 六、PM vs 工程师用 Claude Code 的差异

| 维度 | PM（验证级） | 工程师（生产级） |
|---|---|---|
| **主要任务** | 跑 prototype / 写 Product Note / 做 eval | 写生产代码 / 重构 / debug |
| **信任度** | 中等（PM 不审代码细节，看输出和决策） | 高（工程师审每一行） |
| **Prompt 重点** | 业务上下文 + 用户故事 + 期望结果 | 技术约束 + 架构 + 测试要求 |
| **验收标准** | 跑得起来 + demo 看着对 + eval 过 | 单测 + 集成测 + code review + CI 绿 |
| **代码归属** | 一次性，跑完就丢 / 给工程师重写 | 长期维护，进 main 分支 |
| **Session 长度** | 短（< 50 轮，跑完即停） | 长（持续迭代，配合 git history） |
| **Skill 焦点** | 重复工作自动化（访谈 / NPS / release notes） | 工程效率提升（重构 / 测试生成 / 文档） |
| **失败容忍** | 高（跑不通就换方向）| 低（生产 bug 要负责）|
| **典型耗时** | 20 分钟-3 小时 | 半天-1 周 |
| **risk** | 把 demo 当产品上线 | 过度信任 Claude 不 review |

**一句话边界**：
> **PM 用 Claude Code 是为了"决策更快"，工程师用 Claude Code 是为了"代码更好"。混了角色就两边都不像。**

---

## 七、引用规范（Pool 位置 + 已核 URL）

| 内容 | 来源 | 已核 URL | 参照库位置 |
|---|---|---|---|
| Cat Wu "Prototypes over PRDs" + Antfooding + 5-10 分钟反馈循环 | Lenny's Podcast 2026-04-23 | [lennysnewsletter.com](https://www.lennysnewsletter.com/p/how-anthropics-product-team-moves) | Pool 1.3 |
| Mike Krieger Product Note 3-4 段框架 | Lenny's Podcast Mike Krieger 集 | lennysnewsletter.com | Pool 1.3（关联） |
| Boris Cherny 100% Claude Code + commit review | Lenny's Podcast Boris Cherny 集 2026-02 | lennysnewsletter.com | Pool 1.4 |
| Sachin Rekhi 13 skills + Claude Code webinar 1500 PM | X 2025-11 | [x.com/sachinrekhi](https://x.com/sachinrekhi/status/2029620106213621971) | Pool 1.7 |
| Sachin Rekhi 10× × 3× 杠杆 | X 2025-11 | [x.com/sachinrekhi](https://x.com/sachinrekhi/status/2025963914966823066) | Pool 1.7 |
| Sachin Rekhi AI Prototyping Mastery Ladder | sachinrekhi.com 2025-10 + Reforge blog | [sachinrekhi.com](https://www.sachinrekhi.com/p/the-ai-prototyping-mastery-ladder) | Pool 1.7 / Pool 10.2 |
| Dennis Yang Chime PM markdown PRD → 20 分钟 prototype | Lenny's Podcast 2025-10 | [lennysnewsletter.com](https://www.lennysnewsletter.com/p/cursor-is-a-much-better-product-manager) | Pool 1.12 |

**参照库全文（128 条全球 tier-1 源）**：`/Users/caiyiwen/ai-product-column-research/tools/_global-references.md`

---

## 八、设计依据 & 批判性自评 v1.0 ⭐

### 8.1 这套 SOP 的 4 个全球 tier-1 参照

| 框架 | 我借鉴了什么 | 我没采用什么 | 原因 |
|---|---|---|---|
| **Cat Wu Anthropic Product Note**（Pool 1.3）| Product Note 3-4 段结构（Step 2）+ antfooding 反馈循环（Step 4）| 5-10 分钟全员反馈节奏 | 1 人 PM 没有 internal Slack 频道——降级为"录屏 + 团队 review"|
| **Boris Cherny 100% Claude Code**（Pool 1.4）| "PM 不写代码但所有决策都在场"原则（Step 4 Editor-in-Chief 模型）| 100% 代码由 Claude 写的工程师工作流 | PM 不是工程师，验收标准不同 |
| **Sachin Rekhi 3 阶梯**（Pool 1.7）| Apprentice/Journeyman/Master 框架 + 13 skills 具体清单 | 15 skills mastery ladder 完整版 | 那 15 skills 偏 designer/developer，PM 实战用 13 skills 更对齐 |
| **Mike Krieger Product Note**（Pool 1.3 关联）| "PRD → Product Note" 替代逻辑 | 完整 spec 流程 | Anthropic 内部跳 spec，但 1 人 PM 仍需保留 prd.md 作为 Claude Code 的 context |

### 8.2 为什么选 5 步 SOP

| 替代方案 | 优势 | 缺点 | 拒绝原因 |
|---|---|---|---|
| Cat Wu 原版 4 步（spec → prototype → dogfood → ship）| Anthropic 实战验证 | 假设 internal 用户和反馈频道 | **1 人 PM 没频道**，必须补 Step 1 + Step 5 |
| Dennis Yang 3 步 | 极简 | 没有"plan 再 code"和"留 eval"两个保险 | **太简** |
| Sachin 完整 15 skills mastery ladder | 最系统 | PM 初学者会被压垮 | **太重** |
| 我的 5 步 SOP（本版）| 覆盖 context / spec / plan / role / eval 五个 PM 实际卡点 | 没经过真 PM 测试 | **✅ 选这个** |

### 8.3 已知盲区 + 后续验证计划

| 盲区 | 影响 | v1.1 / v2.0 计划 |
|---|---|---|
| ⚠️ **未做真 PM 测试** (n=0) | 不知道 5 步在真实评审场景的实际跑通率 | v1.1 蔡逸雯本人跑 1 个真案例 + v2.0 找 3-5 个 AI PM 试跑 |
| ⚠️ **缺案例 3（蔡逸雯亲身案例）** | 1 个真实国内 PM 案例缺位，3 案例都是国外 | v1.1 蔡逸雯审改时补 |
| ⚠️ **没覆盖 Sub-agent 编队 / Skills Marketplace** | Anthropic 2026-06 Agent SDK 独立 credit + GitHub `pm-skills` marketplace 已成形 | v2.0 加 Step 6 |
| ⚠️ **没说明 Skill 沉淀格式标准** | 5 个踩坑 #6 提到"沉淀成 skill"但没给模板 | v1.1 补一个 skill `.md` 模板（4 件套） |
| ⚠️ **PM × 工程师交接动作没细化** | 第六节对比表说清差异但没给 handoff doc 模板 | v1.1 补 handoff doc 1 页模板 |

### 8.4 适用 / 不适用边界

- ✅ **适用**：AI 应用层 PM（聊天 / Agent / RAG / 内容生成 / 内部工具）/ 1 人 PM + 小团队 / 增量验证 + 全新原型 / B 端 + C 端
- ❌ **不适用**：不碰技术的传统行业 PM / 生产代码直接上线 / 纯 UI mockup（v0 / Lovable 更高效）/ AI 基础模型公司的 PM

### 8.5 这套 SOP 的 "调研依据深度等级"

| 元素 | 等级 | 依据 |
|---|---|---|
| Step 1 上下文准备（2 个 markdown）| L2 | Cat Wu 节目反复强调"为什么 + 在哪里"，但 2 个文件结构是我的设计判断 |
| Step 2 Product Note 3-4 段 | **L1** | Mike Krieger + Cat Wu 双口径，Anthropic 内部正在用 |
| Step 3 plan 再 code | **L1** | Cat Wu + Boris Cherny + Dennis Yang 三人 workflow 同时印证 |
| Step 4 Editor-in-Chief 角色 | **L1** | Boris Cherny "100% Claude Code 但每个 commit review" 原话支撑 |
| Step 5 eval 钩子 | L2 | Sachin Rekhi 公开方法 + 通用 AI 工程最佳实践 |
| 3 阶梯框架 | **L1** | Sachin Rekhi 原创框架，sachinrekhi.com + Reforge 双发 |
| 13 skills 清单 | **L1** | Sachin Rekhi X 公开帖 |
| 5 + 1 踩坑 | L3 | 案例归纳 + 我的经验，未做大样本测试 |
| 第六节 PM vs 工程师 10 维对比 | L4 | 我的设计判断，行业无现成对比表 |
| 自评 5 问 + 周使用次数阈值 | L4 | 我设定的判分标准，未经验证 |

**说明**：标 L4 的元素是"做最好"路径上待验证的部分，v2.0 优先升级（找 5-10 个真 AI PM 校准阈值）

---

## 九、配套使用建议

这份 SOP 推荐配合：
- **9 种 Vibe Coding 工具横评表**（同钩子领取）—— Step 3 选工具时对照
- **Claude Code 起手 prompt 模板（PM 专用 3 套）**（同钩子领取）—— Step 2 + 3 + 5 直接抄
- **第 17 篇正文 7 个真实 prompt** —— 跑 5 步 SOP 时填进每一步

---

## 十、读者使用反馈征集

用过这套 5 步 SOP 跑出来一个 prototype 了吗？卡在哪一步？
欢迎加微信 **CYW960325** 反馈，被采纳的真实案例会出现在 v1.1。

---

## 文末微信钩子

```
─────────────────────────────
📦 配套资源 · 第 17 篇

加我微信 **CYW960325**（备注「专栏17」），免费领：
✓ PM × Claude Code 工作流 SOP（含 Cat Wu / Dennis Yang / Sachin Rekhi 案例拆解）
✓ 9 种 Vibe Coding 工具横评表
✓ Claude Code 起手 prompt 模板（PM 专用 3 套）

【3 种格式任选】
📄 PDF：加微信后直接发文件给你
🔗 腾讯文档：微信里直接打开（推荐 📱）
💻 GitHub Pages：长期收藏 / 外链分享
─────────────────────────────
```

---

> 蔡逸雯 · 8 年 QE → AI PM · 公众号「蔡逸雯」
> v1.0 · 2026-05-21 · 建议蔡逸雯审改时补案例 3 后转 v1.1
> CC-BY-NC 4.0 · 转载请注明出处
