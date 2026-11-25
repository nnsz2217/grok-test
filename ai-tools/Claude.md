# Claude

这篇说明怎样进入 Claude（Anthropic 的对话助手）、它适合帮大学生做什么，以及官方已经写明的限制。不展开模型原理，也不写入未核对的价格或套餐金额。Claude Code 的用法不在本篇范围内，只在涉及共用额度时提到。

## 入口

- 网页：[claude.ai](https://claude.ai)，用浏览器即可开始对话。
- 桌面应用：可在 [官方下载页](https://support.claude.com/en/articles/10065433-install-claude-desktop) 安装 Claude Desktop。Windows 要求 Windows 10 或更高版本；也提供 macOS（13 或更高）和 Linux（beta）。装好后从开始菜单打开，登录账号即可。
- 手机：官方提供 iOS 和 Android 应用。
- 年龄：使用 Claude 服务须年满 18 岁。
- 地区：必须位于官方支持的地点。截至 2026-11-25 查询，[官方支持名单](https://support.claude.com/en/articles/8461763-where-can-i-access-claude) 未列出中国大陆、香港特别行政区和澳门特别行政区。
- 开始方法：在输入框用日常语言写出请求，点发送。点左下角 **+**，或输入 `/`，可以查看更多选项和命令。当前使用的模型会显示在输入框下方（网页和桌面）或屏幕顶部（手机），可以点开切换；也可以调整这次回答花费的力气，以及是否使用 extended thinking（扩展思考）。

## 适合什么任务

官方建议像和同事或朋友说话一样向 Claude 提问：简单问题可以直接问，复杂一些的分析、写作、多步骤任务也可以交给它，然后根据结果再追问或改要求。不必一次把提示词写完美。

对大学生比较实用、且已在官方文档里出现的用法包括：

- **带着自己的材料提问。** 把讲义、论文 PDF、笔记附到对话里，请它讲解、摘要、比较或按你的要求改写。先说明你要什么格式（例如“用三条要点解释这个概念，并标出我可能理解错的地方”）。
- **用 Projects（项目）做一门课或一份作业的工作区。** 项目可以自带对话历史和资料库，把相关文件和项目说明放在一起，之后在这个项目里聊天就不用反复交代背景。项目对所有用户开放，包括免费账号；免费用户最多可以创建 5 个项目。付费方案的项目在资料很多时可以使用 RAG，以处理更大容量的内容。
- **需要当前网上信息时使用网页搜索。** [Claude Academy](https://academy.claude.com/tutorials/getting-started-with-claude) 写明：网页搜索在 Free、Pro、Max、Ultra 方案上默认开启；Team 和 Enterprise 默认关闭，需由管理员打开。若只想根据你上传的文档回答，可以关掉搜索，或在提示里明确要求不要搜索。
- **Research（研究）。** 官方说明它会多次搜索并返回带引用的简报，适合较大的问题，需要几分钟，且在付费方案提供。本篇只记录这一官方描述，不做产品评测。

桌面应用在付费方案上还有 Cowork 等能力（在隔离环境里处理你授权的本地文件夹）。那部分偏“把任务交给助手去做”，本篇不展开，避免和 Agent 评测或后续专题重复。你在桌面应用里具体能用哪些功能，以官方安装说明中的方案对照表和你的账号为准。

## 限制

- **有用量限制，也会有单次对话长度限制。** 免费方案有按会话计算、每 5 小时重置的用量限制；可发送的消息数量还会随需求变化，官方也可能再施加其他限制以保证公平使用。达到上限或输入超出可用上下文时，Claude 会提示你。付费方案通常还有每 5 小时的会话限额，以及每周重置的周限额（已验证的 Ultra 账号没有 5 小时限额）。用量受对话长短、所用功能、所选模型和努力程度影响。
- **多个入口共用额度。** 在 claude.ai、Claude Code 和 Claude Desktop 上的使用，计入同一套用量限制。
- **单次对话记不住无限内容。** 这是上下文（工作记忆）限制，和上面的“一段时间能用多少”不是一回事。付费方案上较新模型的上下文窗口官方写到最大 1M token，其他为 500K 或 200K；一部分空间要留给回复。具体以官方按模型说明为准。
- **必须在支持地区，且须年满 18 岁。** 不在支持名单中，将无法按官方途径使用。
- **目前不能从其他 AI 产品导入对话历史。** Free、Pro、Max、Ultra 用户可以使用记忆导入功能，把其他 AI 产品中的记忆转到 Claude，这与导入完整聊天记录不是一回事。
- **桌面应用能做的事取决于方案。** Windows 10 可以安装官方 Desktop，但不等于免费方案拥有全部桌面功能。例如官方写明 Claude Cowork 面向付费方案（Pro、Max、Ultra、Team、Enterprise）。
- 本篇不写 Claude Code 的操作步骤。

## 元数据

- 更新时间：2026-11-25（Asia/Shanghai）
- 来源：
  - [Get started with Claude](https://support.claude.com/en/articles/8114491-get-started-with-claude)
  - [What interfaces can I use to access Claude?](https://support.claude.com/en/articles/8114487-what-interfaces-can-i-use-to-access-claude)
  - [Where can I access Claude?](https://support.claude.com/en/articles/8461763-where-can-i-access-claude)
  - [How do usage and length limits work?](https://support.claude.com/en/articles/11647753-how-do-usage-and-length-limits-work)
  - [Install Claude Desktop](https://support.claude.com/en/articles/10065433-install-claude-desktop)
  - [What are projects?](https://support.claude.com/en/articles/9517075-what-are-projects)
  - [Getting started with Claude · Claude Academy](https://academy.claude.com/tutorials/getting-started-with-claude)
- 信息可信度：部分核对。以上事实已对照 2026-11-25 可访问的官方帮助中心和 Claude Academy；未在中国大陆或不支持地区做登录实测，也未核对手表价或各方案具体消息条数。网页搜索在各方案上的默认开关来自 Claude Academy，不是帮助中心同一条目，已单独标注来源。
- 平台：已核对网页 claude.ai、官方所述 iOS / Android 应用，以及 Windows 10 或更高版本可安装 Claude Desktop 的说明。未实测具体机型。
- 技能门槛：会用浏览器访问网站、注册或登录账号，并能用中文或英文说明自己的任务。不需要编程。使用须年满 18 岁。
- 费用：免费 / 付费。官方写明有免费方案，以及 Pro、Max、Ultra、Team、Enterprise 等付费或团队方案；未核对具体价格，故不写入金额。
