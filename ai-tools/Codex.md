# Codex

这篇说明怎样进入 OpenAI Codex、它适合帮大学生做什么，以及官方已经写明的限制。不展开模型原理，也不写入未核对的价格或套餐金额。ChatGPT 普通对话和 ChatGPT Work 的用法见 [ChatGPT.md](./ChatGPT.md) 和 [chatgpt/](./chatgpt/)；本篇只写面向软件开发的 Codex。更细的操作技巧在 [codex/](./codex/)。

本篇对照官方学习文档与帮助中心整理，查询日期为 2026-11-25（Asia/Shanghai）。本轮没有登录或在本地运行 Codex，不能当作已经实测成功，也不标 Verified。

## 入口

- **ChatGPT 应用中的 Codex：** 在 [ChatGPT 桌面应用](https://learn.chatgpt.com/docs/quickstart) 的产品选择里选 Codex，用于带代码库上下文的开发工作。网页和手机可以查看或继续 Codex Cloud 任务；手机还可通过 Remote 标签与受支持的桌面 Codex 对话交互。
- **IDE 扩展：** 官方支持 Visual Studio Code 及兼容编辑器（包括 Cursor、Windsurf、VS Code Insiders），以及 Xcode 和 JetBrains IDE。在 VS Code / Cursor / Windsurf 中，点击 Codex 图标，或用命令面板运行 “Codex: Open Codex Sidebar”，登录后在当前项目里提问。
- **命令行（CLI）：** 在项目目录运行 `codex`。macOS / Linux 可用官方安装命令 `curl -fsSL https://chatgpt.com/codex/install.sh | sh`。Windows 可使用原生安装，或在 WSL2 中使用同一安装脚本。首次运行时选择 Sign in with ChatGPT 或其他可用登录方式；也可以使用 API 密钥，但官方写明部分功能可能因此不可用。
- **Windows：** 官方 ChatGPT 桌面应用可在 Windows 上原生运行，使用 PowerShell 和 Windows 沙箱，也可改到 WSL2。系统要求和谁能安装桌面应用，以 ChatGPT 总览引用的专门帮助页为准。CLI 另有原生 Windows 与 WSL2 两种方式，详见 [Windows 上的安装与沙箱](./codex/windows-setup.md)。
- **地区与帐户：** 使用 ChatGPT 帐户登录时，须位于 [ChatGPT 与 OpenAI API 支持的国家和地区](https://help.openai.com/en/articles/7947663-chatgpt-and-openai-api-supported-countries-and-territories)。截至 2026-11-25，该名单未列出中国大陆、香港特别行政区和澳门特别行政区。这与 ChatGPT 总览是同一条 Officially Documented 事实。研究环境当日访问 ChatGPT 的结果见 [ChatGPT.md](./ChatGPT.md)，状态为 Unverified。不讨论绕过方法。Codex 本身本轮未做上手测试，状态为 Unverified。
- **开始方法：** 打开一个项目文件夹，说明你想让它解释、修改或排查的问题。官方建议在任务前后使用 Git 检查点，以便还原修改。登录不需要谷歌帐户。

## 适合什么任务

官方把 Codex 定位为软件开发和技术工作，而不是普通问答：

- 在当前仓库里查看代码、做有范围的修改、运行已安装的本地工具、解释不熟悉的项目。
- 在终端、编辑器或桌面应用里保持同一套工作循环：说明目标、查看命令和改动、在同一会话里追问。
- 使用 `/review` 或 IDE 里的差异视图，在提交或开 Pull Request 之前做代码审查。
- 把可重复的项目约定写进 `AGENTS.md`，把可重复的流程做成技能或插件。
- 把较大的任务交到 Codex Cloud，稍后再把结果应用回本地仓库。

对非计算机专业、但愿意尝试的学生：如果只是交一篇读书报告或整理笔记，应优先使用 ChatGPT 的 Chat 或 Work，不必先学 Codex。只有当你已经有一个代码练习、网页小项目或课程编程作业，并且愿意在文件夹里查看它建议的改动时，再进入 Codex。你不必先成为程序员，但需要能看懂“它改了哪些文件”，并在不确定时拒绝或还原修改。

## 限制

- **面向代码工作。** 它需要项目文件夹、以及你允许的文件和命令权限。不要在没有备份或 Git 的情况下，把重要作业文件夹直接交给它任意修改。
- **有用量限制。** Work 与 Codex 使用同一套用量结构，具体数字以帐户和官方说明为准。本篇不写未核对的价格。官方写明客服不会重置用量。
- **地区和帐户限制与 ChatGPT 相同**（在使用 ChatGPT 帐户登录时）。名单以外的访问风险见 ChatGPT 总览，不在此重复讨论绕过方法。
- **默认关闭网络，并受沙箱和审批策略约束。** 这是保护措施，不是故障。新用户应先保持较严格的默认权限，不要一上来就关闭审批。名为 `untrusted` 的旧审批策略已退役，配置里若仍保留可能导致无法启动，见审批与审查笔记。
- **模型选择器与普通 Chat 不完全相同。** 例如 GPT-6.2 Astra 和 GPT-6.2 Sol 在 Codex 选择器中选择；CLI 使用这些模型需要官方写明的最低版本（查询当日：GPT-6.2 需要 CLI `0.166.0` 或更高）。以当前官方说明和你帐户内的选项为准。
- **Windows 有两条因场景而异的路径建议。** 在 WSL2 里开发时，官方建议把仓库放在 Linux 主目录，而不是 `/mnt/c`；若希望 Windows 原生代理处理同时也可被 WSL 访问的项目，官方又提示把项目放在 Windows 磁盘、再通过 `/mnt/...` 访问。请按你实际使用的代理环境选择，详见 Windows 笔记。WSL1 自 Codex `0.115` 起不再支持。
- 本轮没有在本地安装或登录 Codex，以上均为文档说明，不是上手验证。

## 元数据

- 更新时间：2026-11-25（Asia/Shanghai）
- 来源：
  - [Quickstart](https://learn.chatgpt.com/docs/quickstart)
  - [Codex CLI](https://learn.chatgpt.com/docs/codex/cli)
  - [Codex IDE extension](https://learn.chatgpt.com/docs/codex/ide)
  - [ChatGPT desktop app for Windows](https://learn.chatgpt.com/docs/windows/windows-app)
  - [WSL](https://learn.chatgpt.com/docs/windows/wsl)
  - [ChatGPT Work and Codex](https://help.openai.com/en/articles/20001275-chatgpt-work-and-codex)
  - [GPT-6 and other models in ChatGPT](https://help.openai.com/en/articles/20001354-gpt-6-and-other-models-in-chatgpt)
  - [ChatGPT and OpenAI API supported countries and territories](https://help.openai.com/en/articles/7947663-chatgpt-and-openai-api-supported-countries-and-territories)
  - [Agent approvals & security](https://learn.chatgpt.com/docs/agent-approvals-security)
- 信息可信度：部分核对。对照官方文档的入口、定位和限制为 Officially Documented。本轮未安装、未登录、未运行 Codex，所有上手结果均为 Unverified。未核对手表价或具体额度
- 平台：已核对官方文档中的 ChatGPT 桌面应用（含 Windows）、VS Code 兼容编辑器、CLI，以及 WSL2。未实测具体机型或发行版
- 技能门槛：会打开一个项目文件夹，并愿意检查它改了哪些文件。使用 CLI 需要会在终端里进入目录并运行一条命令。不是必须先有计算机专业背景，但 Codex 本身面向编程任务
- 费用：免费 / 付费 / API 计费。可用 ChatGPT 方案登录，也可用 API 密钥（官方写明部分功能可能不可用）。Work 与 Codex 共用用量结构。未核对手表价，故不写入金额
