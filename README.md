# AI 时代 PM 工作流重构

> 第一季 · 26 篇 · 写给 AI PM 的工业级 PM 工作流手册
> 作者：[蔡逸雯](https://github.com/caiyiwenan) · 公众号「蔡逸雯」

---

## ⭐ 一句话 signature

> **AI PM 的工作不是写需求，是定义边界 + 准备降级。**

这是本季 26 篇的核心论断——AI 是概率系统，永远会失败，PM 的核心动作是**定义边界**（AI 能做什么 / 不能做什么）+ **准备降级**（错了怎么办）。这正是 60 年质量工程传统 FMEA 在 AI 时代的延伸。

---

## 写给谁

- **在职 AI PM** — 你已经在做 AI 产品，但工作流没系统化
- **想转型 AI 的传统 PM** — 你有 PM 经验，但不知道 AI 时代该重学什么
- **AI 产品团队 leader** — 你要带团队走完 "AI Native PM" 的工作流升级

**不适合**：
- AI 工程师 / ML 算法工程师（技术深度只到 PM 必须懂的边界）
- 0 经验的 PM 新人（先看传统 PM 入门书）
- 纯学术研究者

---

## 26 篇目录

📖 **前言** · [00-关于本专栏](./00-preface.md)

### 一 · 需求识别（第 1-6 篇）
1. [6 个崩塌点——AI 时代 PM 工作流为什么必须重构](./01-six-collapse-points.md) ⭐ 开篇
2. [从做功能到做能力](./02-from-features-to-capabilities.md)
3. [AI 产品需求来源不再是用户访谈](./03-not-from-user-interviews.md)
4. [该 AI 化 vs 不该 AI 化判断框架](./04-pseudo-ai-needs.md)
5. [Agent 能力边界 4 类硬规则](./05-agent-capability-boundaries.md)
6. [业务方需求评审 SOP + 5 信号打分卡](./06-five-signals.md)

### 二 · 方案 + PRD 框架（第 7-12 篇）
7. [从功能流到能力流——AI 产品设计范式切换](./07-capability-flow.md)
8. [模型选择 4 维度](./08-model-selection.md)
9. [Token 经济学](./09-token-economics.md)
10. [技术路径决策树](./10-tech-path-decision-tree.md)
11. [PRD 4 加 2 砍骨架](./11-prd-skeleton.md) ⭐ 综合原创
12. [Eval 章节 5 要素模板](./12-eval-design.md)

### 三 · PRD 硬通货（第 13-15 篇）
13. [EDD - Eval-Driven Development](./13-eval-driven-development.md)
14. [Bad Case 4 级分级](./14-bad-case-grading.md)
15. [Cost 给 CFO 算账](./15-cost-budget-cfo.md)

### 四 · 交付（第 16-19 篇）
16. [72h MVP 方法论](./16-72h-mvp.md)
17. [PM 用 Claude Code 实战](./17-pm-claude-code.md) ⭐ 杀手锏
18. [多轴灰度策略](./18-gradient-strategy.md)
19. [Pre-launch Eval 5 大类](./19-pre-launch-eval.md)

### 五 · 运营（第 20-22 篇）
20. [4 类 AI 特有监控指标](./20-monitoring-metrics.md)
21. [Bad Case 管理 5 步](./21-bad-case-management.md)
22. [降级勇气清单](./22-courage-to-downgrade.md)

### 六 · 协作（第 23-24 篇）
23. [和工程师的新协作语言](./23-pm-engineer-language.md)
24. [和老板的新对齐框架](./24-aligning-with-ceo.md)

### 七 · 组织 + 终章（第 25-26 篇）
25. [AI Native 团队 3 种模式](./25-ai-native-team.md) ⭐ B 端漏斗发动机
26. [终章——个人 Native 化 vs 公司 Native 化](./26-pm-growth-path.md)

📚 **参考资料索引** · [27-references](./27-references.md)（95 条引用 · v1.1 · 持续补充中）

---

## 9 套可直接抄的工具

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

---

## 4 类原创洞察

1. **综合原创**：PRD 4 加 2 砍（"砍 2" 是反共识——业内只讲加什么，没人讲砍什么）
2. **本土洞察**：个人 Native 化 vs 公司 Native 化两条独立赛道（全球 blindspot）
3. **角度原创**：8 年质量工程视角（FMEA / 概率思维 / 知道何时停止）
4. **方法论原创**：5 信号打分卡 / 4 场景剧本 / 看 trace 最小集 / CFO 成本卡片

---

## 作者锚点

**8 年质量工程出身**（QA → 测试架构师 → PM）。这给了 3 个独有的 framing：

- **FMEA 视角看 PRD** —— 失败模式分析是质量工程 60 年传统，引入 AI PRD 是新组合
- **概率系统的可观测性** —— 用"分布"而非"均值"看 AI 输出，是质量工程师本能
- **"知道什么时候停止"** —— 降级勇气是质量工程师最难的判断力

---

## AI 协作披露

本专栏部分内容由作者与 **Claude Opus 4.7（1M context）** 协作完成——
- **AI 辅助**：案例核查 + 业内引用整理 + 文字润色
- **作者原创**：核心观点 + 框架结构 + 8 年质量工程视角 + 本土洞察
- **责任承担**：所有商业判断 + 内容定稿 + 责任全由作者承担

**为什么主动披露**：这本专栏教 PM 用 Claude Code 重构工作流（第 17 篇）——作者自己用 Claude 协作写专栏，**就是这套工作流的最佳示范**。

---

## 免责声明

本仓库引用的业内案例、报告数据、KOL 观点、模型数据均来自**公开来源**，属评论性引用（fair use）。提及的公司名（Anthropic / OpenAI / Notion / Cursor / Lovable / Microsoft / Klarna / Air Canada / DPD 等）、产品名、商标归各自权利人所有，**本专栏不构成代言或商业合作**。

**模型版本号与数据**：使用 2026-Q2 业内快照（Claude Opus 4.7 / GPT-5.5 / Gemini 3.1 Pro / DeepSeek V3.2 / Kimi K2.6 等），**3-6 个月内必须以厂商官方 model card 为准**——本仓库不为这些精确数字背书。

完整参考资料 URL 清单见 [27-references.md](./27-references.md)。

---

## License

**[CC-BY-NC 4.0](./LICENSE)** · Creative Commons Attribution-NonCommercial 4.0 International

你可以：
- ✅ 自由阅读 / 分享 / 引用本仓库内容
- ✅ 把工具模板抄进自己公司 PRD
- ✅ 在 PM 培训 / 内部分享时引用（注明出处）

你不能：
- ❌ 把内容直接打包成付费课程 / 书籍出售
- ❌ 用于商业产品 / 营销资料而不注明出处
- ❌ 篡改或删除作者署名

**商业合作 / 引用授权**：通过公众号「蔡逸雯」留言联系。

---

## 反馈 / 交流

- **公众号**：「蔡逸雯」
- **付费实战社群**（含月度直播 + 蔡的咨询答疑）：公众号留言「实战社群」
- **第二季预告**：Context Engineering / Memory / Multi-Agent / Agent OS——预计 2026-Q3 首发

---

## Star 这个仓库

如果这本专栏对你有帮助——

⭐ **Star 这个仓库** —— 是给作者最好的反馈
🔄 **Fork 后写自己的版本** —— 这套方法论需要更多本土实践
📢 **转发给一位 AI PM 朋友** —— 让圈层一起升级

---

> **第一季完结 · 第二季 2026-Q3 见**
