# 17 · PM 的新杠杆——用 Claude Code 不依赖工程师跑通验证 ⭐

> 第一季《AI 时代 PM 工作流重构》· 第 17 篇 · 第四部分 交付
> 预估字数：6000（专栏杀手锏，最长篇之一）

---

第十六个"不以为然"——**也是这本专栏最关键的一篇**——

**90% 的 PM 还在「等工程师才能验证需求」**。

不是 PM 不想自己跑通。是大多数 PM **以为"代码是工程师的事，PM 不用碰"**——结果一个 3 小时就能验证的需求，**走"评审 → 立项 → 排期 → 开发"流程需要 2-4 周**——而那 2-4 周里别人用 Claude Code 已经验证了 10 个需求。

读完这一篇你会知道——**PM 用 Claude Code 不是替代工程师，是给自己装一个验证杠杆**。但用法有讲究——**半懂比不懂更危险**。

---

## 上半篇 · workflow

### PM 用 Claude Code 的最小路径

**你不需要会写代码，但要会跑通验证**。

具体路径：

```
Step 1：装 Claude Code（5 分钟）
  → npm install -g @anthropic-ai/claude-code
  → 在终端运行 `claude`
  → 配置 API key

Step 2：开新项目目录（隔离环境）
  → mkdir prototype-xxx
  → cd prototype-xxx
  → 不要在生产 repo 里玩

Step 3：写一份 markdown 需求（10 分钟）
  → 创建 prd.md
  → 写清楚：goal / 输入输出 / API 契约示例

Step 4：让 Claude Code 跑通（30 分钟-3 小时）
  → "Read prd.md. Build the smallest working prototype."
  → 看跑通 → 改 prompt → 再跑

Step 5：判断（10 分钟）
  → 跑通了 → 决定要不要立项
  → 跑不通 → 砍掉需求
```

**全流程 < 4 小时**——比传统"评审 → 立项 → 排期 → 开发"快 1-2 个月。

### 适用场景（5 类）

PM 用 Claude Code 适合：
1. **能力快速验证**：模型能不能做这个任务
2. **Prompt 调试**：哪个 prompt 效果最好
3. **MVP 原型**：给老板 / 客户演示用
4. **Bad case 复现**：生产环境的 case 在本地跑一遍
5. **跨系统拉数据**：Linear / Slack / GitHub 拉数据写周报

### 不适用场景（5 类）

PM 用 Claude Code **不**适合：
1. **生产代码**：你写的代码不能上线，必须工程师重写
2. **性能敏感**：高并发 / 低延迟 / 高 QPS 路径
3. **复杂前端**：长期维护的 UI / 复杂状态管理
4. **跨系统集成**：webhook / 回调 / 消息队列正式上线
5. **关键业务逻辑**：订单 / 计费 / 风控

**一句话边界**：**能扔的，PM 自己写；不能扔的，给工程师**。

### PM 的 Claude Code 5 步循环

```
Step 1：开新项目（隔离环境）
   ↓
Step 2：说清需求（PRD/markdown）
   ↓
Step 3：看跑通（让它真的运行）
   ↓
Step 4：改 prompt 而不是改代码（成本左移）
   ↓
Step 5：收敛（明确 demo 性质，决定下一步）
```

**关键反共识**：**改 prompt 而不是改代码**。

PM 不要陷入"改代码"——那是工程师的事。PM 应该改 markdown / prompt——让 Claude Code 再跑一遍。

**这是 PM 杠杆的核心**。

---

## 7 个 PM 用 Claude Code 的真实 prompt（可直接抄）

### 场景 1：30 分钟验证一个 AI 需求是否可行

```
Read PRD.md in this folder. Build the smallest possible working
prototype that validates the core hypothesis: "用户可以上传一段
微信聊天记录，AI 自动总结对方的性格"。
Use Anthropic's claude-sonnet API. UI 用最简单的 HTML 页面。
不要写测试，不要做错误处理，不要部署。跑通后告诉我怎么本地启动。
```

- **预期输出**：一份能跑的脚本 + 一个本地端口
- **验证什么**：核心 AI 能力是否能交付想要的输出质量
- **踩坑**：别让它做"完整版"——明确说 "smallest possible"

### 场景 2：复现一个生产环境的 bad case

```
这是用户报告的 bad case：[贴完整输入] → 我们的 AI 回答了：[贴输出]。
用户期望：[贴期望]。
请：1) 在我的 codebase 里找到处理这个 case 的 prompt 模板路径
    2) 用同样的输入本地复现一遍
    3) 给出 3 个可能的根因排序。
不要修改代码。
```

- **验证什么**：bad case 是 prompt 问题、模型问题还是数据问题
- **踩坑**：不加"不要修改代码"它会自己开始改，把根因覆盖掉

### 场景 3：调试一个 prompt

```
我有一个 prompt 在 ./prompts/summarizer.md。
跑 10 个测试样例（在 ./test_cases.jsonl），告诉我：
- 哪些 case 失败了
- 失败模式分类（幻觉/格式错/漏信息/啰嗦）
- 给出 3 个 prompt 改写版本，按预期改善程度排序
```

- **验证什么**：prompt 边界与失败模式
- **踩坑**：要给真实 test cases，不要让它自己造样例（会捡软柿子）

### 场景 4：给老板演示的 MVP 原型

```
读 prd.md。做一个纯前端的 clickable demo，所有数据用 mock。
要求：1) 不需要任何后端
     2) 看起来像真的产品（用 Tailwind）
     3) 用户能完整走一遍核心流程 3 个步骤
     4) 跑 npm run dev 就能看
```

- **注**：这个场景 v0 / Lovable 比 Claude Code 更高效，除非你需要 Claude Code 的 codebase 上下文

### 场景 5：测试一个 RAG 流程的可行性

```
我要验证：把我们 200 篇知识库文档 chunk + embed 后，能否答对
./eval_questions.txt 里的 50 个问题。
请：1) 用 LangChain + Chroma 跑一个最简 pipeline
    2) 输出每个问题的 retrieve top-3 片段 + 生成答案 + 是否命中标准答案
    3) 给出整体准确率
不要做 reranker、不要 hybrid search，先看 baseline。
```

- **验证什么**：RAG baseline 准确率，决定要不要立项
- **踩坑**：一上来就让它加 reranker / fine-tune，看不出 baseline 真实水平

### 场景 6：评估一个新功能的工程复杂度

```
读完整个 src/ 目录。我想加这样一个功能：[描述]。
请告诉我：1) 涉及哪些现有文件
        2) 需要新建哪些
        3) 哪些地方跟现有逻辑冲突
        4) 一个有经验的工程师做这个估计要几天。
不要写代码，只给评估。
```

- **验证什么**：在跟工程师沟通前对复杂度的预判
- **踩坑**：它会高估自己的判断——一定要把结论拿给工程师 sanity check

### 场景 7：跨系统拉数据做周报

```
通过 MCP 拉取：
1) 过去 7 天 Linear 上 status=done 的 ticket
2) 同期 #checkout-project Slack 频道的高赞消息
3) GitHub main 分支合并的相关 PR
合成一份给 CEO 看的周报，重点突出"用户可见的变化"和"卡住的事情"。
```

- **验证什么**：跨系统信息整合能力——**这是 Claude Code 相对 v0 / Lovable 的真正优势**

---

### Claude Code 之后的下一代 PM 工具

写到这里要把视野抬一层——**Claude Code 是 2025-2026 上半年的杠杆，不是终极形态**。

2026 年下半年起，业内 PM 工具栈正在向 4 个方向位移：

**从 Claude Code → Agent SDK**。Anthropic 2026-06 把 Agent SDK / `claude -p` 切到独立 monthly credit——意味着 PM 的工作单位从"我敲一个 prompt"升级为"我派一组 agent 跑一个任务"。PM 不再坐在终端前等回应，**开个会回来看 sub-agent 编队的 outcome 报告**。

**从手写 prompt → 自建 Skills**。Skills 是 filesystem-based 的"领域专家包"——客户访谈合成 / eval 跑批 / bad case 分类，每一个都是一个可复用的 skill 包。Sachin Rekhi 现在带 PM 的方向已经从"7 个 prompt"切到"13+ 个 skills"——**PM 的资产从"prompt 笔记"升级为"个人 skill 库"**。

**从单 agent → Sub-agent 编队**。一个 lead agent 派 N 个 specialist sub-agent 并行跑（每个独立 model / prompt / tools），最后 Outcomes grader 判收敛——**PM 设计的不再是 prompt，是编队拓扑**。

**从对话式 UI → Generative UI**。Vercel AI SDK 3 + json-render + Google A2UI 正在让 LLM 直接生成 React 组件——**产品的"界面"从设计师交付物变成运行时 LLM 输出**，PM 的 mockup 思维要彻底重写。

7 个 prompt 模板今晚就能用——同时留意接下来这 4 个位移。6 个月后回头看——**只会敲 prompt 而不会编排 skill + sub-agent 的 PM，会发现自己只在用 2026 上半年的工具栈**。

---

## 工具对比：6 个 vibe coding 工具的 PM 视角

| 工具 | PM 上手难度 | 最适合的 PM 场景 | 不适合 |
|------|-----------|----------------|-------|
| **Claude Code** | 中（需开终端）| 跨文件改动、读代码库、复现 bad case、跑 agent/RAG、连 Linear/Jira/Slack MCP | 纯 UI mockup |
| **Cursor** | 中高（IDE 形态）| 已有代码库的 PM 想读懂工程师写的逻辑 | 完全没碰过 IDE 的 PM |
| **v0** | 低 | UI mockup、设计稿到代码 | 后端逻辑、Agent 流程 |
| **Lovable** | 最低（浏览器内）| 非技术 PM 的端到端可上线小工具 | 复杂自定义、性能敏感 |
| **Bolt.new** | 最低 | 30 分钟内出 clickable demo | 持续维护的代码 |
| **Replit Agent** | 中 | 全栈小工具 | 纯 mockup |

**Anna Arteeva 的总结被引用最多**：

> "Lovable 赢非技术 PM，Bolt 赢速度，v0 赢 UI，Replit 赢全栈，Cursor / Claude Code 赢工程深度。"

### PM 怎么选

| PM 场景 | 推荐工具 |
|---------|---------|
| 第一次玩 | **v0 / Lovable**（不需要终端）|
| 验证 AI Agent / RAG 流程 | **Claude Code**（唯一能直接调 API、装 SDK）|
| 给老板演示 | **v0** |
| 验证可上线小工具 | **Lovable / Replit** |
| 复现工程师的 bad case | **Claude Code**（必须能读真实 codebase）|

---

## 下半篇 · engineering reality

### 业内 PM 用 AI Coding 的真实案例

#### Dennis Yang（Chime PM）—— 标杆案例
- markdown 写 PRD → 终端打开 `claude` → **20 分钟跑出可点击原型** → Slack 录屏分享
- 这是"PRD 即可执行规范"最早被传播的具体操作版

#### Lenny Rachitsky 的核心观点（2026-02 文章）
> "Everyone should be using Claude Code more"

他公开收集了 **50 个非技术用户的 Claude Code 用例**。核心观点：

> "**忘掉它叫 Claude Code，把它当作 Claude Local / Claude Agent**。"

#### Sachin Rekhi（前 LinkedIn / Reforge 讲师）—— 最系统
- **1500 个 PM 参加的 webinar** 上展示了 **13 个自建 skills**（来源：Sachin 公开 webinar 录像 + sachinrekhi.com 课程页）
- 覆盖：客户访谈合成 / NPS 自治 / 无 SQL 的 EDA / 产品战略 critique / release notes 自动化
- 同期产出 **"AI Prototyping Mastery Ladder"**——**15 个具体技能**按 Apprentice / Journeyman / Master 三档划分（来源：sachinrekhi.com 公开课程页）

#### Boris Cherny（Anthropic Claude Code 负责人）
- Lenny 播客自述：**自 2025-11 起 100% 代码由 Claude Code 写**，自己已不手敲
- Anthropic 内部工作流：**先做 prototype 再 dogfood，并不是先写 PRD 再开发**

#### Cat Wu（Anthropic Claude Code Head of Product）
- Lenny 节目分享：Anthropic 产品团队"为什么比所有人都快"
- **PM/Designer/Eng 都用 Claude Code 直接产出 working prototype 评审**，而不是 Figma + 文档

### 4 个常见陷阱

#### 陷阱 1：沉迷写代码，PM 越写越不像 PM

**案例**：业内 KOL 多次警告：
> "PM 花几小时几天 vibe code 原型，就没花在用户访谈、跨部门影响、战略规划上。"

**怎么识别**：一周内你打开 Claude Code 比打开访谈记录的次数多。

**怎么避免**：给自己设硬上限——验证一个假设最多 2 小时；超过就停下来问"**为什么我自己写而不是让工程师评估？**"

#### 陷阱 2：把 demo 当产品（验证级 ≠ 生产级）

**关键警告**：Retool 调研：**vibe-coded app 接真数据库时 SQL 注入是"等待发生的数据泄露"**。

**怎么识别**：你开始考虑"要不要让真实用户用一下"。

**怎么避免**：
- 从一开始命名就叫 `prototype-xxx`，不要叫 `feature-xxx`
- 明确 demo 不接生产 DB / 不存真用户数据

#### 陷阱 3：不读代码就提交

**业内案例**：某团队 critical path 陷阱——agent 把成就系统逻辑塞进游戏主循环里，让最热的代码膨胀两倍。

**怎么识别**：你 review 时连"它改了哪几个文件"都说不清。

**怎么避免**：
- 每次让它先 plan 再 execute
- 提交前必须能用一句话解释每个改动
- 改 critical path（登录、支付、核心循环）必须找工程师

#### 陷阱 4：用 Claude Code 替代沟通

**业内引语**：
> "如果一个功能重要到你急着 vibe code，那它就重要到该让团队优先做。"

**核心矛盾**：PM 自己跑通 ≠ 团队能 ship。

**怎么避免**：跑通的第一件事是录屏 + 标 "validation only, not production"，主动拉工程师看 5 分钟，问的不是"能不能上线"而是"**我的假设对吗**"。

### 验证级 vs 生产级 边界

#### PM 能做（验证级，7 类）：
1. **AI 能力探针**：调一个模型 API、试几个 prompt、看输出质量
2. **本地 mock 数据 demo**：纯前端 + 假数据
3. **bad case 复现脚本**：复现一次就丢
4. **数据探索 / EDA**：CSV → 图表 → 洞察
5. **跨系统信息合成**：Linear+Slack+GitHub 拉数据写周报
6. **小工具内部用**：自己用、最多团队用、不联生产数据
7. **prompt 评测台**：跑测试集对比多个 prompt 版本

#### PM 不要做（生产级，7 类）：
1. **接生产数据库**（写权限尤其危险）
2. **用户认证 / 鉴权 / 支付** 相关代码
3. **关键业务逻辑**（订单、计费、风控）
4. **性能敏感模块**（高并发、低延迟、高 QPS 路径）
5. **跨系统集成正式上线**（webhook、回调、消息队列）
6. **复杂前端状态管理 / 长期维护的 UI**
7. **任何会影响其他工程师 codebase 的改动**（critical path / 公共组件）

### 一句话边界

> **能扔的，PM 自己写；不能扔的，给工程师。**

---

## 质量工程视角看 PM 的 Claude Code 杠杆

**8 年做软件质量工程的视角**——

任何工程领域的进化都遵循一个规律：**把验证成本从"高门槛专业角色"下放到"业务角色"**。

- 30 年前：测试需要硬件实验室 + 专业仪器
- 20 年前：测试需要自动化框架 + QA 工程师
- 10 年前：测试需要 CI/CD pipeline + 工程师
- 现在：**测试需要 markdown PRD + Claude Code + PM 自己**

Claude Code 不是 PM 的新工具——**是把"验证"这个动作从工程师下放到 PM**。

这意味着 PM 的工作发生根本变化——**从"等验证结果"变成"自己跑验证"**。等的人会被甩开 10 倍速度。跑的人成为新一代 PM。

---

## 给你的可执行清单

#### 动作 1：今天就装 Claude Code
- `npm install -g @anthropic-ai/claude-code`
- 配置 API key
- 用 5 步循环跑一个最小验证

#### 动作 2：把 7 个 prompt 收藏起来
- 7 个场景的真实 prompt 已经给你
- 直接 copy-paste 改一下场景就能用

#### 动作 3：你下一个需求评审前 3 小时跑一次验证
- 在评审前用 Claude Code 跑通
- 评审会直接放 demo 给所有人看
- 评审效率提升 5 倍

#### 动作 4：把 4 个陷阱贴在工位
- 沉迷写代码 / demo 当产品 / 不读代码 / 替代沟通
- 每次打开 Claude Code 前问自己一遍

---

## 反共识金句

- **"PM 的新杠杆不是写代码，是把'要不要立项'的决策成本从 2 周压到 2 小时。"**
- **"Lenny 说得对：忘掉它叫 Claude Code，它是你的 Local Agent。"**
- **"PRD 不死，但 PRD 的下一个读者是 AI——能被 AI 一次跑通的 PRD，才是好 PRD。"**
- **"AI 把 PM 从'催排期的人'变成'先验证假设再排期的人'——这才是杠杆。"**

---

## 写在最后

这一篇是专栏的杀手锏。

读完应该有 3 个动作：
1. 装 Claude Code
2. 把 7 个 prompt 试一遍
3. 下一个需求评审前跑一次验证

下一篇讲 AI 产品的灰度策略——**和传统功能灰度的根本不同**。

prompt 版本、模型版本、参数版本的多轴切换。多轴灰度怎么设计、影子流量（shadow traffic）业内最佳实践、Notion 70 个工程师靠双轨 eval 活下来的真实案例。

下一篇见。

---

> **本文配套资产**：PM 专用 Claude Code 脚手架（含 prompt 模板、目录结构）+ 5 步循环 checklist（付费读者解锁）⭐ 重磅
> **下一篇预告**：18 · AI 产品的灰度策略——传统 A/B 失效之后
> **反馈 / 加入读者群**：欢迎在公众号「蔡逸雯」留言
