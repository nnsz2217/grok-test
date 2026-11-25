# Anthropic 官方 Skills（anthropics/skills）与 Claude Code 内置技能

这是 Anthropic 公开的官方技能仓库，再加上 Claude Code 文档里列出的**内置（bundled）**技能。两者都是官方材料，但不是同一件事：前者是可以查看源码、按插件市场安装的公开示例与文档技能；后者随 Claude Code 一起提供，本批没有在公开仓库里读到这些内置技能的 `SKILL.md` 原文。

## 基本信息

- **名称**：Skills（Anthropic 对 Claude 的技能实现与示例仓库）
- **GitHub**：[github.com/anthropics/skills](https://github.com/anthropics/skills)
- **规范站点**：仓库 README 指向 [agentskills.io](https://agentskills.io)，并写明本仓库是 Anthropic 对 Claude 的实现，标准本身见规范站点。
- **作者 / 团队**：Anthropic
- **最近推送**：GitHub API 记录 `2026-11-16T14:22:50Z`（换算为 2026-11-16 22:22，Asia/Shanghai）。未归档。
- **热度快照**：2026-11-25（Asia/Shanghai）查询时 200,160 stars、23,409 forks。只是当天数字，不是质量排名。
- **开源许可证**：GitHub API 在仓库级未返回 SPDX 许可证（根目录也没有 `LICENSE` 文件）。README 写明「Many skills in this repo are open source (Apache 2.0)」；本批实际打开了 `skills/pdf/LICENSE.txt` 和 `skills/skill-creator/LICENSE.txt`，均为 Apache License 2.0。根目录另有 `THIRD_PARTY_NOTICES.md`，为随附第三方组件做归属说明。使用某个子技能前，应再看该技能目录自己的 `LICENSE.txt`。
- **仓库自我定位**：演示和教学用途。README 的 Disclaimer 写明：其中一些能力可能已出现在 Claude 产品中，但你从 Claude 得到的实现和行为可能与仓库里展示的不同；用于关键任务前要在自己的环境里充分测试。

## 它能完成什么，和普通聊天有什么区别

普通对话里，模型主要靠通用能力和你当场粘贴的说明。这里的 Skill 把「怎么处理 PDF / 怎么写一个新技能」等可重复流程写成文件夹：智能体先根据简介决定要不要用，再用正文和脚本把步骤跑稳。

仓库顶层真实结构（GitHub Contents API，2026-11-25 查询）：

```
.claude-plugin/     # 作为 Claude Code 插件市场的元数据
README.md
THIRD_PARTY_NOTICES.md
skills/             # 示例与文档技能
spec/               # Agent Skills 规范副本（本批未展开阅读该目录全部文件）
template/           # 仅含一份模板 SKILL.md
```

`skills/` 下本批核到的子目录共 19 个：`academy-guide`、`algorithmic-art`、`brand-guidelines`、`canvas-design`、`claude-api`、`discernment-nudge`、`doc-coauthoring`、`docx`、`frontend-design`、`internal-comms`、`mcp-builder`、`pdf`、`pptx`、`skill-creator`、`slack-gif-creator`、`theme-factory`、`web-artifacts-builder`、`webapp-testing`、`xlsx`。

README 特别指出：`skills/docx`、`skills/pdf`、`skills/pptx`、`skills/xlsx` 是驱动 [Claude 文档能力](https://www.anthropic.com/news/create-files) 的文档创建与编辑技能，同样以 Apache 2.0 公开，作为「生产环境里更复杂技能」的参考。

## 安装与使用（官方说明，本批未实际执行安装）

### Claude Code

仓库 README 给出的安装方式是把它注册为插件市场：

```
/plugin marketplace add anthropics/skills
```

然后在界面中选择 `anthropic-agent-skills`，再安装 `document-skills` 或 `example-skills`；或直接：

```
/plugin install document-skills@anthropic-agent-skills
/plugin install example-skills@anthropic-agent-skills
```

官方使用示例（来自 README，不是本批实测）：安装 `document-skills` 后，可以对 Claude Code 说：`Use the PDF skill to extract the form fields from path/to/some-file.pdf`。

自己写的技能，按 [Claude Code Skills 文档](https://code.claude.com/docs/en/skills) 放到：

| 范围 | 路径 |
| --- | --- |
| 个人（本机所有项目；文档写明不用于 Cowork 或云端会话） | `~/.claude/skills/<name>/SKILL.md` |
| 项目（提交后团队可共享） | `.claude/skills/<name>/SKILL.md` |
| 企业托管配置 | 受管设置目录下的 `.claude/skills/` |

文档还写明：可以用 `/skill-name` 显式调用；也可以让 Claude 按 `description` 自动选用。自定义命令已经并入 skills，旧的 `.claude/commands/` 仍可用。

### Claude.ai 与 API

README 写明：这些示例技能在 Claude.ai 的**付费方案**中已经可用；上传自定义技能见 [Using skills in Claude](https://support.claude.com/en/articles/12512180-using-skills-in-claude)（本环境复查该链接时会跳到同编号文章的当前 slug：`.../use-skills-in-claude`）。API 方面，README 指向 [Skills API Quickstart](https://docs.claude.com/en/api/skills-guide#creating-a-skill)。**本环境在 2026-11-25 用 curl 跟踪 `docs.claude.com` 与 `platform.claude.com` 时，被转到 `https://claude.com/app-unavailable-in-region`，未能复核 API 文档正文。** 链接保留，内容以你本地能打开的官方页为准。

### 是否需要编程、服务器、API Key

- 查看和阅读这些 `SKILL.md`：不需要自己部署服务器。
- 在 Claude Code / Claude.ai 里使用：需要相应产品账号。文档技能会调用本地或环境中的 Python 库、命令行工具（如 `pypdf`、`pdfplumber`、`qpdf`），这属于「技能在已有工具上编排」，不是另建一台服务器。
- 是否需要 API Key：用 Claude API 上传或调用技能时需要 Anthropic API 凭证；仅在 Claude Code 或 Claude.ai 里用，则走该产品登录，不额外等同于「必须自备服务器」。具体套餐价格本批未从结算页核对，不编造。
- Windows：Claude Code 官方文档给出的是通用路径约定。本批没有在 Windows 上实测安装。

## 本批实际读过的代表性 SKILL.md

下面只写打开过源码的技能。其余 19 个目录中未读到的，不根据名字推测功能。

### 1. `template/`（入门模板）

路径：[template/SKILL.md](https://github.com/anthropics/skills/blob/main/template/SKILL.md)。目录里只有这一份文件，全文很短，frontmatter 为：

```yaml
name: template-skill
description: Replace with description of the skill and when Claude should use it.
```

正文只有一句：`# Insert instructions below`。适合当空白骨架，本身不是可工作的业务流程。

### 2. `skill-creator`（编写和评估技能的元技能）

路径：[skills/skill-creator/SKILL.md](https://github.com/anthropics/skills/blob/main/skills/skill-creator/SKILL.md)。本批打开的正文约 485 行。

- **description（原文）**：Create new skills, modify and improve existing skills, and measure skill performance. Use when users want to create a skill from scratch, edit, or optimize an existing skill, run evals to test a skill, benchmark skill performance with variance analysis, or optimize a skill's description for better triggering accuracy.
- **真实目录**：`SKILL.md`、`LICENSE.txt`、`agents/`、`assets/`、`eval-viewer/`、`references/`、`scripts/`。正文末尾说明 `agents/` 里有评分、盲比、分析用的子代理说明；`references/schemas.md` 记录评估 JSON 结构。
- **它解决的问题**：把「写技能」本身做成可重复流程：先抓住意图，再写草稿，再用测试提示词跑「有技能 / 基线」对照，和用户一起看结果，然后改写，最后还可以单独优化 `description` 的触发准确度。
- **对写作有用的原设计**：三层渐进披露；`SKILL.md` 理想情况下少于 500 行；大参考文件（>300 行）要有目录；多云或多框架时按变体拆到 `references/`；「不要让技能做出让用户吃惊的事」，禁止把恶意软件或未授权访问写进技能；指令用祈使语气；用「为什么要这样做」代替一味堆 `ALWAYS` / `NEVER`；先写 2–3 条真实测试提示词，存进 `evals/evals.json`。

官方站点 [Optimizing skill descriptions](https://agentskills.io/skill-creation/optimizing-descriptions) 也提到，`skill-creator` 可以自动跑触发评测循环。本批没有实际运行该技能。

### 3. `pdf`（文档技能，生产级参考）

路径：[skills/pdf/SKILL.md](https://github.com/anthropics/skills/blob/main/skills/pdf/SKILL.md)。正文约 314 行。

- **description（原文）**：Use this skill whenever the user wants to do anything with PDF files. This includes reading or extracting text/tables from PDFs, combining or merging multiple PDFs into one, splitting PDFs apart, rotating pages, adding watermarks, creating new PDFs, filling PDF forms, encrypting/decrypting PDFs, extracting images, and OCR on scanned PDFs to make them searchable. If the user mentions a .pdf file or asks to produce one, use this skill.
- **license 字段**：`Complete terms in LICENSE.txt`（Apache 2.0）。
- **真实目录**：`SKILL.md`、`REFERENCE.md`、`FORMS.md`、`LICENSE.txt`、`scripts/`。正文一开始就把高级特性和表单填写指到那两份参考文件，主文件只保留快速开始和常用库（`pypdf`、`pdfplumber`、`reportlab`）以及 `pdftotext` / `qpdf` / `pdftk` 命令。这是规范里「主文件保持精瘦、细节按需加载」的真实例子。
- Anthropic 工程文章 [Equipping agents for the real world with Agent Skills](https://www.anthropic.com/research/equipping-agents-for-the-real-world-with-agent-skills)（页面原工程路径会跳转到 `/research/`；文章日期 Oct 16, 2025）用这个 PDF 技能说明：填写表单时再读 `forms.md`；提取表单字段可以跑预先写好的 Python 脚本，而不必把脚本或整个 PDF 读进上下文。

### 4. `docx` / `xlsx` / `pptx`

三份主文件都已打开。它们与 `pdf` 同属文档技能组，目录里都有 `LICENSE.txt`（本批抽查 `pdf` 与 `skill-creator` 为 Apache 2.0；`docx` 目录同样含 `LICENSE.txt`，未再把全文读完）。`docx` 另有 `scripts/`。这些文件较长（尤其 `pptx` 约 28 KB），本批核对了 frontmatter 和章节结构，没有逐行复述全部操作细节。它们的共同模式是：description 写清「处理该类办公文档时使用」，正文给库与命令级步骤，复杂部分再拆文件或脚本。

### 5. `mcp-builder`（这是技能，不是 MCP 服务器本身）

路径：[skills/mcp-builder/SKILL.md](https://github.com/anthropics/skills/blob/main/skills/mcp-builder/SKILL.md)。这是一份**教智能体如何编写 MCP 服务器**的 Skill，本身不是一个 MCP 工具。正文按「调研规划 → 实现 → 审查测试 → 写评估题」分阶段，并指向 `reference/` 下的 MCP 最佳实践和各语言指南。请不要把它和「已经连好的 MCP 服务器」混为一谈。

## Claude Code 内置技能（官方文档，未读到 SKILL.md 原文）

[Claude Code Skills 文档](https://code.claude.com/docs/en/skills) 列出的 bundled skills 包括：`/doctor`、`/code-review`、`/batch`、`/debug`、`/loop`、`/claude-api`。它们是提示词型技能：给 Claude 详细说明，再让它用已有工具编排。可用 `/` 调用，有些也会在相关时自动启用。可用 `disableBundledSkills` 关闭；文档写明 `/doctor` 在关闭后仍可输入，若要彻底隐藏需另设环境变量或 `skillOverrides`。

文档还说明 Claude Code 在开放规范之外增加了若干字段，例如 `disable-model-invocation`、`when_to_use`、`user-invocable`、`allowed-tools`、`disallowed-tools` 等。这些是产品扩展，不是规范必填项。文档甚至写到：在 Claude Code 里所有 frontmatter 字段都可选，只是强烈建议写 `description`——这与开放规范「`name` 和 `description` 必填」并不完全相同。若要跨产品分发，仍应按规范补全必填项。

## 官方使用与安全提醒

- Anthropic 工程文章建议：只从信任来源安装技能；来源不够可信时，先通读文件，尤其注意脚本、依赖，以及会让模型连接不可信外部网络的指令。恶意技能可能在运行环境中引入漏洞，或引导模型外泄数据、做出非预期操作。
- 仓库 Disclaimer：不要把演示实现当成 Claude 产品行为的保证。

## 优点、局限与费用

优点：有可打开的生产级文档技能源码；`skill-creator` 把评测和触发优化写进了可运行流程；Claude Code 安装路径清楚；与开放规范对齐。

局限：仓库声明以演示和教学为主；Claude.ai / API 文档在本环境存在区域跳转，未能复核；仓库根目录无统一 SPDX；示例技能里既有办公文档，也有偏演示的创作类技能，不能一律当作「日常必装」。

费用：技能源码按各技能 `LICENSE.txt` 使用（本批抽查为 Apache 2.0）。在 Claude 产品中运行这些技能，需要该产品的账号或付费方案。Claude.ai 的示例技能，README 写的是「付费方案已可用」。具体价格未核。API 另计。

## 元数据

- 更新时间：2026-11-25（Asia/Shanghai）
- 来源：
  - [anthropics/skills README](https://github.com/anthropics/skills)
  - 已打开的源码：`template/SKILL.md`、`skills/skill-creator/SKILL.md`、`skills/pdf/SKILL.md`、`skills/docx/SKILL.md`、`skills/xlsx/SKILL.md`、`skills/pptx/SKILL.md`、`skills/mcp-builder/SKILL.md`，以及 `skills/pdf/LICENSE.txt`、`skills/skill-creator/LICENSE.txt`
  - [Claude Code Skills 文档](https://code.claude.com/docs/en/skills)
  - [Equipping agents for the real world with Agent Skills](https://www.anthropic.com/research/equipping-agents-for-the-real-world-with-agent-skills)（从 `/engineering/` 跳转到 `/research/`）
  - GitHub API `https://api.github.com/repos/anthropics/skills`（2026-11-25）
- 信息可信度：部分核对。已打开仓库 README、若干 SKILL.md、Claude Code 文档和工程文章；未实际安装插件或在 Claude.ai 界面点选；`docs.claude.com` / `platform.claude.com` 在本环境跳转到区域不可用页，API 细节未复核；未读完全部 19 个技能目录。
- 平台：已在官方文档中出现的包括 Claude Code、Claude.ai（付费方案）、Claude API。其他客户端若兼容同一格式，理论上可复用这些文件夹，但本批未做跨客户端实测。
- 技能门槛：阅读和复制技能只需会用 Git 和 Markdown；在 Claude Code 里按文档安装属于「简单配置」；要改脚本或跑 `skill-creator` 评测，需要会使用终端和该产品的基本命令。
- 费用：源码抽查为 Apache-2.0；产品侧为付费方案或 API 计费，具体价格未知
