# 高级使用技巧索引

本页检索 `ai-tools/` 里已经写入的高级技巧。第一批只填 ChatGPT、Grok 和 Codex；DeepSeek、Claude 技巧正文、Gemini、其他工具、跨平台技巧和高级工作流仍是占位，没有可引用的结论。

查询日期为 2026-11-25（Asia/Shanghai）。本批对照官方文档、产品页和官方新闻稿整理，没有登录产品实操。功能状态只用 Officially Documented、Community Reported 或 Unverified，不标 Verified，也不声称已经实测成功。价格未经核对，各篇都不写入金额。需要谷歌帐户的步骤已在对应条目标明。

产品入口、地区限制和 2026-11-25 的访问记录仍以各工具总览为准，本页不重复改写那些记录。

## 怎样使用本索引

1. 先看对应产品的总览，确认入口和限制，尤其是地区和方案差异。
2. 再按下面的主题打开技巧笔记。每条都包含用途、步骤或示例、限制和来源。
3. 社区经验会单独标明。官方尚未写出逐步手册的部分，会标明文档缺口，而不是编造点击路径。

## ChatGPT

总览：[ChatGPT.md](./ChatGPT.md)。技巧目录：[chatgpt/](./chatgpt/)。

| 技巧 | 可信度 | 笔记 |
| --- | --- | --- |
| 给一门课建项目并写项目说明 | Officially Documented | [项目、说明与记忆边界](./chatgpt/projects-context-and-instructions.md) |
| 项目说明覆盖全局自定义指令 | Officially Documented | 同上 |
| 默认记忆或仅项目记忆 | Officially Documented | 同上 |
| 把有用回复存成项目资料 | Officially Documented；定期整理总述为 Community Reported | 同上 |
| 项目中学习模式、定时任务和 GPT 首条消息的边界 | Officially Documented | 同上 |
| 查看和修正记忆 | Officially Documented | [记忆与临时对话](./chatgpt/memory-and-temporary-chat.md) |
| 临时对话开始前选择是否个性化 | Officially Documented | 同上 |
| 深度研究：先改计划，并可限定网站 | Officially Documented | [深度研究](./chatgpt/deep-research.md) |
| 学习模式：在普通对话里开启并先说明程度 | Officially Documented | [学习模式](./chatgpt/study-mode.md) |
| 把文件直接附到对话并指明页码；项目/GPT 知识库可能不含嵌入图 | Officially Documented | [文件、数据分析与写作块](./chatgpt/files-data-and-writing-blocks.md) |
| 表格分析前先整理成一行一条 | Officially Documented | 同上 |
| 用写作块和代码块改草稿；Canvas 已退出现行模型 | Officially Documented；现行界面是否完全无残留入口为 Unverified | 同上 |
| 音频转写须选用支持的模型和入口 | Officially Documented | 同上 |
| 分清 Chat、Work 和 Codex；代理模式已退出 | Officially Documented | [Chat、Work 与模型选择](./chatgpt/work-and-model-selection.md) |
| 按思考等级选择模型 | Officially Documented；选择器实况为 Unverified | 同上 |
| 用 Work 生成可编辑文档或幻灯片（原生 Google 文档需要谷歌帐户） | Officially Documented | 同上 |
| 自定义 GPT 计划于 2026-12-11 退役；个人帐户不能新建 GPT | Officially Documented | [插件、自定义 GPT 过渡与定时任务](./chatgpt/plugins-gpts-and-scheduled-tasks.md) |
| 用插件安装可复用技能和连接 | Officially Documented | 同上 |
| 定时任务与事件触发任务；项目内任务读不到项目文件 | Officially Documented | 同上 |

主要原始来源包括：[Projects in ChatGPT](https://help.openai.com/en/articles/10169521-projects-in-chatgpt)、[Memory in ChatGPT](https://help.openai.com/en/articles/8590148-memory-in-chatgpt)、[Deep research in ChatGPT](https://help.openai.com/en/articles/10500283-deep-research-in-chatgpt)、[Using study mode in ChatGPT](https://help.openai.com/en/articles/11780217-using-study-mode-in-chatgpt)、[Uploading files and audio to ChatGPT](https://help.openai.com/en/articles/8555545-uploading-files-and-audio-to-chatgpt)、[Working with writing blocks and code blocks in ChatGPT](https://help.openai.com/en/articles/20001246-working-with-writing-blocks-and-code-blocks-in-chatgpt)、[Model Release Notes](https://help.openai.com/en/articles/9624314-model-release-notes)、[ChatGPT Work and Codex](https://help.openai.com/en/articles/20001275-chatgpt-work-and-codex)、[GPT-6 and other models in ChatGPT](https://help.openai.com/en/articles/20001354-gpt-6-and-other-models-in-chatgpt)、[Custom GPT retirement and migration FAQ](https://help.openai.com/en/articles/20001519-custom-gpt-retirement-and-migration-faq)、[Plugins in ChatGPT](https://help.openai.com/en/articles/20001256-plugins-in-chatgpt)、[Scheduled tasks in ChatGPT](https://help.openai.com/en/articles/10291617-scheduled-tasks-in-chatgpt)。完整出处见各篇文末。

## Grok

总览：[Grok.md](./Grok.md)。技巧目录：[grok/](./grok/)。以 grok.com 与官方应用为准，不把 X 平台里的 Grok 或 Grok Bot 当作同一套操作说明。

| 技巧 | 可信度 | 笔记 |
| --- | --- | --- |
| 使用 grok.com 和 Chrome / Chromium，以免看不到 Projects | Officially Documented | [使用 grok.com 与 Projects 的文档现状](./grok/grok-com-and-projects.md) |
| 消费端 Projects 存在，但缺少完整官方操作手册 | 存在为 Officially Documented；逐步操作为 Unverified | 同上 |
| 多文件上传、按页码提问和官方格式限制 | Officially Documented；本轮未完成上传问答，效果为 Unverified | [文件上传与提问](./grok/files-and-multimodal.md) |
| 用内置 Skills 生成 Word / 幻灯片 / 表格 / PDF | Officially Documented；输出质量为 Unverified | [Skills 与办公文件](./grok/skills-and-office-outputs.md) |
| 把反复使用的流程存成自己的技能 | 概述为 Officially Documented；界面细节为 Unverified | 同上 |
| 连接器：没有谷歌帐户时改用 Outlook / OneDrive 等 | Officially Documented | [连接器与谷歌帐户限制](./grok/connectors-and-account-limits.md) |
| 按任务选择搜索、深度推理或多智能体（多智能体随 SuperGrok） | Officially Documented；按钮实况为 Unverified | [搜索、深度推理与多智能体](./grok/search-reasoning-and-multi-agent.md) |
| 不把 DeepSearch 当作现行功能名 | 现行产品页未列出该名称；旧材料可能过时 | 同上 |
| 产品页列出跨对话记忆与自定义指令 | 能力存在为 Officially Documented；操作步骤为 Unverified | [记忆、自定义指令及与 ChatGPT 的差异](./grok/memory-instructions-and-chatgpt-differences.md) |
| 与 ChatGPT 在入口、地区名单、Canvas、工作流上的差异 | Officially Documented（分项对到来源）；非实测评测 | 同上 |

主要原始来源包括：[Welcome to Grok](https://docs.x.ai/grok/overview)、[FAQ - Grok Website / Apps](https://docs.x.ai/grok/faq)、[Connectors](https://docs.x.ai/grok/connectors)、[Grok 产品页](https://x.ai/grok)、[Skills in web, iOS, and Android](https://x.ai/news/grok-skills)、[License & User Management](https://docs.x.ai/grok/management)。完整出处见各篇文末。

## Codex

总览：[Codex.md](./Codex.md)。技巧目录：[codex/](./codex/)。本轮未安装、未登录、未运行。

| 技巧 | 可信度 | 笔记 |
| --- | --- | --- |
| 按工作方式选择桌面应用、IDE、CLI 或 Cloud | Officially Documented | [选择入口并说明任务](./codex/surfaces-and-first-prompts.md) |
| 提示词写清目标、上下文、限制和完成标准 | Officially Documented | 同上 |
| Windows 原生与 WSL2 应把项目放在对应位置；WSL1 已不受支持 | Officially Documented | [Windows 上的安装与沙箱](./codex/windows-setup.md) |
| 用 AGENTS.md 分层写可复用约定 | Officially Documented | [用 AGENTS.md 写可复用约定](./codex/agents-md.md) |
| 复杂任务先用 Plan 模式 | Officially Documented | [先做计划，再改代码，并做审查](./codex/plan-review-and-approvals.md) |
| 保留沙箱和审批；旧的 untrusted 策略已退役 | Officially Documented | 同上 |
| 改完后用 /review 检查再提交 | Officially Documented | 同上 |
| 把重复流程做成技能，或安装插件（Google 类插件需要谷歌帐户） | Officially Documented | [技能与插件](./codex/skills-and-plugins.md) |

主要原始来源包括：[Quickstart](https://learn.chatgpt.com/docs/quickstart)、[Codex CLI](https://learn.chatgpt.com/docs/codex/cli)、[Codex IDE extension](https://learn.chatgpt.com/docs/codex/ide)、[Best practices](https://learn.chatgpt.com/guides/best-practices)、[Custom instructions with AGENTS.md](https://learn.chatgpt.com/docs/agent-configuration/agents-md)、[Agent approvals & security](https://learn.chatgpt.com/docs/agent-approvals-security)、[Build skills](https://learn.chatgpt.com/docs/build-skills)、[ChatGPT desktop app for Windows](https://learn.chatgpt.com/docs/windows/windows-app)、[WSL](https://learn.chatgpt.com/docs/windows/wsl)、[ChatGPT Work and Codex](https://help.openai.com/en/articles/20001275-chatgpt-work-and-codex)。完整出处见各篇文末。

## 第一批未写入正文的分类

这些目录目前只有简短说明，提醒后续再写，不能当成已经研究过的技巧清单：

- [deepseek/](./deepseek/)
- [claude/](./claude/)（Claude 总览已有，技巧正文待补）
- [gemini/](./gemini/)
- [other-tools/](./other-tools/)
- [cross-platform-tips/](./cross-platform-tips/)
- [advanced-workflows/](./advanced-workflows/)

## 本批刻意未当成现行功能收录的内容

- **ChatGPT Canvas：** 官方在 2026-05-28 写明不再用于 GPT-5.5 Instant / Thinking，改由写作块和代码块提供；2026-10-14 又宣布从 ChatGPT 退役 GPT-5.5。本批把它记为已退出的功能，而不是现行技巧。
- **ChatGPT agent mode：** 官方帮助写明已不再提供，应改用 ChatGPT Work。
- **把“现在去新建一个自定义 GPT”当作个人用户的现行步骤：** 官方写明个人帐户不能新建或发布 GPT，自定义 GPT 计划于 2026-12-11 退役。
- **Grok DeepSearch 作为现行功能名：** 未出现在 2026-11-25 查询的产品页和消费端概览中；本批不按旧名称教授。
- **Grok 消费端 Projects 的逐步点击教程：** 官方确认功能存在，但本轮未找到与 ChatGPT 相当的操作手册，故不编造步骤。

## 元数据

- 更新时间：2026-11-25（Asia/Shanghai）
- 来源：本目录当前技巧笔记和各篇文末列出的官方链接；总览与 2026-11-25 访问记录见 [ChatGPT.md](./ChatGPT.md)、[Grok.md](./Grok.md)、[Claude.md](./Claude.md)、[Codex.md](./Codex.md)
- 信息可信度：部分核对。本页作为索引已与第一批已完成的文件清单对齐。表中对照官方文档的条目为 Officially Documented 或按备注区分；本轮没有登录实操，不能当作上手验证。未完成分类为结构规划已核对，内容待后续研究补充
- 平台：见各篇笔记。未实测具体机型
- 技能门槛：会打开本库中的 Markdown 笔记并按出处核对。使用各产品的门槛见对应笔记
- 费用：免费 / 付费 / API 计费 / 不适用。未核对手表价，故不写入金额
