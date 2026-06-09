# BlackieDM Blog — AI Series Plan

## 系列概述

每天发布一篇 AI 相关博客，中英双语，7个栏目循环轮转（不绑定到固定星期几）。

## 7 个固定栏目

| # | 栏目名 | 英文标签 | 内容定位 | 参考 Jekyll tags |
|---|---|---|---|---|
| 1 | **模型速递** | Model Watch | 最新模型发布、能力评测、Benchmark 横评、版本更新解读 | `model-watch` |
| 2 | **工程实战** | Engineering in Practice | RAG / Agent / MCP 架构实践、代码模式、生产部署经验、Context Engineering | `engineering` |
| 3 | **论文解读** | Paper Decoded | 重要 AI 研究论文拆解，用工程师语言讲清楚核心贡献与应用价值 | `paper` |
| 4 | **产品拆解** | Product Teardown | AI 产品深度分析、功能拆解、UX 模式、竞品对比 | `product` |
| 5 | **商业战略** | Business & Strategy | 融资动态、商业模式、竞争格局、市场趋势、头部公司战略解读 | `business` |
| 6 | **监管与安全** | Regulation & Safety | 全球 AI 政策、合规动态、AI Safety、数据治理、伦理议题 | `regulation` |
| 7 | **开发者生态** | Dev Ecosystem | 开源工具、框架库、API 变化、开发者工具链、生态系统动态 | `devtools` |

## 轮转规则

- 严格按 1→2→3→4→5→6→7→1→… 顺序轮转，不跳号
- 每次新建文章前，从本文件 `## 轮转状态` 区块查看下一篇应写哪个栏目
- 写完后更新 `## 轮转状态` 中的计数器

## 轮转状态

```
上一篇栏目编号: 1  (模型速递 / 全景扫描)
上一篇发布日期: 2026-06-09
下一篇栏目编号: 2  (工程实战 / Engineering in Practice)
下一篇发布日期: 2026-06-10
```

## 文章格式规范

### Jekyll Front Matter

```yaml
---
layout: post
title: "【栏目名】文章标题 | English Subtitle"
date: YYYY-MM-DD HH:MM:SS
categories: AI
tags: [栏目tag, 相关tag1, 相关tag2]
series: "每日AI洞察"
column: "栏目名（中文）"
---
```

### 文件命名

```
YYYY-MM-DD-column-slug-keywords.md
```

示例：
- `2026-06-10-engineering-mcp-agent-patterns.md`
- `2026-06-11-paper-decoded-graphrag.md`

### 文章结构模板

```markdown
*[一句话英文摘要，供英文读者快速定位]*

---

## 一、[引入/背景]

[中文正文，关键术语保留英文]

*[English summary of this section in italics]*

---

## 二、[主体内容]

...（3-5个二级章节）...

---

## [本篇要点 / Key Takeaways]

1. ...
2. ...
3. ...

---

*Sources:*
- [来源标题](URL)
```

### 字数参考

- 模型速递：800-1200字（信息密度高，表格为主）
- 工程实战：1200-2000字（代码/架构图/步骤为主）
- 论文解读：1000-1500字（背景+核心贡献+工程意义）
- 产品拆解：800-1200字（截图/对比表格为主）
- 商业战略：800-1200字（数据+分析为主）
- 监管与安全：800-1200字（法规原文引用+影响分析）
- 开发者生态：1000-1500字（工具介绍+使用场景）

## 写作流程（每次执行步骤）

1. 查看本文件 `## 轮转状态`，确认下一篇栏目
2. 使用 `deep-research` skill 搜索该栏目相关最新内容
3. 按上述格式规范撰写文章
4. 文件保存至 `_posts/YYYY-MM-DD-*.md`
5. `git add` + `git commit` + `git push`
6. **更新本文件 `## 轮转状态`**，计数器 +1
