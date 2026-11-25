# 第一批推荐：官方 Skills 与 Skill Engineering

本页只对 **2026-11-25（Asia/Shanghai）第一批已核实** 的官方规范、官方仓库和官方文档材料分级。它不是开源技能总榜，也不对未打开 `SKILL.md` 的单个第三方插件打「可安装」高分。

评分维度：实用价值、功能完整性、设计质量、维护活跃度、文档质量、兼容性、安全性、使用成本。等级含义：

- **A**：优先使用或优先读完；若是可安装对象，值得在对应产品里优先装。
- **B**：质量较好，适合特定场景。
- **C**：有特色，值得了解，不必急着装。
- **D**：仅供研究，不建议作为当前安装来源或日常依赖。

本批没有在产品里实际跑通这些技能。等级依据官方文档和已读源码，不是使用测试分数。费用只在已核对的范围内写，价格数字一律不编造。

## A. 优先阅读或优先安装

### Agent Skills 开放规范 — A（必读，不是安装包）

- 笔记：[official-skills/agent-skills-specification.md](official-skills/agent-skills-specification.md)
- 为什么放在 A：后面几乎所有官方仓库都按这套格式写。不先读规范，很容易把产品扩展字段当成标准，或把 MCP、提示词和 Skill 混在一起。
- 简评：设计质量与文档质量高；维护仍在进行（最近推送 2026-11-05 03:47，Asia/Shanghai）。局限是规范尚未版本化，`allowed-tools` 仍是实验性字段。
- 使用成本：阅读免费。
- 技能门槛：能读英文文档、会改 Markdown。

### `skill-creator`（anthropics/skills）— A（若你打算自己写技能）

- 笔记：[official-skills/anthropics-skills.md](official-skills/anthropics-skills.md)
- 为什么放在 A：这是本批读到的、最完整地把「起草 → 对照评测 → 改写 → 优化触发」写进一份技能的官方材料，也是开放规范写作指南多次提到的配套技能。
- 简评：设计质量高，目录里有评测脚本和参考文件；许可抽查为 Apache-2.0。实用前提是你使用 Claude / Claude Code，或至少愿意按其流程改写到别的客户端。
- 使用成本：技能源码按 Apache-2.0；在 Claude 产品中运行需该产品账号或付费方案，价格未知。
- 注意：仓库 Disclaimer 声明这些技能以演示和教学为主，用于关键任务前要自己测试。

### 文档技能 `pdf` / `docx` / `xlsx` / `pptx`（anthropics/skills 的 document-skills）— A（若你用 Claude 处理办公文档）

- 笔记：同上，已打开 `pdf` 全文结构及另外三份主文件开头。
- 为什么放在 A：这是 Anthropic README 明确称为「驱动 Claude 文档能力、并作为生产级复杂技能参考」的一组，而且 `pdf` 的拆分（`REFERENCE.md`、`FORMS.md`、`scripts/`）本身就是教材。
- 简评：功能完整性在已读范围内高；安装路径在 Claude Code 插件市场有官方命令。局限仍是仓库级 Disclaimer，以及需要相应 Python 库或命令行工具。
- 官方示例（来自 README，非本批实测）：安装后可要求 “Use the PDF skill to extract the form fields from path/to/some-file.pdf”。

### Cursor 内置技能（已在产品中，不必另找安装源）— A（若你已经使用 Cursor）

- 笔记：[official-skills/cursor-official-skills.md](official-skills/cursor-official-skills.md)
- 为什么放在 A：对 Cursor 用户来说，`/create-skill`、`/review`、`/migrate-to-skills` 等已经在编辑器里，优先知道它们的名字和用途，比再装一套外部合集更划算。
- 简评：文档清楚，Windows 快捷键有官方说明。局限是本批没有读到内置技能的 `SKILL.md` 原文，无法按源码评设计质量；故「A」指「优先使用官方已提供的入口」，不是对每条内置指令打了源码分。

## B. 特定场景值得安装或深入使用

### google/skills 整库，尤其 `finding-google-skills` 与入门配方 — B（做 Google Cloud / Google 产品开发时接近 A）

- 笔记：[official-skills/google-skills.md](official-skills/google-skills.md)
- 为什么不是对所有人的 A：219 个技能大多绑定 Google 产品与云操作，对不做这些工作的人实用价值有限，而且可能产生云费用。
- 为什么是扎实的 B：仓库仍在更新（本批查询当天仍有推送），Apache-2.0，有 `index.json` 和专门的目录导航技能；已读样本在 description 里认真划分边界。若你正在上 Google Cloud，可把本库和 `finding-google-skills` 视为优先。
- 安装（官方 README，未实测）：`npx skills add google/skills`（需要 Node.js）。
- 使用成本：技能源码免费许可；云资源与 API 按 Google 账单计费，价格未知。
- 安全：只装你需要的技能，执行前看清是否会启用 API、绑定账单或改资源。

### openai/plugins 中的第一方 `openai-developers` — B（使用 ChatGPT / Codex 做 OpenAI 开发时）

- 笔记：[official-skills/openai-plugins.md](official-skills/openai-plugins.md)
- 为什么是 B：`plugin.json` 确认作者为 OpenAI；已读的密钥与排障技能把安全规则写得很硬，适合作为官方工作流。但它是 Proprietary，且会涉及 API 密钥与潜在 API 费用，不适合当作「随便再分发的开源包」。
- 文档站在本环境 curl 复查为 403，安装步骤请以你能打开的官方插件文档为准。
- 使用成本：专有许可 + 产品 / API 计费，价格未知。

### plugin-eval（openai/plugins 内）— B（你在为 Codex / ChatGPT 写技能并需要评估工具时）

- 笔记：同上。
- 为什么是 B：它把「评估这个技能、先修什么」做成仓库内的官方工具，对 Skill Engineering 很有用。局限：README 写明包是 private，预期从本地检出运行；根仓库无统一开源许可证，再分发需谨慎。
- 技能门槛：需 Node.js 20+ 和终端。

### npx skills（vercel-labs/skills）— B（作为安装工具，不是技能）

- 笔记：[official-skills/skills-sh-cli.md](official-skills/skills-sh-cli.md)
- 为什么是 B：安装 Google 官方技能的推荐入口，MIT，Release 到 v1.9.0（2026-11-16）。它不提供推理期路由，也不应被当成官方技能内容本身。
- 安全：会把远程技能（可能含脚本）写入本地，只从信任源添加。

## C. 值得了解，不必优先安装

### anthropics/skills 中尚未深读的示例技能，以及仓库整体的「示例」定位 — C（学习设计时浏览）

- 除 document-skills 与 `skill-creator` 外，仓库还有创作、品牌、测试网页等示例。本批没有打开它们的 `SKILL.md`，因此不升级为 A/B 安装推荐。仓库自己也强调演示和教学用途。
- `mcp-builder` 已打开，它是「教你写 MCP 服务器」的技能，适合在真正要开发 MCP 时查阅，日常使用不必预装。评为 C 到「特定开发场景的 B」之间；因受众窄，本表放在 C。

### Claude Code 内置 bundled skills（`/doctor`、`/code-review` 等）— C（对 Claude Code 用户是「先知道有」）

- 已在产品中，文档有列表。本批未读源码，故不按 A 的源码标准推荐；用 Claude Code 时直接在文档和 `/` 菜单里查看即可。

### Gemini CLI 的技能机制与内置 skill-creator — C（对 Gemini CLI 用户）

- 记在 Google 笔记中。它是客户端能力，本批没有单独评一份 Gemini 官方技能包（官方目录仍以 `google/skills` 为主）。

### openai/plugins 里未核作者与许可的示例插件（如 data-analytics 等）— C

- 仓库是官方策划的示例集，不等于每一个插件都是 OpenAI 第一方，也不等于都可以按开源许可再分发。本批只打开了 `analyze-data-quality` 一份正文，作为工作流写法参考是有价值的，但不推荐在未读许可和作者字段前整包安装。

### Google README 列出的其他官方仓库（Android、Dart、Flutter/agent-plugins、Firebase、Maps、agents-cli 等）— C

- 仅核到仓库仍在维护和许可证，未读 `SKILL.md`。做对应平台开发时可以列入后续深挖，不在本批推荐预装。

## D. 仅供研究，不建议作为当前安装来源

### openai/skills（已弃用的旧目录）— D

- 笔记：[official-skills/openai-plugins.md](official-skills/openai-plugins.md)
- 官方 README 已声明 deprecated，弃用提交时间为 2026-06-22（UTC）。仓库尚未归档，star 仍然很高，部分使用文档仍提到 `$skill-installer` 和旧路径，这正是容易装错的原因。
- 新的技能与插件示例应以 [openai/plugins](https://github.com/openai/plugins) 和现行 Plugins 文档为准。若研究历史目录，可以阅读，但不要把它当作现行官方技能包来依赖。

## 本批不评分、避免误判的对象

- Microsoft SkillOpt、obra/superpowers：非官方平台技能包，见 [skill-engineering/guide.md](skill-engineering/guide.md) 附录。不在本页打安装等级。
- Agent Skills Client Showcase 的完整产品名单：该页在本环境未能核出列表。
- 任何本批没有打开 `SKILL.md` 的单个技能的「功能完整性」细项。

## 元数据

- 更新时间：2026-11-25（Asia/Shanghai）
- 来源：本批 [official-skills/](official-skills/) 与 [skill-engineering/guide.md](skill-engineering/guide.md) 各文已列的原始链接；分级是本库根据那些已核事实做的判断，不是某一家官方榜单。
- 信息可信度：部分核对。分级所依据的仓库状态、许可证抽查和已读源码已核对；未进行实际安装与效果测试；未打开的技能不提升等级。
- 平台：见各被推荐条目自己的笔记。
- 技能门槛：见各条目；总体上海从「会用对应产品的聊天或终端」到「会改 Markdown / 运行 Node.js」不等。
- 费用：各条目已区分源码许可与产品 / 云 / API 费用；具体价格未知。
