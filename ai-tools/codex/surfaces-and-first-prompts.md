# 选择入口并说明任务

适用产品：OpenAI Codex（ChatGPT 桌面应用、IDE 扩展、CLI、Codex Cloud）。先选对入口，再用清楚的任务说明，通常比把整份课程要求一次性粘贴进去更有效。以下为官方说明，状态为 Officially Documented。本轮没有运行 Codex，不能当作已经实测成功。

## 1. 按你现在的工作方式选择入口

**用途：** 避免只为改三行代码去配置一整套命令行，或在没有项目文件夹的网页对话里要求它“直接改我电脑上的作业”。

**官方入口怎样选：**

- **IDE 扩展：** 适合已经在 VS Code、Cursor、Windsurf、Xcode 或 JetBrains 里打开项目的人。可以把当前打开的文件、选中的代码和最近的对话带到输入框里，并在编辑器旁边查看改动。
- **ChatGPT 桌面应用中的 Codex：** 适合希望在同一应用里切换 Chat / Work / Codex，并使用本地文件夹、工作树、插件和技能的人。Windows 应用支持原生沙箱与 PowerShell，也可改用 WSL2。
- **CLI：** 适合习惯终端，或需要 `codex exec` 做重复脚本和 CI 的人。在项目目录运行 `codex`。常用命令包括 `/init`（生成 AGENTS.md）、`/status`、`/permissions`、`/model`、`/review`。
- **Codex Cloud：** 适合任务较大、想交给云端环境稍后再把结果应用回本地的情况。可从终端使用 `codex cloud`，也可在网页或桌面应用中提交。官方写明：交给云端的任务在隔离环境中运行，代理阶段默认关闭互联网，除非你为该环境打开。

官方建议：为软件开发选择 Codex；为研究分析和做文档、演示、表格等成品选择 Work；为快速提问选择 Chat。不要把这三者当成同一个开关上的三个模型名。

**适用场景：** 课程编程作业已经在 VS Code 里打开，优先用 IDE 扩展；只想在文件夹里试一次，可用桌面应用；需要以后重复执行同一条命令，再考虑 CLI。

**限制：** 各入口能用的模型、插件和本地文件能力并不完全相同，以帐户和官方说明为准。使用 API 密钥登录时，官方写明部分功能可能不可用。本轮未安装任何入口，属 Unverified。

**来源与可信度：** Officially Documented。[Quickstart](https://learn.chatgpt.com/docs/quickstart)、[Codex CLI](https://learn.chatgpt.com/docs/codex/cli)、[Codex IDE extension](https://learn.chatgpt.com/docs/codex/ide)、[Prompting](https://learn.chatgpt.com/docs/prompting)。查询日期 2026-11-25。

## 2. 第一次就写清：目标、上下文、限制、完成标准

**用途：** 让 Codex 少做假设、改动范围更小、也更容易检查是否做完。官方最佳实践把这四项作为默认结构。

**操作方法：**

1. **目标：** 你要改什么或做什么，用结果而不是含糊的“优化一下”。
2. **上下文：** 哪些文件、文件夹、报错或示例相关。在 IDE 或 CLI 里可以用 `@` 提到文件。
3. **限制：** 哪些约定或安全要求必须遵守，哪些文件不要动。
4. **完成标准：** 怎样才算做完，例如某项测试通过、某个错误不再出现、或某段行为发生变化。

若 GPT-6.2 Sol 可用，官方建议多数任务从它开始；跨多个软件包的改动再在选择器中改用 GPT-6.2 Astra。推理力度先用客户端的默认值。官方还提示：GPT-6 Luna 可从 High 开始，GPT-6 Astra 可从 Light（配置里的 `low`）开始。具体选项以你帐户为准。普通 Chat 的选择器与 Codex 并不完全相同，见 ChatGPT 的模型选择笔记。

**可复制的提示词示例：**

```text
目标：修复学生成绩页面在没有成绩时仍显示“NaN”的问题。
上下文：请先看 @src/grades.js 和 @src/grades.test.js，以及我粘贴的报错。
限制：不要改数据库结构，不要新增依赖。保持现有的函数名。
完成标准：当成绩列表为空时显示“暂无成绩”；现有测试以及你新增的回归测试都通过。
先告诉我你准备改哪些文件，等我同意后再改。
```

```text
请先不要改代码。用你看到的仓库说明：这个项目怎么启动、测试命令是什么、和本次作业最相关的文件夹在哪。
列出你还不确定的问题，向我确认后再继续。
```

**适用场景：** 任何一次具体的修改、排错或解释任务。第二例适合你还不完全熟悉这个课程项目时。

**限制：** 提示词再清楚，也不等于可以不看差异。官方还提醒：一个对话对应一个完整的工作单元；整学期都挤在同一条超长对话里，上下文会膨胀、效果会变差。同一问题的后续追问可以留在同一对话；真正分叉时再用 `/fork`。本轮未实测对话变长后的表现。

**来源与可信度：** Officially Documented。[Best practices](https://learn.chatgpt.com/guides/best-practices)、[Prompting](https://learn.chatgpt.com/docs/prompting)、[ChatGPT Work and Codex](https://help.openai.com/en/articles/20001275-chatgpt-work-and-codex)。查询日期 2026-11-25。

## 元数据

- 更新时间：2026-11-25（Asia/Shanghai）
- 来源：上文各官方学习文档与帮助中心链接
- 信息可信度：部分核对。入口划分和提示结构为 Officially Documented。本轮未运行 Codex，推荐模型在你帐户里是否可见为 Unverified。未核对手表价
- 平台：桌面应用（含 Windows）、VS Code 兼容编辑器、CLI、Cloud。未实测
- 技能门槛：会打开项目并说明要改的结果。使用 `@` 提及文件需要在相应入口里操作一次。不需要先会写配置文件
- 费用：免费 / 付费 / API 计费。模型与云端任务都会占用方案或额度；未核对手表价，故不写入金额
