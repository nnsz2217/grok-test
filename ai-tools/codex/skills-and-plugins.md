# 技能与插件

适用产品：OpenAI Codex，以及与 ChatGPT 共用的插件目录。当同一套步骤你已经反复说明多次，就应写成技能或安装现成插件，而不是继续加长提示词。以下为官方说明，状态为 Officially Documented。本轮没有安装技能或插件，不能当作已经实测成功。

## 1. 把已经跑通的重复流程做成一个技能

**用途：** 让“按这份清单整理日志”“按课程要求写提交说明”等任务在以后被自动或显式调用，并保持步骤一致。

**操作方法：**

1. 技能是一个目录，至少包含 `SKILL.md`，其中必须有 `name` 和 `description`；可选地放脚本、参考文档和模板。它遵循开放的 Agent Skills 标准。
2. 官方建议每个技能只做一件事，先覆盖两三个真实用例，写清输入和输出，并在描述里写上用户会真正说出的触发语。描述会被用于隐式匹配，应把关键用途写在前面。
3. 在 Codex 中可用 `$skill-creator` 对话生成；也可以手动新建文件夹。ChatGPT Work 中则使用 `@skill-creator`。若流程更适合演示而不是口述，官方提供 Record & Replay，由录制结果起草技能。
4. 显式调用：在 CLI 或 IDE 中用 `/skills` 或 `$` 提及技能。隐式调用：当任务与描述匹配时，Codex 可以自行选用。可用 `agents/openai.yaml` 把 `allow_implicit_invocation` 设为 `false`，改为只接受显式调用。
5. Codex 会从仓库、用户、管理员和系统位置加载本地技能，例如当前目录到仓库根目录沿途的 `.agents/skills`，以及 `~/.agents/skills`。同名技能不会合并，可能同时出现在选择器中。系统自带 `skill-creator` 和 `skill-installer`。
6. 可用 `$skill-installer` 安装策划技能，例如 `$skill-installer linear`。若要分发给别人或搭配连接器，官方建议打包为插件，而不是只留在本地文件夹。
7. ChatGPT 桌面应用、Codex CLI 和 IDE 扩展可以使用独立技能；打包进插件的技能也可在网页、桌面和手机的 Chat 与 Work 中使用。

**可复制的 SKILL.md 骨架（官方结构，内容需换成你的任务）：**

```markdown
---
name: lab-report-checklist
description: 在学生提交课程实验报告前，按固定清单检查结构是否完整。在用户说“检查实验报告”“交之前看一下”或附上报告草稿时使用。不要用来代写报告正文。
---

当用户提供实验报告草稿时：
1. 只检查是否包含：目的、材料、步骤、数据、误差来源、结论。
2. 列出缺失或过短的部分，不要擅自补写实验数据。
3. 用简体中文输出一份可勾选的修改清单。
```

**适用场景：** 每次提交前都要跑同一组检查；反复把测试失败日志整理成一段话；课程规定了一种固定的提交说明格式。

**限制：**

- 官方写明：初始技能列表默认最多占用模型上下文的 2%，或在上下文大小未知时最多 8,000 字符；技能很多时会先缩短描述，必要时省略部分技能并给出警告。可用 `skills.max_context_tokens` 调整，最高 10,000 tokens。这只限制初始列表；一旦选中某个技能，仍会读取完整 `SKILL.md`。
- 改完技能后，若未自动出现，需重启 Codex。
- 可用 `~/.codex/config.toml` 中的 `[[skills.config]]` 禁用某个技能而不删除文件。
- 本轮未创建技能，属 Unverified。带脚本的技能会执行代码，只应在你理解内容时使用。

**来源与可信度：** Officially Documented。[Build skills](https://learn.chatgpt.com/docs/build-skills)、[Best practices](https://learn.chatgpt.com/guides/best-practices)。查询日期 2026-11-25。

## 2. 用插件连接已有工具，但只安装你真的会用到的

**用途：** 当需要的信息或操作在仓库之外（例如 GitHub、日历、文档）时，用插件或 MCP 连接，而不是反复复制粘贴。

**操作方法：**

1. ChatGPT 与 Codex 共用公开插件目录。在桌面应用、网页或 CLI 的插件界面中浏览并安装。CLI 文档展示了从市场浏览、查看已安装插件的界面，并提到可用 `/apps` 在 Codex 中使用 ChatGPT 应用。
2. 在受支持的 Codex 任务视图中，可通过 Sources → Use plugins 选择已安装插件。
3. 需要自定义连接时，可用 `codex mcp add` 添加 MCP 服务器，或在桌面应用的 Settings > MCP servers 中查看推荐与自定义服务器。官方建议先加一两个能去掉你现有重复劳动的工具，不要一开始接上所有服务。
4. 连接 Gmail 或 Google Drive 等插件 **需要谷歌帐户**。没有谷歌帐户时，跳过这些插件，改用 GitHub 或其他不依赖 Google 的工具，或只使用不含 Google 连接的技能。

**适用场景：** 需要根据 GitHub 上的讨论修改代码；或希望在 Codex 里使用已安装的文档类插件。

**限制：** 插件能否出现，取决于方案、工作区、角色和地区。部分插件仅限桌面或仅限 Codex。Personal Skills 在 ChatGPT 一侧主要面向商务和教育等方案，见 ChatGPT 的插件笔记，不要假定个人帐户在所有界面都有同样的创建权限。授权后，相关输入可能发给第三方。本轮未浏览插件市场实况，属 Unverified。

**来源与可信度：** Officially Documented。[Build skills](https://learn.chatgpt.com/docs/build-skills)、[Plugins in ChatGPT](https://help.openai.com/en/articles/20001256-plugins-in-chatgpt)、[Codex CLI](https://learn.chatgpt.com/docs/codex/cli)、[Best practices](https://learn.chatgpt.com/guides/best-practices)。查询日期 2026-11-25。

## 元数据

- 更新时间：2026-11-25（Asia/Shanghai）
- 来源：上文各官方文档链接
- 信息可信度：部分核对。技能格式、加载位置、插件目录和 MCP 入口为 Officially Documented。本轮未创建或安装技能/插件，属 Unverified。未核对手表价
- 平台：独立技能可用于桌面应用、CLI 和 IDE；插件技能还可用于网页和手机上的 Chat / Work。Windows 可用桌面应用或 CLI。未实测
- 技能门槛：会新建一个文件夹并编辑 Markdown。这已经比“只在聊天框里提问”多一步，但仍不必先会写程序。带脚本的技能和自定义 MCP 需要更多技术判断，本篇不作为入门必做
- 费用：免费 / 付费 / API 计费。插件可用性因方案而异；未核对手表价，故不写入金额
