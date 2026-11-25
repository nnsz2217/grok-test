# OpenAI 官方继任来源：Plugins，以及已弃用的 openai/skills

OpenAI 曾经用 [openai/skills](https://github.com/openai/skills) 作为 Codex 的技能目录。该仓库 README 在文首用醒目说明宣布：**This repository is deprecated.** 并要求当前的 Codex 技能与插件示例改用 [openai/plugins](https://github.com/openai/plugins)，自己编写技能则跟随 [Build plugins](https://developers.openai.com/codex/plugins/build)（文档写明包含如何创建仅含技能的插件）。

本笔记把「已弃用目录」和「当前官方示例仓库 + 官方文档」写在一起，避免以后误把旧仓库当成现行安装源。

## 重要复查说明

文档正文此前已通过文档抓取工具读到。但在 2026-11-25（Asia/Shanghai）用 curl 复查下列页面时，统一返回 **HTTP 403**：

- https://developers.openai.com/plugins
- https://developers.openai.com/plugins/build/skills
- https://developers.openai.com/plugins/concepts/skills
- https://developers.openai.com/plugins/build/plugins
- https://learn.chatgpt.com/docs/build-skills
- https://developers.openai.com/codex/plugins/build
- https://developers.openai.com/codex/skills
- https://developers.openai.com/codex/skills/create-skill

链接保留。若你打开时正常，以你浏览器里的官方页面为准；下文中来自这些页面的内容，可信度记为「抓取时已读到，curl 复查失败」。GitHub 仓库和 raw 文件的 curl 复查为 HTTP 200。

## 一、已弃用：openai/skills

- **GitHub**：[github.com/openai/skills](https://github.com/openai/skills)
- **弃用提交**：[778b0e6 Deprecate skills repository (#496)](https://github.com/openai/skills/commit/778b0e6129cf18cbaee3bf11479f583fadae8d03)，提交说明为 “Move users towards Plugins directory for skills and apps.” 作者时间 `2026-06-22T20:36:37Z`（换算为 2026-06-23 04:36，Asia/Shanghai）。
- **仓库状态**：GitHub API 显示**尚未归档**（`archived: false`），最近一次推送 `2026-10-28T17:31:41Z`（2026-10-29 01:31，Asia/Shanghai）。2026-11-25 查询时 29,117 stars、2,061 forks。不要把「还有 star、还没点 Archive」理解成仍是现行官方目录。
- **许可证**：API 未返回仓库级 SPDX；根目录文件只有 `.gitignore`、`README.md`、`contributing.md` 和 `skills/`。README 写明各技能许可证在各自目录的 `LICENSE.txt`。本批没有抽查旧目录里的许可证文件。
- **README 仍保留的旧安装说明**（仅作历史记录，现行来源见下一节）：`.system` 下的技能会随最新版 Codex 自动安装；curated / experimental 技能可在 Codex 里用 `$skill-installer` 按名或 GitHub 目录 URL 安装，之后重启 Codex。
- **与新文档的交叉**： [Build skills | ChatGPT Learn](https://learn.chatgpt.com/docs/build-skills) 在抓取时仍提到，可用 `$skill-installer` 安装 curated skills，并举例 `$skill-installer linear`，也写到可从其他仓库安装。也就是说，**部分官方使用文档在弃用公告之后，仍提到旧仓库的安装器用法**。新工作应以 `openai/plugins` 和 Plugins 文档为准，不要把旧仓库当作「当前官方技能包」来维护或推荐优先安装。

## 二、现行官方示例仓库：openai/plugins

- **名称**：Plugins（README 自称 “a curated collection of Codex plugin examples”）
- **GitHub**：[github.com/openai/plugins](https://github.com/openai/plugins)
- **作者**：仓库由 OpenAI 维护。但「curated collection of examples」意味着其中既有 OpenAI 自己的插件，也有合作方或示例插件。**不能把 `plugins/` 下每一个目录都当成 OpenAI 第一方产品。** 本批只把已打开 `plugin.json`、作者字段写明 OpenAI 的 `openai-developers` 当作第一方样例详写；其他目录只列存在性。
- **最近推送**：`2026-11-18T19:14:28Z`（2026-11-19 03:14，Asia/Shanghai）。未归档。
- **热度快照**：2026-11-25 查询时 8,358 stars、1,109 forks。
- **许可证**：仓库根目录未找到 `LICENSE` / `LICENSE.md` / `LICENSE.txt`。第一方样例 `plugins/openai-developers/.codex-plugin/plugin.json` 的 `"license"` 字段为 **`Proprietary`**。因此不要假定这个仓库里的插件都可以按 Apache / MIT 随意再分发。
- **真实顶层结构**：`.agents/`、`.github/`、`README.md`、`plugins/`。本批用 Contents API 列出 `plugins/` 下 **62** 个目录（adobe、figma、notion、github、openai-developers、plugin-eval、data-analytics、superpowers、vercel 等）。其中 `superpowers` 出现在这个官方示例仓库里，并不等于它是 OpenAI 官方技能包；它的设计方法若在后文工程指南中被提及，只作为社区方法论参考。

README 点名的较丰富示例包括：`plugins/figma`、`plugins/notion`、`plugins/build-ios-apps`、`plugins/build-macos-apps`、`plugins/build-web-apps`、`plugins/expo`，以及 `plugins/netlify`、`plugins/remotion`、`plugins/google-slides` 等「技能和/或 MCP」打包。这些目录本批没有逐个打开 `SKILL.md`。

默认市场文件在 `.agents/plugins/marketplace.json`（指向 `plugins/`）；API key 登录用户另有 `.agents/plugins/api_marketplace.json`。本批未展开这两个 JSON 的全部条目。

## 官方文档里：Skill 和 Plugin 各是什么

据已读到的 [Build skills](https://developers.openai.com/plugins/build/skills)、[Skills 概念页](https://developers.openai.com/plugins/concepts/skills)、[Package your plugin](https://developers.openai.com/plugins/build/plugins) 和 [ChatGPT Learn: Build skills](https://learn.chatgpt.com/docs/build-skills)：

- **Skill** 是带 `SKILL.md` 的文件夹，可含 `scripts/`、`references/`、`assets/`，以及可选的 `agents/openai.yaml`（界面元数据、是否允许隐式调用、MCP 依赖等）。它建立在开放 Agent Skills 标准之上。
- **Plugin** 是 ChatGPT 与 Codex 共享的安装与分发单位，可以只含技能，也可以同时带 MCP 服务器、生命周期 hooks 和界面资源。公开插件发布到两边共用的 plugin directory。
- 分工：MCP 负责实时数据、鉴权、受控动作；Skill 负责步骤、决策点、输出要求、例子和模板。没有 MCP 时，技能也可以只靠说明和打包资源工作。
- 调用方式（Learn 文档）：ChatGPT 用 `@` 选择技能；Codex CLI / IDE 用 `/skills` 或 `$` 提及。也可以按 `description` 隐式匹配。
- Codex 本地加载位置包括：从当前工作目录向上到仓库根的 `.agents/skills`、用户级 `$HOME/.agents/skills`、管理员级 `/etc/codex/skills`，以及随 Codex 捆绑的系统技能（文档写明默认包含 `skill-creator` 和 `skill-installer`）。
- 创建：ChatGPT Work 用 `@skill-creator`，Codex 用 `$skill-creator`。也可以手写文件夹。文档建议每个技能只对一个可识别的用户目标，触发、输入或成功标准不同就拆开。

文档中的官方示例（不是本批实测）包括用 `@skill-creator` 创建名为 `tabletop-dice` 的技能，按 `3d6` 这类记号掷骰并汇总；以及 Learn 页展示的若干已装技能名称（如 Skill Creator、Skill Installer、OpenAI Docs 等）。这些是文档截图/列表里的例子，本批没有在 ChatGPT 或 Codex 账号里逐项点开验证。

## 本批实际读过的第一方 / 官方仓库内技能

### 1. 插件 `openai-developers`（第一方）

- 路径：[plugins/openai-developers](https://github.com/openai/plugins/tree/main/plugins/openai-developers)
- `plugin.json` 声明：`name: openai-developers`，`version: 1.2.3`，`author.name: OpenAI`，`license: Proprietary`，`skills: "./skills/"`，并配置了 MCP 与 app。描述是用 OpenAI API、Agents SDK 和 ChatGPT Apps 开发，并在 Codex 里创建和保存 API 密钥。
- 插件 README 列出的技能目录：`openai-platform-api-key`、`openai-api-troubleshooting`、`agents-sdk`、`build-chatgpt-app`、`chatgpt-app-submission`。本批打开了前三个的 `SKILL.md`。

**`openai-platform-api-key`**（约 143 行）：description 要求在搭建、运行、调试 OpenAI 应用或设置 `OPENAI_API_KEY` 时使用；明文密钥不得暴露；在开始 API 工作前先安全检查并询问是复用还是新建。正文有 Safety Rules、强制的第一步和凭据决策说明。这是典型的「先把危险动作挡住」的官方技能，不是普通提示词。

**`openai-api-troubleshooting`**（约 49 行）：在 API 请求失败时分类原因（网络、凭证、额度、速率限制、模型或组织权限等），并把密钥发放交给上一技能、把查文档交给 `openai-docs`。短小、边界清楚。

**`agents-sdk`**（约 174 行）：用于创建、运行、评估和部署 OpenAI Agents SDK 应用。正文含 Intake、Build / Eval / Deploy 工作流和完成标准。

这些技能会涉及 OpenAI 平台登录或 API 密钥，属于「需要 API Key / 可能产生 API 费用」的工作流。价格未核。

### 2. 插件 `plugin-eval`（仓库内官方工程工具，许可未在根目录写明）

- 路径：[plugins/plugin-eval](https://github.com/openai/plugins/tree/main/plugins/plugin-eval)
- README 说明它既是本地 Node.js CLI（要求 Node.js >= 20），也是 Codex 插件，用来评估本地技能或插件。当前 `package.json` 标为 `"private": true`，预期从本地检出运行，而不是从公共 npm 安装。
- 本批打开了 [skills/evaluate-skill/SKILL.md](https://github.com/openai/plugins/blob/main/plugins/plugin-eval/skills/evaluate-skill/SKILL.md)（约 54 行）。description 面向「评估 / 审计这个技能、为什么是这个分数、先修什么」。同一插件下还有 `evaluate-plugin`、`improve-skill`、`metric-pack-designer`、`plugin-eval` 等目录，未全部打开。

### 3. 插件 `data-analytics`（示例工作流合集，作者与许可本批未从 plugin.json 核对）

- 路径：[plugins/data-analytics](https://github.com/openai/plugins/tree/main/plugins/data-analytics)
- README 给出可直接套用的提问例子，例如 “Diagnose why weekly active users dropped last week”，并映射到具体技能名。本批打开了 `analyze-data-quality/SKILL.md`（约 162 行）：评估结构化数据或分析结论是否足够可信，再给出严重级别和输出标准。
- README 还列出可选集成（BigQuery、Snowflake、Mixpanel、Gmail 等）。这些是「若已连接则可使用」，本批未验证任何连接，也不把它们算进已测试功能。
- **未核对该插件的 `plugin.json` 作者与许可证**，因此不把它写成「确认的 OpenAI 第一方产品」，只作为官方示例仓库里已读过一份 SKILL.md 的工作流包。

## 安装、平台、门槛、费用

- **类别**：现行来源是「官方策划的插件示例仓库 + 官方文档」；旧 `openai/skills` 是已宣布弃用的技能目录。
- **平台**（据已读文档）：ChatGPT（网页、桌面、移动的 Chat 与 Work，视技能是独立文件夹还是打进插件而有所不同）、Codex（ChatGPT 桌面应用中的 Codex、Codex CLI、IDE 扩展）。独立技能文件夹主要用于桌面应用、Codex CLI 和 IDE 扩展；打进插件后也可用于 Chat / Work。本批未实测。
- **是否需要编程**：按文档用 `$skill-creator` 或在界面里安装插件，属于产品内配置。从仓库本地跑 `plugin-eval` CLI 需要 Node.js 和终端。
- **是否需要自建服务器**：一般不需要。带 MCP 的插件会连接外部服务，那是服务方的服务器，不是你为技能另搭一台。
- **API Key**：开发类技能（尤其 `openai-platform-api-key`、`agents-sdk`）会用到 OpenAI API。ChatGPT / Codex 产品本身的登录与订阅是另一件事。价格未核。
- **Windows**：文档给出的是跨平台产品路径；本批未在 Windows 实测 Codex CLI。
- **技能门槛**：阅读文档和安装插件：会使用 ChatGPT 或 Codex 界面即可。编写并评估技能：要会改 `SKILL.md`，评测 CLI 还要会运行 Node.js 命令。

## 优点和局限

优点：官方已明确指出继任仓库；插件形态把「分发、安装、可选 MCP」说清楚；第一方 `openai-developers` 把密钥安全写成硬规则；`plugin-eval` 提供可复用的评估入口。

局限：`openai/skills` 已弃用但未归档，旧文档与新公告并存，容易装错来源；`openai/plugins` 是策划示例集，不全是第一方，根目录又无统一开源许可证，`openai-developers` 明确为 Proprietary；developers.openai.com 在本环境 curl 复查 403；本批只深读了少数 `SKILL.md`。

## 元数据

- 更新时间：2026-11-25（Asia/Shanghai）
- 来源：
  - [openai/skills README](https://github.com/openai/skills) 及[弃用提交 778b0e6](https://github.com/openai/skills/commit/778b0e6129cf18cbaee3bf11479f583fadae8d03)
  - [openai/plugins README](https://github.com/openai/plugins)
  - 已打开：`plugins/openai-developers/.codex-plugin/plugin.json` 与其 README，以及 `openai-platform-api-key`、`openai-api-troubleshooting`、`agents-sdk`、`plugin-eval/skills/evaluate-skill`、`data-analytics/skills/analyze-data-quality` 的 `SKILL.md`
  - 官方文档（抓取时已读，curl 复查 403）：[Build skills](https://developers.openai.com/plugins/build/skills)、[Skills 概念](https://developers.openai.com/plugins/concepts/skills)、[Package your plugin](https://developers.openai.com/plugins/build/plugins)、[ChatGPT Learn: Build skills](https://learn.chatgpt.com/docs/build-skills)
  - GitHub API（两仓库，2026-11-25）
- 信息可信度：部分核对。仓库状态、弃用声明、已打开的源码和 plugin.json 已核对；OpenAI 文档站 curl 复查失败；未在 ChatGPT / Codex 里实际安装或调用；`data-analytics` 等非已读 plugin.json 的目录，作者与许可证待核实。
- 平台：官方文档中的 ChatGPT 与 Codex（见上文）。本批未做跨客户端实测。
- 技能门槛：使用现成插件需会操作 ChatGPT 或 Codex；编写和评估技能需会编辑 Markdown，必要时会运行 Node.js。
- 费用：`openai-developers` 在清单中声明 Proprietary；产品与 API 价格未知。不要把 GitHub 上能浏览源码理解成可免费商用再分发。
