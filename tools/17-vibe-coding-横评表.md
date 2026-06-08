---
tool_id: P0-17-1
serves_essay: 17
status: ready-for-review
last_updated: 2026-05-21
deliverable_formats: [markdown, pdf-table, notion, tencent-doc]
hours_actual: 3 (v0.1 skeleton 1h + v1.0 retrofit 2h)
version: v1.0
references_pools_used: [P1.13 Anna Arteeva, P8.8 Aider, P8.9 Continue.dev, P8.10 Cline, P8.11 Cognition Devin, P9.4 Pragmatic Engineer "AI Tooling 2026" 调研, P9.11 r/LocalLLaMA, P9.12 HackerNews]
validation_status: "蔡逸雯亲测 4/9 款（Claude Code / Cursor / Lovable / v0）+ 第五节个人横评 5.1-5.4 已审改完成（2026-06-07）；其余 5 款基于 Anna Arteeva 评测 + Pragmatic Engineer 调研 + GitHub 数据；未做真 PM 群体测试 (n=0)；v1.1 计划 n=5"
---

# 9 种 Vibe Coding 工具横评表 v1.0

> 服务于第 17 篇《PM × Claude Code》配套资源 ①
> 数据基线日期：**2026-05**（每季度更新，见第六节）
> 注：Manus / 天工等中文区工具不在本横评（参照库原则 "国内市场存在信息差，不参考"）

---

## 一、为什么需要这份横评

### 1.1 三个硬数据：AI 编码已是 PM 的"水电煤"

**Pragmatic Engineer《AI Tooling for Software Engineers in 2026》调研**（2026-01-27 至 2026-02-17，近 1000 名工程师参与）：

> - **95% 工程师每周至少用一次 AI 工具**
> - **75% 用 AI 完成至少一半的编码工作**
> - **55% 已定期使用 AI agent**（vs 18 个月前几乎为 0）
> - **Claude Code 8 个月内从 0 跃为 #1**，超越 GitHub Copilot 和 Cursor

含义对 PM：**你团队里的工程师 95% 已经在用 AI 工具——PM 还没用，等于差了一代杠杆**。

### 1.2 第二个数据点：Claude Code GitHub 增长曲线

| 时间 | Claude Code GitHub stars |
|---|---|
| 2025-05（GA 发布） | 0 |
| 2025-12 | 81.6k |
| 2026-04 | 115k |
| 2026-05 | **121k**（本表基线） |

**对照**：Aider（开源 terminal 鼻祖）从 2024 起累计才到 ~45k；Cline（开源 VS Code 新星）2026-05 ~61k。Claude Code **8 个月做到 Aider 3 年的星数**——是开源 coding agent 史上最快增长。

### 1.3 为什么 PM 需要横评而不是"跟着工程师选"

工程师选工具的优先级是：**代码质量 > 速度 > 价格 > UI**
PM 选工具的优先级是：**上手时间 > UI > 价格 > 代码质量**

**两个优先级完全相反**——所以工程师群里推荐的 Cursor、Aider、Cline 对 PM 不一定是最优。本横评从 PM 视角重排。

---

## 二、9 工具横评主表

> 数据基线 2026-05。价格为月付（年付通常便宜 10-20%）。GitHub stars 仅适用于开源项目。

| # | 工具 | 起步价/月 | GitHub stars | 适合人群 | 上手时间 | 核心优势 | 核心劣势 | 真实案例锚点 |
|---|---|---|---|---|---|---|---|---|
| 1 | **Claude Code** | $20 Pro / $100 Max 5x / $200 Max 20x | **121k** (2026-05) | 工程深度 + 进阶 PM | 1-3 天 | SWE-bench 第一档；MCP 接 Linear/Slack/GitHub；codebase 上下文最强 | 命令行门槛；视觉/UI 弱；2026-Q2 计费规则改了 3 次 | Anthropic 内部 PM/Designer/Eng 全员用；Boris Cherny 自 2025-11 起 100% 代码由 Claude Code 写 |
| 2 | **Cursor** | $20 Pro / $40 Business / $200 Ultra | 闭源 | 工程师 + 已有 codebase 的 PM | 1-2 天 | IDE 集成原生；tab 补全顺滑；多模型可切 | 2025-06 credit billing 暴雷（社区抗议）；mid-2025 转 credit-based 后真实成本不透明 | 100 人撑 $1B ARR（2025-09 媒体报道） |
| 3 | **Lovable** | $25 Pro / $50 Business | 闭源 | 非技术 PM / 创始人 | 10 分钟 | 全栈自动生成；UI 漂亮；社区强 | 工程深度弱；超出模板自定义难；credit 烧得快 | 18 人 $17M ARR（2025 Q2 公开数据） |
| 4 | **Bolt.new** (StackBlitz) | $25 Pro / $30/座位 Teams | 闭源 | 速度优先 / Demo 一次性 | 10 分钟 | 最快出 prototype（< 5 分钟）；浏览器内即写即运行 | 后端能力弱；token 用得激进，1M 免费额度撑不久 | StackBlitz 母公司 ARR 2025 突破 $20M（Sacra 数据） |
| 5 | **v0** (Vercel) | $20 Premium / $30/座位 Team | 闭源 | UI 设计师 / 前端 PM | 30 分钟 | UI 质量最高（shadcn+Tailwind）；Figma 导入；可推 Vercel 一键部署 | 仅前端；后端要拼 Vercel 全家桶；UI 风格同质化（"v0 味") | Vercel 自家 dashboard 多处 UI 直接来自 v0 |
| 6 | **Replit** | $20 Core（含 $25 usage credits）/ $30 Teams | 闭源 | 全栈学习者 / 教育场景 | 1 天 | 全栈 + 一键部署 + Agent 3 强；浏览器内可跑数据库 | UI 偏初级；usage credits 不滚存；Agent 烧钱重，$50-150/月超额很常见 | Replit Agent 是早期"PM 一人撑全栈"的代表工具 |
| 7 | **Aider** | 免费（自带 API key） | **~45k** (2026-05) | 工程出身 / Linux 极客 / 想自动化的 PM | 半天 | terminal-first；100+ LLM 适配；自动 git commit；公开 code-edit benchmark | 没 UI，纯终端；新手起步陡 | 开源 coding agent 鼻祖（2024 起）；Paul Gauthier 一人维护，无 VC 压力 |
| 8 | **Cline** | 免费（自带 API key） | **~61k** (2026-05) | VS Code 用户 + 想看每步审批的 PM | 半天 | VS Code 内可视化"批准每一步"；并行 sub-agent；30+ provider | 仍是开源项目；调试体验依赖 IDE；与 Claude Code 重合度高 | 2025 下半年 star 增长最陡的 coding agent；社区把它叫"Claude Dev"（旧名） |
| 9 | **Cognition Devin** | $20 Core / $500 Team / Enterprise 议价 | 闭源 | 工程团队 + 大企业 | 几小时配置 | 真 "autonomous SWE"；Devin 2.0 从 $500 降到 $20 大众化 | 演示争议史（2024-03 launch 被工程师 teardown 指控剪辑） | 89% Cognition 自身代码由 Devin 写；Mercedes legacy 项目 **8 天 vs 原 8 个月**；客户含 NASA / Goldman Sachs / Santander；2026-05 估值 $26B post-money |

---

## 三、用户场景 → 推荐工具决策表

| 你是 | 你要做的事 | 首选 | 备选 | 不要选 |
|---|---|---|---|---|
| 非技术 PM 第一次玩 | 给老板看 clickable prototype | **Lovable** | Bolt.new / v0 | Aider / Cline（命令行劝退） |
| PM + 想自学一点工程 | 跑 eval / 写小脚本 / 周报自动化 | **Claude Code** | Cursor | Lovable（接不到真 API） |
| UI 重的产品 PM | 拿设计稿想直接生成 React | **v0** | Lovable | Claude Code（UI 不是它强项） |
| 1 人 ToC App 创业者 | 从 0 到上线 MVP | **Lovable + Claude Code 组合** | Replit | Devin（贵且重） |
| 工程团队 PM | 评审前快速验证 spec / 复现 bad case | **Claude Code** | Cursor | Bolt.new（demo 一次性，不能读真 codebase） |
| 有 codebase 想读懂工程师写啥 | 读代码 + 提问 | **Cursor** | Claude Code | v0（不读代码） |
| 想自动化跑批 eval / 跑 100 次 prompt 对比 | terminal 脚本 | **Aider** | Claude Code | Lovable（不是 batch 工具） |
| 不熟代码但想"看每一步" | 安全审批 AI 改动 | **Cline** | Claude Code（带 plan mode） | Devin（autonomous，不审批） |
| 大企业要 SOC2 + VPC 部署 | 自治 agent 解决 backlog | **Devin Enterprise** | Claude Code Enterprise | 开源项目（合规缺位） |

---

## 四、按维度深潜：4 大派系的 PM 选型逻辑

### 4.1 派系划分

```
                ① Terminal 派      ② IDE 派        ③ Web 全栈派       ④ Autonomous 派
                ───────────────    ─────────────    ─────────────      ─────────────
                Claude Code         Cursor           Lovable             Devin
                Aider               Cline            Bolt.new
                                                     v0
                                                     Replit
```

### 4.2 Terminal 派（Claude Code / Aider）

**核心命题**：把 PM 的工作从"点 IDE"压到"敲命令"——节省的不是时间，是**心智切换成本**

**适合 PM**：每天本来就用 terminal / 已经习惯 git CLI / 想自动化跑批的 PM

**Claude Code vs Aider**：
- Claude Code = 闭源 + Anthropic 官方 + MCP 生态完整
- Aider = 开源 + Paul Gauthier 一人维护 + 多 LLM 适配 + 公开 benchmark
- **PM 推荐 Claude Code**（不折腾，开箱即用）；**Aider 给工程倾向 PM**

### 4.3 IDE 派（Cursor / Cline）

**核心命题**：在 PM 已经打开的 VS Code / Cursor 里嵌入 AI——**零迁移成本**

**Cursor vs Cline**：
- Cursor = 闭源 IDE fork，所有功能内置，tab 补全顺滑
- Cline = 开源 VS Code 扩展，可视化"批准每一步"，30+ provider
- **PM 推荐 Cursor**（产品化好）；**Cline 给想用开源的 PM**

**Cursor 2025-06 billing 暴雷**：社区反弹很大——从 request-based 改 credit-based 后实际成本上涨。**PM 提醒**：不要把 Cursor 当唯一工具，留 1-2 个备选

### 4.4 Web 全栈派（Lovable / Bolt.new / v0 / Replit）

**核心命题**：浏览器一打开就能生成完整 app——**0 安装 0 配置**

**4 款细分**：

| 工具 | 真正擅长 | 不擅长 |
|---|---|---|
| **Lovable** | 完整全栈 app（前后端 + 数据库都给你拼） | 复杂自定义 / 工程深度 |
| **Bolt.new** | 最快出 prototype（< 5 分钟） | 长期维护 / 后端复杂 |
| **v0** | UI 质量最高（shadcn/Tailwind） | 后端（要拼 Vercel 全家桶） |
| **Replit** | 全栈 + 真能跑（带数据库 + 部署） | UI 偏初级 |

**Anna Arteeva 总结被引最多**：

> "**Lovable 赢非技术 PM，Bolt 赢速度，v0 赢 UI，Replit 赢全栈，Cursor / Claude Code 赢工程深度。**"
> — Anna Arteeva, [The Vibe-Coder's Prompting Guide](https://annaarteeva.medium.com/the-vibe-coders-prompting-guide-e04ba0295a18) + Maven 课程《Vibe-Coding for Marketing》

### 4.5 Autonomous 派（Cognition Devin）

**核心命题**：PM 派任务给 agent → 关掉电脑去开会 → 回来看 PR——**把 PM 从"操作员"升级为"产品经理人"**

**Devin 2024 vs 2026**：
- 2024-03 launch 时引发"被剪辑 demo"争议——但 2026 用 **89% Cognition 自身代码 Devin 写 + Mercedes 8 天 vs 8 个月 + $26B 估值**回应批评
- Devin 2.0 价格从 $500 降到 $20——意味着**单 PM 也能用**

---

## 五、蔡逸雯个人横评

**亲测覆盖率**：4/9 款（Claude Code / Cursor / Lovable / v0）

### 5.1 我自己最常用的（个人主推）

**Claude Code——但我不忠诚于它。**

我的实际工作流是**多工具交叉**：Claude Code 开发 / Codex 测试 / 另一款写方案。我从不把自己锁死在一个 AI 工具上。

「最常用」≠「忠诚」。我用 Claude Code 是因为**它当下解决我的问题最好**——仅此而已。Claude Code 涨价我不介意，因为我真正在意的是**能不能解决问题**。

> **PM 视角的反共识**：不要给自己贴「工具忠诚度」标签。今天最好用的不是明天最好用的——AI 工具半年一代，**忠诚于问题，不忠诚于工具**。

### 5.2 我推给 PM 朋友的（友推）

**我不推任何工具。除非我在带团队落地一个具体项目。**

PM 朋友问我「用什么 AI 工具好」——我的回答是：**先别问工具，先问你的思维**。

工具半年一代，思维管 10 年。我推给 PM 朋友的不是 Claude Code / Cursor / Lovable——是 3 本书：

- **《金字塔原理》**（Barbara Minto）—— 怎么把混乱想清楚
- **《大象——Thinking in UML》**（谭云杰）—— 怎么用结构化语言描述系统
- **《学会提问》**（Browne & Keeley）—— 批判性思维入门

> **反共识**：90% 的 PM 在工具横评里找答案，但真正决定他们能不能用好 AI 的是「**提问能力 + 结构化思维**」——这两个是底层。
>
> 工具我自己用就够了。PM 朋友要带，我带的是思维。

### 5.3 我会避雷的（避雷）

**我不吐槽任何工具。**

任何 AI 工具都有好的一面和坏的一面——但**绝大多数让你想吐槽的「工具问题」，根因都不在工具**：

- 可能是你**需求没传达清楚**（需求模糊，工具只能瞎猜）
- 可能是工具**没拿到足够清晰的上下文**（你没给 context.md，没拆任务）
- 可能是你选错了工具类型（拿 Lovable 做工程级 codebase 改造）

> **反共识**：AI PM 在公开渠道吐槽工具是廉价的——读者看完只会更焦虑「那我该用什么」。**真正难的是承认自己的需求没说清、上下文没给够**。

要「避雷」的话，避的是**自己的思维懒惰**，不是某个工具。

### 5.4 一句话总结

> PM 焦虑「用哪个 AI 工具」。
>
> **但真正决定你能不能用好 AI 的，从来不是工具——是你能不能把需求说清楚。**

---

## 六、数据更新计划

| 季度 | 重审项 | 负责人 |
|---|---|---|
| **2026-Q3** | 定价（Claude Code Max / Cursor Ultra / Devin Team） + 新增工具 | 蔡逸雯 |
| **2026-Q4** | benchmark 数据 + 案例 | 蔡逸雯 |
| **2027-Q1** | 全表重审（含中文区是否破信息差） | 蔡逸雯 |

---

## 七、引用规范（Pool 位置 + 已核 URL）

| 数据 / 引用 | 来源 | 参照库位置 | 已核 URL |
|---|---|---|---|
| 95% 工程师每周用 AI / 75% 一半工作用 AI / 55% 用 agent | Pragmatic Engineer《AI Tooling for Software Engineers in 2026》(2026-02) | **Pool 9.4** | [newsletter.pragmaticengineer.com/p/ai-tooling-2026](https://newsletter.pragmaticengineer.com/p/ai-tooling-2026) |
| Claude Code 121k GitHub stars (2026-05) | GitHub anthropics/claude-code | — | [github.com/anthropics/claude-code](https://github.com/anthropics/claude-code) |
| Aider ~45k stars / Paul Gauthier 一人维护 | Pool 8.8 Aider | **Pool 8.8** | [aider.chat](https://aider.chat) / [github.com/Aider-AI/aider](https://github.com/Aider-AI/aider) |
| Cline ~61k stars / VS Code 可视化审批 | Pool 8.10 Cline | **Pool 8.10** | [github.com/cline/cline](https://github.com/cline/cline) |
| Devin $26B post-money 估值 / Mercedes 8 天 vs 8 个月 | Pool 8.11 Cognition Devin | **Pool 8.11** | [cognition.ai](https://cognition.ai) / [cognition.ai/blog/devin-2](https://cognition.ai/blog/devin-2) |
| Devin 2.0 从 $500 降到 $20 | VentureBeat 2026 | Pool 8.11 | [venturebeat.com Devin 2.0](https://venturebeat.com/programming-development/devin-2-0-is-here-cognition-slashes-price-of-ai-software-engineer-to-20-per-month-from-500) |
| Anna Arteeva 总结金句 | Pool 1.13 Anna Arteeva | **Pool 1.13** | [annaarteeva.medium.com](https://annaarteeva.medium.com/the-vibe-coders-prompting-guide-e04ba0295a18) |
| Claude Code 定价 | Anthropic 官方 (2026-05) | — | [claude.com/product/claude-code](https://claude.com/product/claude-code) |
| Cursor 定价 | Cursor 官方 | — | [cursor.com/pricing](https://cursor.com/pricing) |
| Lovable 定价 | Lovable 官方 | — | [lovable.dev/pricing](https://lovable.dev/pricing) |
| Bolt.new 定价 | StackBlitz 官方 | — | [bolt.new/pricing](https://bolt.new/pricing) |
| v0 定价 | Vercel 官方 | — | [v0.app/pricing](https://v0.app/pricing) |
| Replit 定价 | Replit 官方 | — | [replit.com/pricing](https://replit.com/pricing) |
| Devin 定价 | Devin 官方 | Pool 8.11 | [devin.ai/pricing](https://devin.ai/pricing/) |
| StackBlitz $20M ARR | Sacra | — | [sacra.com/c/bolt-new/](https://sacra.com/c/bolt-new/) |
| r/LocalLLaMA 社区共识 | Pool 9.11 | **Pool 9.11** | [reddit.com/r/LocalLLaMA](https://reddit.com/r/LocalLLaMA) |

**参照库全文（128 条全球 tier-1 源）**：`/Users/caiyiwen/ai-product-column-research/tools/_global-references.md`

---

## 八、设计依据 & 批判性自评 v1.0 ⭐

### 8.1 这份横评的 3 个全球 tier-1 参照

| 参照 | 我借鉴了什么 | 我没采用什么 | 原因 |
|---|---|---|---|
| **Pragmatic Engineer《AI Tooling 2026》调研** | 工具排名口径 + 95%/75%/55% 三个硬数据作为引言 | 全工具长 tail 排名（30+ 工具） | PM 只需 9 选 1 |
| **Anna Arteeva Vibe-Coder's Prompting Guide** | "Lovable 赢非技术 PM / Bolt 赢速度..." 金句作为派系划分锚 | 她针对 marketing 人群的具体 prompting 模板 | 本表服务 PM 不是 marketer |
| **vibecoding.gallery + cleverhack AI Coding Landscape 2026** | 34 工具对比的列结构 | 全部 34 个工具 | 34 工具对 PM 决策太重，9 工具是「能决策」的极限 |

### 8.2 为什么选这 9 个而不是其他组合

| 替代方案 | 优势 | 缺点 | 拒绝原因 |
|---|---|---|---|
| **6 工具版**（去掉 Aider / Cline / Devin） | 表更短 | 漏掉 terminal 派 + autonomous 派 | **太窄** |
| **34 工具全景** | 最全 | PM 看完不会做决策 | **太宽** |
| **15 工具版**（加 Copilot / Codeium / JetBrains AI 等） | 较全 | Copilot / Codeium 已是默认装在 IDE 的工具 | **冗余** |
| **加中文区工具**（Manus / 天工 / Trae / Lingma 等） | 中文区 PM 友好 | 参照库原则"国内市场存在信息差，不参考" | **信息差风险** |
| **9 工具 = 4 派系完整覆盖**（本版） | 派系结构清晰 + 每派代表完整 + PM 5 分钟可决策 | 没真 PM 群体测试 | **✅ 选这个** |

### 8.3 已知盲区 + 后续验证计划

| 盲区 | 影响 | v1.1 计划 |
|---|---|---|
| ⚠️ **未做真 PM 群体测试** (n=0) | 不知道决策表在真实 PM 选型时的"误推率" | v1.1 找 5 个真 AI PM 用决策表选 1 个工具用 1 周 |
| ⚠️ **5/9 款蔡逸雯没亲测** | Bolt / Replit / Aider / Cline / Devin 评价基于二手资料 | v1.1 蔡逸雯亲测 Bolt + Cline 至少 1 周 |
| ⚠️ **没覆盖"组合用法"** | 真实 PM 多是组合用 | v1.1 加第 4.6 节"3 套主流组合工作流" |
| ⚠️ **企业级合规维度缺失** | Devin Enterprise / Claude Code Enterprise 的 SOC2 / VPC 对比没做 | v1.2（企业 PM 受众扩展时再补） |
| ⚠️ **中文区横评缺位** | 国内 PM 看完还要单独查 Manus / 天工 | 不补在本表（保持全球 tier-1 一致性）。中文区单独出第 17 篇附录 B |

### 8.4 适用 / 不适用边界

- ✅ **适用**：PM 第一次选 vibe coding 工具
- ✅ **适用**：PM 已经用 1 个想换 / 想加第 2 个
- ✅ **适用**：1 人创业者 / 小团队 lead 选工具栈
- ❌ **不适用**：纯工程师选工具（应看 Pragmatic Engineer 原调研）
- ❌ **不适用**：企业级合规选型（应看各家 Enterprise 合同 + SOC2 报告）
- ❌ **不适用**：中文区合规重的 PM 选型（本表故意不收中文工具）
- ❌ **不适用**：选 LLM 模型本身（这是选"上层 agent 工具"不是选模型）

### 8.5 这份横评的"调研依据深度等级"

| 元素 | 等级 | 依据 |
|---|---|---|
| 引言三大数据（95% / 75% / 55%） | **L1** | Pragmatic Engineer 2026 近千人调研 |
| Claude Code 121k / Aider 45k / Cline 61k stars | **L1** | GitHub 公开数据 + 三方报道交叉 |
| Devin $26B 估值 / 89% 自家代码 Devin 写 | **L1** | Pool 8.11 公开融资 + 官方 blog |
| 派系 4 分类 | **L2** | Anna Arteeva 总结 + 蔡逸雯归纳 |
| 9 工具选哪 9 个 | L3 | 蔡逸雯设计判断（基于 Pool 8 + Pool 9） |
| 用户场景决策表 9 行 | L3 | 蔡逸雯设计判断（基于 4/9 亲测 + 5/9 二手） |
| 蔡逸雯个人横评 5.1-5.4 | **L4** | 占位待审改 |
| "上手时间"列具体数字 | L3 | 蔡逸雯估算 + 社区共识混合 |

---

## 九、文末微信钩子

```
─────────────────────────────
📦 配套资源 · 第 17 篇

加我微信 **CYW960325**（备注「专栏17」），免费领：
✓ 9 种 Vibe Coding 工具横评表（含定价、案例、推荐场景）
✓ Claude Code 起手 prompt 模板（PM 专用 3 套）
✓ PM × Claude Code 工作流 SOP

【3 种格式任选】
📄 PDF：加微信后直接发文件给你
🔗 腾讯文档：微信里直接打开（推荐 📱）
💻 GitHub Pages：长期收藏 / 外链分享
─────────────────────────────
```

---

> 蔡逸雯 · 8 年 QE → AI PM · 公众号「蔡逸雯」
> CC-BY-NC 4.0 · 转载请注明出处
> 本表数据基线 2026-05 · 每季度更新 · 见第六节更新计划
