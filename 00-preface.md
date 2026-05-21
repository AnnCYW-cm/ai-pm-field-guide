# 前言 · 关于本专栏

> 第一季《AI 时代 PM 工作流重构》· 序篇
> 作者：蔡逸雯（公众号「蔡逸雯」）

---

## 这本专栏的核心论断

> **AI PM 的工作不是写需求，是定义边界 + 准备降级。**

这是本季 26 篇的 signature。

业内已有的 framing 都在占自己的位置：
- **Hamel Husain**：「Eval-driven development is the defining skill for AI PMs」
- **Aparna Chennapragada**：「Prompt sets are the new PRDs」
- **Cat Wu**：「Prototypes over PRDs」
- **Marty Cagan**：「Discovery over delivery」

我占的位置——**「边界 + 降级」**。

为什么是这两件事？因为 AI 是**概率系统**，不是确定系统——
- 模型永远会失败（详见第 14 篇 Bad Case 4 级）
- 上线永远会出意外（详见第 19 篇 Pre-launch Eval 5 大类）
- 业务永远会出现 AI 边界外的需求（详见第 5 篇 Agent 边界 + 第 22 篇降级勇气）

所以 PM 的核心动作是两件事：
- **定义边界**——AI 在这个场景能做什么 / 不能做什么 / 什么时候转人工（第 2 / 5 / 7 / 11 / 23 篇）
- **准备降级**——错了怎么办 / 降到规则 / 转人工 / postmortem（第 14 / 19 / 21 / 22 篇）

**如果一本 AI PM 专栏不能让你内化这两件事，其他都是 nice-to-have**。

而这两件事——**正是质量工程 60 年传统里 FMEA 的核心动作**。这就是为什么作者 8 年质量工程背景成为这本专栏的真护城河。

---

## 这本专栏写给谁

**核心读者**：
- 在职 AI PM —— 你已经在做 AI 产品，但工作流没系统化
- 想转型 AI 的传统 PM —— 你有 PM 经验，但不知道 AI 时代该重学什么
- AI 产品团队的 leader —— 你要带团队走完"AI Native PM"的工作流升级

**不适合**：
- AI 工程师 / ML 算法工程师（这本是 PM 视角，技术深度只到 PM 必须懂的边界）
- 0 经验的 PM 新人（建议先看传统 PM 入门书再来读这本）
- 纯学术研究者（这本是工业实战，不是 AI 理论）

---

## 这本专栏不写什么

诚实告知——

1. **不教你写 prompt 语法** —— 这是工程师的活，PM 只需要懂边界（详见第 23 篇）
2. **不教你 fine-tune / RAG / 推理优化的具体实现** —— PM 不需要懂这些
3. **不复制 Hamel / Cat Wu / Aparna 原文** —— 全球前沿的最新概念（Context Engineering / Memory Architecture / Agent OS）不在本季覆盖范围，留到第二季
4. **不预测股价 / 不教你投资 AI 公司** —— 这是 PM 专栏不是投资专栏

---

## 这本专栏的差异化定位

中文 AI PM 圈大多数内容是**翻译 Lenny / Marty Cagan / Sachin Rekhi**。

这本专栏不一样的地方——

**作者锚点：8 年质量工程出身**（QA → 测试架构师 → PM）。这给了 3 个独有的 framing：
- **FMEA 视角看 PRD** —— 失败模式分析是质量工程 60 年传统，引入 AI PRD 是新组合
- **概率系统的可观测性** —— 用"分布"而非"均值"看 AI 输出，是质量工程师本能
- **"知道什么时候停止"** —— 降级勇气是质量工程师最难的判断力

**本土洞察**：中国 PM 大多在「公司没启动 AI 转型 + 个人有野心」的两难处境。**全球内容默认你公司是 OpenAI / Anthropic 这种 AI Native——这本专栏专门处理中文环境**。

---

## 总免责声明

本专栏引用的业内案例、报告数据、KOL 观点、模型数据均来自**公开来源**，属评论性引用（fair use）。

提及的公司名（Anthropic / OpenAI / Notion / Cursor / Lovable / Microsoft / Klarna / Air Canada / DPD 等）、产品名（Claude Code / ChatGPT / Cursor 等）、商标归各自权利人所有，**本专栏不构成代言或商业合作**。

引用的 KOL 公开观点（Hamel Husain / Cat Wu / Sachin Rekhi / Mike Krieger / Aparna Chennapragada 等）—— 来源以公开访谈 / 博客 / podcast / 会议演讲 / Twitter 为准。完整引用 URL 清单见配套资产《参考资料索引》。

**模型版本号与数据**：本专栏使用的是 2026-Q2 的业内快照（Claude Opus 4.7 / GPT-5.5 / Gemini 3.1 Pro / DeepSeek V3.2 / Kimi K2.6 等），**模型迭代极快，3-6 个月内必须以厂商官方 model card / Artificial Analysis / SEAL 等第三方榜单为准**——本专栏不为这些精确数字背书。

**翻车案例数据**：所有金额、日期、影响范围数据来自公开新闻报道，作者已尽力核对（Air Canada 加币 650.88 / Klarna 700 客服 FTE / Cursor billing 暴雷等），但**业内事实可能随时间澄清更新**，建议读者结合最新报道判断。

---

## AI 协作披露

本专栏部分内容由作者与 **Claude Opus 4.7（1M context）** 协作完成——
- 案例核查 + 业内引用整理 + 文字润色：AI 辅助
- 核心观点 + 框架结构 + 8 年质量工程视角 + 本土洞察：作者原创
- 所有商业判断 + 内容定稿 + 责任承担：作者

**为什么主动披露**：这本专栏教 PM 用 Claude Code 重构工作流（第 17 篇）—— 作者自己用 Claude 协作写专栏，**就是这套工作流的最佳示范**。

读者拿到的是「PM × AI 协作」的真实产物，不是「装作没用 AI」的过时模式。

---

## 配套资产说明

每篇文末都标有「配套资产」—— 付费读者解锁。**所有 9 套工具均可直接抄进自己公司 PRD**：

| # | 工具 | 篇 |
|---|------|---|
| 1 | 5 信号需求评审打分卡 + 5 句反问模板 | 06 |
| 2 | PRD 4 加 2 砍骨架模板 | 11 |
| 3 | Eval 章节 5 要素模板 | 12 |
| 4 | Bad Case 4 级 + Microsoft RAI 矩阵 | 14 |
| 5 | CFO 成本卡片模板 | 15 |
| 6 | 7 个 Claude Code 实战 prompt | 17 |
| 7 | Pre-launch Eval 5 大类 checklist | 19 |
| 8 | 4 种降级场景 + 3 句话术 | 22 |
| 9 | 4 场景协作剧本 + 看 trace 5 字段速查 | 23 |

另：**《参考资料索引》** —— 26 篇所有引用 URL 完整清单（业内 KOL 出处 / 第三方报告 / 翻车案例新闻链接），方便读者深挖任何一条想进一步研究的引用。

---

## 反馈 / 退订 / 加入读者群

- **加入读者群**：在公众号「蔡逸雯」留言
- **反馈**：公众号「蔡逸雯」直接留言
- **退订**：按平台规则在 7 天内可申请退款
- **第二季预告**：会处理 Context Engineering / Memory Architecture / Multi-Agent Orchestration / Agent OS 这些全球前沿议题。订阅本季读者优先低价。

---

## 一句话告诉你这本专栏的价值

> **省你 50 小时自己整理 Hamel / Cat Wu / Anthropic / a16z 原文的时间，
> 给你 9 套可直接抄进公司的 PM 工具，
> 加 4 类原创洞察（综合 / 本土 / 角度 / 方法论）。**

下面开始第 1 篇——**6 个崩塌点**。

---

> 作者：蔡逸雯
> 首发：2026-05-21
> 第一季完结
