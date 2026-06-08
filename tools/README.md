# tools/ · 9 套配套工具源文件

服务于公众号《AI 时代 PM 工作流重构》第一季的"加微信领配套资源"钩子。

**总进度查询**：见上级目录 `../TODO-9-tools.md`

## 目录结构

```
tools/
├── README.md                          ← 本文件
│
├── # P0 头三篇（17 / 04 / 11）配套
├── 04-伪ai需求6问checklist.md
├── 04-mit-nanda分类表.md
├── 17-vibe-coding-横评表.md
├── 17-claude-code-prompt模板.md
├── 17-pm-claude-code-sop.md
├── 11-prd-4增2删模板.md
├── 11-案例prd-3份.md
│
├── # P1 工具包（边发边补）
├── pack-eval/             # 覆盖 12/13/19/21
├── pack-cost/             # 覆盖 08/09/15
├── pack-capability/       # 覆盖 02/03/05/06/07/10
├── pack-launch/           # 覆盖 14/16/18/20/22
├── pack-collaboration/    # 覆盖 23/24
└── pack-growth/           # 覆盖 01/25/26
```

## 文件状态约定

每个工具文件 frontmatter 含：
```yaml
---
tool_id: P0-04-1
serves_essay: 04
status: draft | review | ready
last_updated: YYYY-MM-DD
deliverable_formats: [markdown, pdf, notion]
---
```

## 交付流程（每个工具）

1. **草稿**：在此目录写 .md
2. **审核**：蔡逸雯审改 + 补真实案例
3. **二次输出**：转 Notion / 飞书 / PDF（视读者方便）
4. **链接固化**：发到公众号文末"加微信领"前一天准备好可访问的下载链接
5. **状态更新**：回 `../TODO-9-tools.md` 改状态符号
