# Codex 高级技巧

本目录整理 OpenAI Codex 的高级用法，作为 [产品总览](../Codex.md) 的补充。Codex 面向软件开发，和 ChatGPT 的普通对话不是同一套界面。

本批对照官方学习文档整理，查询日期为 2026-11-25（Asia/Shanghai）。没有登录或在本地运行 Codex，所以功能状态只用 Officially Documented、Community Reported 或 Unverified，不标 Verified，也不声称已经实测成功。

使用 ChatGPT 帐户登录时，地区限制与 ChatGPT 相同，见总览。登录不需要谷歌帐户；只有在安装依赖 Gmail 或 Google Drive 的插件时才需要谷歌帐户，相关处会标明。

## 当前内容

- [选择入口并说明任务](./surfaces-and-first-prompts.md)：桌面应用、IDE、CLI 和 Cloud 怎么选；以及“目标、上下文、限制、完成标准”四段提示。
- [Windows 上的安装与沙箱](./windows-setup.md)：原生 Windows 与 WSL2 的官方建议并不完全相同，需按实际环境选择。
- [用 AGENTS.md 写可复用约定](./agents-md.md)：全局、仓库和子目录说明如何叠加，以及 `/init` 只是起点。
- [先做计划，再改代码，并做审查](./plan-review-and-approvals.md)：Plan 模式、默认沙箱与审批、以及 `/review`。不要一上来关闭保护。
- [技能与插件](./skills-and-plugins.md)：把反复出现的流程做成技能，或安装官方目录中的插件。

## 元数据

- 更新时间：2026-11-25（Asia/Shanghai）
- 来源：本目录当前文件清单；各篇事实来源见文末。产品总览见 [../Codex.md](../Codex.md)
- 信息可信度：部分核对。本页作为索引已与当前文件清单对齐。各篇对照官方文档的内容为 Officially Documented。本轮没有运行 Codex，不能当作上手验证
- 平台：官方文档中的 ChatGPT 桌面应用（含 Windows）、VS Code 兼容编辑器、CLI，以及 WSL2。未实测
- 技能门槛：会打开项目文件夹并阅读它建议的改动。CLI 和 AGENTS.md 需要能编辑一个 Markdown 文件并在终端运行命令。不要求计算机专业，但任务本身是编程
- 费用：免费 / 付费 / API 计费。未核对手表价，故不写入金额
