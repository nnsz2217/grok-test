# Google 官方 Agent Skills（google/skills）

这是 Google 面向自家产品和 Google Cloud 的官方技能仓库，不是提示词合集，也不是 MCP 服务器目录。仓库同时附带「技能 + MCP」形式的插件安装说明。安装官方推荐命令依赖 `npx skills`（[vercel-labs/skills](https://github.com/vercel-labs/skills) 提供的 CLI，本身不是 Google 的技能包，见本目录安装工具说明）。

## 基本信息

- **名称**：Agent Skills（Google products and technologies）
- **GitHub**：[github.com/google/skills](https://github.com/google/skills)
- **官方介绍**：
  - 发布公告：[Level Up Your Agents: Announcing Google's Official Skills Repository](https://cloud.google.com/blog/topics/developers-practitioners/level-up-your-agents-announcing-googles-official-skills-repository)（2026-04-22，Megan O'Keefe）。当时写的是仓库起步有 13 个技能，安装命令示例是 `npx skills install github.com/google/skills`。**当前 README 使用的命令是 `npx skills add google/skills`**，请以仓库 README 为准。
  - 工程实践：[Behind the scenes, two months later: How we ship Google Agent Skills like products](https://cloud.google.com/blog/topics/developers-practitioners/behind-the-scenes-two-months-later-how-we-ship-google-agent-skills-like-products)（2026-10-28，Remigiusz Samborski）。文中写到仓库当时已超过 21,000 stars、托管 170 多个技能。这是文章发表时的数字，不是今天的查询结果。
- **作者 / 团队**：Google（README 写明欢迎报错和提新技能建议）
- **开源许可证**：Apache-2.0（仓库 `LICENSE`，GitHub API SPDX 亦为 Apache-2.0）
- **最近推送**：`2026-11-25T04:48:57Z`（换算为 2026-11-25 12:48，Asia/Shanghai）。未归档。
- **热度快照**：2026-11-25（Asia/Shanghai）查询时 24,636 stars、2,050 forks。
- **技能数量**：本批下载并解析了仓库根目录的 [index.json](https://raw.githubusercontent.com/google/skills/main/index.json)（文件自身注明 generated，不要手改）。其中 `skills` 数组长度为 **219**。这与 2026-10-28 博文中的「170 多个」并不矛盾，说明此后仍在增加；也不要把博文旧数字当成今天的库存。

顶层真实结构包括：`LICENSE`、`README.md`、`index.json`、`skills/`、`plugins/`、`.agents/`、`.claude-plugin/`、`.github/` 等。`skills/` 下分类目录为：`ads`、`analytics`、`cloud`、`developers`、`identity`、`platform-devices`。

## 它能完成什么，和普通聊天有什么区别

这批技能主要把「如何正确使用某项 Google 产品或云配方」写成智能体可按需加载的说明，减少靠模型记忆过时 API、或把整本文档一次性塞进上下文的问题。发布公告把 Skill 称作「精炼的、面向智能体的文档」，并对比了文档 MCP：MCP 实时但容易造成 context bloat，Skill 按需加载。

覆盖面从 README 分类可见，包括：Google Cloud 入门与认证、多产品方案、AI/ML 与 Agent Platform、基础设施、数据库与分析、应用开发、Well-Architected 各支柱、安全与身份，以及 Google Analytics 等。本批没有把 219 个技能逐一打开，下面只详写读过 `SKILL.md` 的代表。

## 安装与更新（官方 README，本批未实际执行）

需要本机已有 Node.js（从而有 `npx`）：

```bash
npx skills add google/skills
```

按提示选择要装的技能、目标智能体，以及项目级或全局范围。更新：

```bash
npx skills update
```

更新时可选删除已经过时的技能。

仓库还给出了插件安装方式（技能 + MCP）：

| 客户端 | 官方 README 中的命令 |
| --- | --- |
| Claude Code | `claude plugin marketplace add google/skills`，再 `claude plugin install @google-plugins` |
| Codex | `codex plugin marketplace add google/skills`，再从 `/plugins` 浏览器安装 |
| Antigravity CLI | `agy plugin install https://github.com/google/skills/` |

README 把目标智能体写作可配置项；发布公告提到包括 Antigravity、Gemini CLI 以及第三方智能体。本批未在这些客户端上实测。

Windows：安装入口同样是 `npx`（需先装 Node.js）。`finding-google-skills` 的正文里甚至写了用 PowerShell 过滤目录的例子。本批未在 Windows 上跑安装向导。

### Gemini CLI 如何发现技能

Google 的 [Creating Agent Skills | Gemini CLI](https://geminicli.com/docs/cli/creating-skills/)（页面显示 Last updated: Apr 30, 2026）说明：技能放在 `.gemini/skills/` 或兼容别名 `.agents/skills/`（用户级则是 `~/.gemini/skills/` 或 `~/.agents/skills/`）。可用内置 `skill-creator` 生成技能，或 `gemini skills install` / `link` / `uninstall` 管理。文档明确写了 Windows PowerShell 的建目录命令。这是客户端用法，不是另一份技能目录。

## 是否需要 API Key、付费、自己的服务器

- 技能文件本身按 Apache-2.0 复制使用，不需要为「下载技能」付费。
- 多数技能会指导智能体调用 `gcloud`、客户端库或 Google API。这意味着通常需要 Google 账号、项目，以及相应 API 的启用。只做只读咨询和做会改云资源的操作，成本完全不同。
- `google-cloud-recipe-onboarding` 的流程包含账号、项目和**账单绑定**校验；`gemini-api` 的 `compatibility` 字段写明需要有效的 Google Cloud 凭证、已启用结算，以及启用 Gemini platform API（`aiplatform.googleapis.com`）。云侧费用以 Google Cloud 报价为准，本批不编造价格。
- 不需要为这些技能单独搭一台「技能服务器」；但要执行其中的云操作，你得有可登录的 Cloud 环境。
- 是否需要编程：按 README 用 `npx` 安装属于简单配置；真正完成入门或 API 调用，往往还要会在终端里运行 `gcloud`，并理解技能给出的示例代码。门槛按具体技能变化。

## 本批实际读过的代表性 SKILL.md

### 1. `finding-google-skills`（目录导航技能）

- 路径：[skills/developers/finding-google-skills/SKILL.md](https://github.com/google/skills/blob/main/skills/developers/finding-google-skills/SKILL.md)
- 目录里目前只有 `SKILL.md`（无 scripts/references）。
- frontmatter：`name: finding-google-skills`；`metadata.version: "1.1.0"`，`category: MultiProductSolutions`。
- description 的要点（据原文）：在开发者选择或搭建技术栈、而 Google 产品是合理候选项时使用——即使请求里没有点名供应商；若栈已经确定在别家且未点名 Google 产品，或任务不涉及平台选择，则跳过。任务是把匹配的 Google 技能拉进来，权衡取舍，并说明何时不该用 Google。
- 正文标题为「Google Skill Finder」，核心工作流是去取官方目录 `index.json`，并强调：**必须拿到未改动的原始字节**，不能用被截断或被总结过的目录；取回后要确认正文能解析为带 `skills` 数组的 JSON，404、HTML 错误页或证书失败都算失败。证书失败不要重试。这是一个「先找对技能再加载」的元技能，设计上非常强调防幻觉和防截断。

### 2. `google-cloud-recipe-onboarding`（新开发者入门）

- 路径：[skills/cloud/google-cloud-recipe-onboarding/SKILL.md](https://github.com/google/skills/blob/main/skills/cloud/google-cloud-recipe-onboarding/SKILL.md)
- 目录含 `SKILL.md` 和 `references/`。
- `metadata.version: "1.0.1"`，`category: GettingStarted`。
- description 写明：覆盖账号创建、结算、项目管理和部署第一个资源；用于开发者初始化第一个项目。不要用于企业组织级开通，也不要用于复杂多项目架构。
- 正文按步骤组织：检查本机工具、认证、选择或创建项目、校验并关联账单、再链式调用后续技能（支出控制与工作负载），并有「Validation Logic」。这是「可复用工作流 + 明确不要用的边界」的典型官方写法。

### 3. `gemini-api`

- 路径：[skills/cloud/gemini-api/SKILL.md](https://github.com/google/skills/blob/main/skills/cloud/gemini-api/SKILL.md)（约 112 行）
- `metadata.version: "1.0.4"`，`category: AiAndMachineLearning`。
- description 写清适用：在 Gemini platform（文档注明其前身包括 Gemini Enterprise Agent Platform 和 Vertex AI）上用统一 Google Gen AI SDK 做生成、JSON、函数调用、Search grounding 等。同时用「Don't use」把边界划给兄弟技能，例如 stateful agent sessions 应走 `gemini-interactions-api`，Managed Agent CRUD 应走 `gemini-agents-api`，Live API 排障走 `gemini-live-api`。
- `compatibility` 声明了凭证、结算和 API 启用要求。正文还包含 Usage Attribution、认证与 Python 快速开始，以及把细节指到其他参考的「Reference Routing」。

### 4. `google-analytics-data-api-basics`

- 路径：[skills/analytics/google-analytics-data-api-basics/SKILL.md](https://github.com/google/skills/blob/main/skills/analytics/google-analytics-data-api-basics/SKILL.md)（约 260 行）
- 官方产品文档也有对应页：[Google Analytics AI agent skills](https://developers.google.com/analytics/devguides/agent-skills)。
- description 写明用于报表和 Data API（v1beta），并明确不要用于 Admin API（创建媒体资源、管用户）或前端跟踪代码安装。
- 正文从「用 `gcloud services enable analyticsdata.googleapis.com` 启用 API」和 ADC 认证开始，再给多语言客户端库和 Python 快速开始，以及常用维度 / 指标。若本机没有 `gcloud`，技能要求先提示用户安装，而不是假装已经可用。

## 官方工程方法（对写技能有用，不是安装步骤）

2026-10-28 博文把技能当作产品发布：每次行为变更要有语义化版本；用确定性检查（结构、lint、链接）做门禁；每项变更带评估报告，对比上一版本，新技能则对比「没有该技能的智能体」。合并前还要过 AI 审查和领域专家批准。文中建议先跑便宜的确定性检查，再跑昂贵的 LLM 评估。这些是 Google 内部仓库的发布门禁描述；公开 GitHub 镜像是否运行完全同一套流水线，本批没有从 `.github/` 工作流文件逐项核对。

## README 列出的其他官方 Google 技能仓库（本批只核元数据，未深读 SKILL.md）

这些是 `google/skills` README「Additional Google skills」列出的独立仓库。本批用 GitHub API 核对了存在性、许可证和最近推送，**没有**再打开其中的 `SKILL.md`，因此只作为索引，不当作已完成的技能评测。

| 仓库 | 2026-11-25 核到的状态 |
| --- | --- |
| [android/skills](https://github.com/android/skills) | 未归档；Apache-2.0；最近推送 `2026-11-23T13:39:36Z`（2026-11-23 21:39，Asia/Shanghai）；10,751 stars |
| [dart-lang/skills](https://github.com/dart-lang/skills) | 未归档；BSD-3-Clause；最近推送 `2026-11-16T22:26:36Z`（2026-11-17 06:26，Asia/Shanghai）；561 stars |
| [flutter/skills](https://github.com/flutter/skills) | 该 URL 会重定向到 [flutter/agent-plugins](https://github.com/flutter/agent-plugins)。后者未归档；BSD-3-Clause；最近推送 `2026-11-19T00:23:23Z`（2026-11-19 08:23，Asia/Shanghai）；3,210 stars |
| [googlemaps/agent-skills](https://github.com/googlemaps/agent-skills) | 未归档；Apache-2.0；最近推送 `2026-11-19T15:06:28Z`（2026-11-19 23:06，Asia/Shanghai）；76 stars |
| [firebase/agent-skills](https://github.com/firebase/agent-skills) | 未归档；Apache-2.0；最近推送 `2026-11-09T18:52:44Z`（2026-11-10 02:52，Asia/Shanghai）；530 stars |
| [google/agents-cli](https://github.com/google/agents-cli) | README 称为 Agent Development Kit (ADK) Skills。未归档；Apache-2.0；最近推送 `2026-11-24T18:35:07Z`（2026-11-25 02:35，Asia/Shanghai）；6,401 stars |
| README 还列出 [Advanced Google Cloud Storage Skills](https://github.com/gemini-cli-extensions/google-cloud-storage) | 该 API 路径会转到 [GoogleCloudPlatform/google-cloud-storage-plugin](https://github.com/GoogleCloudPlatform/google-cloud-storage-plugin)。未归档；Apache-2.0；最近推送 `2026-11-23T21:59:50Z`（2026-11-24 05:59，Asia/Shanghai）；36 stars。本批未读其技能正文。 |

## 优点和局限

优点：仍在频繁更新；数量和分类清楚；`index.json` 可被 `finding-google-skills` 程序化检索；已读样本在 description 里认真写了「不要用于什么」；入门技能把账单和认证当成显式步骤，而不是假定环境已就绪；许可证明确。

局限：大多数技能面向 Google Cloud / Google 产品开发，对不做这些工作的人实用价值有限；执行技能可能产生云费用；219 个技能本批只深读了 4 个；安装依赖第三方 `npx skills` CLI（需 Node.js）。发布公告里的旧安装命令与当前 README 不一致，应以 README 为准。

## 元数据

- 更新时间：2026-11-25（Asia/Shanghai）
- 来源：
  - [google/skills README](https://github.com/google/skills)
  - [index.json](https://raw.githubusercontent.com/google/skills/main/index.json)（2026-11-25 下载，数组长度 219）
  - 已打开：`finding-google-skills`、`google-cloud-recipe-onboarding`、`gemini-api`、`google-analytics-data-api-basics` 的 `SKILL.md`
  - [2026-04-22 发布公告](https://cloud.google.com/blog/topics/developers-practitioners/level-up-your-agents-announcing-googles-official-skills-repository)、[2026-10-28 工程博文](https://cloud.google.com/blog/topics/developers-practitioners/behind-the-scenes-two-months-later-how-we-ship-google-agent-skills-like-products)
  - [Gemini CLI Creating Agent Skills](https://geminicli.com/docs/cli/creating-skills/)
  - [Google Analytics AI agent skills](https://developers.google.com/analytics/devguides/agent-skills)
  - GitHub API（主仓库及上表附加仓库，2026-11-25）
- 信息可信度：部分核对。主仓库元数据、README 安装命令、index.json 数量和 4 份 SKILL.md 已核对；未实际运行 `npx skills add`；未读完全部 219 个技能；附加仓库只核 API 元数据；Google 内部 CI 门禁以博文描述为准，未逐项对照公开工作流文件。
- 平台：官方文档或 README 提到的包括可通过 `npx skills` 配置的多种智能体，以及 Claude Code、Codex、Antigravity CLI、Gemini CLI。本批未做兼容性实测。
- 技能门槛：安装需要会用终端和 Node.js / `npx`；使用云技能通常还要会登录 Google Cloud 并理解基本的项目与账单概念。
- 费用：技能源码为 Apache-2.0（免费使用许可）。运行技能所触发的 Google Cloud / API 费用未知，以 Google 报价和项目账单为准。
