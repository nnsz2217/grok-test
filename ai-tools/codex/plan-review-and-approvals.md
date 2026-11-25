# 先做计划，再改代码，并做审查

适用产品：OpenAI Codex。把“想清楚、改动、检查”分成可控制的步骤，并保留默认的安全限制。以下为官方说明，状态为 Officially Documented。本轮没有运行 Codex，不能当作已经实测成功。

## 1. 复杂任务先用 Plan 模式，同意后再改文件

**用途：** 在目标还不清楚、涉及多个文件、或你还不敢让它直接改作业时，先让它收集上下文、提问并给出计划。

**操作方法：**

1. 官方写明，对大多数用户，最省事的方式是打开 Plan 模式：在 CLI 使用 `/plan`，或用 Shift+Tab 切换。
2. 若只有模糊想法，可以请它先采访你：对你的假设提出疑问，把想法变成具体计划，再开始写代码。
3. 更进阶的用法是为较长任务准备 `PLANS.md` 或执行计划模板，见官方 execution plans 指南。本篇不把该模板写成入门必做项。
4. 官方还建议在任务前后创建 Git 检查点，以便还原。没有 Git 时，桌面应用的部分审查功能不可用，见 Windows 笔记。

**可复制的提示词示例：**

```text
请先进入计划模式，不要改任何文件。
阅读这个课程项目，提出你准备怎样修复“空列表显示 NaN”的问题。
列出将要修改的文件、测试计划，以及你需要我确认的问题。
我同意之前不要开始编辑。
```

**适用场景：** 第一次接触某个课程仓库；一次改动可能影响多个文件；你希望先看到步骤再授权。

**限制：** 计划仍然可能有错，需要你看过再同意。官方提醒不要在还不理解工作方式时，就给 Codex 完整的电脑权限。本轮未实测 `/plan` 界面，属 Unverified。

**来源与可信度：** Officially Documented。[Best practices](https://learn.chatgpt.com/guides/best-practices)、[Prompting](https://learn.chatgpt.com/docs/prompting)、[Codex CLI](https://learn.chatgpt.com/docs/codex/cli)。查询日期 2026-11-25。

## 2. 保留沙箱和审批，不要一上来关闭保护

**用途：** 让 Codex 只能在你允许的范围内读文件、改文件或上网，降低误改系统文件或运行意外命令的风险。

**官方已经写明的要点：**

- 安全由两层一起构成：**沙箱模式**决定它在执行命令时技术上能做什么（例如能写到哪里、能否访问网络）；**审批策略**决定它在何种情况下必须先问你（例如离开沙箱、使用网络、或运行受信任集合之外的命令）。
- 默认情况下，代理运行时网络是关闭的。本地使用操作系统强制的沙箱，通常限制在当前工作区，再加上审批策略。
- 新使用编码代理的人，应先保持默认权限，只在可信仓库或明确需要时再放宽。
- 名为 `untrusted` 的旧审批策略已经退役，Codex 和 ChatGPT Work 不再支持 `approval_policy = "untrusted"`。配置里若仍保留，可能导致客户端无法启动。应删掉用户或项目配置中的该项。官方给出的交互式只读示例是 `sandbox_mode = "read-only"` 与 `approval_policy = "on-request"`，或命令行 `codex --sandbox read-only --ask-for-approval on-request`。在 `on-request` 下，沙箱允许的命令可以不经询问运行；若已打开网络，也可使用网络。
- 可在 CLI 使用 `/permissions` 查看或调整当前会话允许做的事，并在继续前检查沙箱和可写根目录。

**适用场景：** 第一次在个人作业文件夹里使用 Codex；或要临时打开网络以便查阅文档。

**限制：** 审批不是万能的。你批准的命令仍会真实执行。不要在含有密钥、密码或未备份的重要文件的目录里做高权限试验。本轮未查看默认策略在某一设备上的实况，属 Unverified。配置示例来自官方文档，不是要求你改成更宽松的设置。

**来源与可信度：** Officially Documented。[Agent approvals & security](https://learn.chatgpt.com/docs/agent-approvals-security)、[Best practices](https://learn.chatgpt.com/guides/best-practices)、[Codex CLI](https://learn.chatgpt.com/docs/codex/cli)。查询日期 2026-11-25。

## 3. 改完后用 /review 做一次检查，再提交

**用途：** 在提交作业或打开 Pull Request 前，让 Codex 按你的关注点检查改动，而不是只看“它说已经修好了”。

**操作方法：**

1. 官方建议不要止于“请改一下”，还要让它在需要时补测试、运行相应检查、确认结果，并在你接受前审查。这些要求可以写在提示词或 `AGENTS.md` 里。
2. 在 CLI 运行 `codex` 后输入 `/review`。可选预设包括：相对某一基础分支做类似 PR 的审查、审查未提交的改动、审查某次提交，或给出自定义审查说明。也可以写成 `/review Focus on edge cases and security issues`。
3. 官方写明：审查会报告优先发现的问题，并且不修改你的工作区，便于在提交前处理风险。根据反馈修改后，可再运行一次 `/review`。
4. 在桌面应用中，可用差异面板查看改动，并针对某一行给出反馈，作为下一轮上下文。
5. 若在 GitHub 上启用了 Codex 代码审查，也可以在 Pull Request 里用评论点名，例如 `@codex review` 或更具体的 `@codex review for security vulnerabilities and security concerns`。这需要先按官方 Code review 文档完成仓库设置，不是命令行 `/review` 的必做项。

**适用场景：** 课程作业准备提交；修改已经涉及多个文件；想先听一遍“可能漏掉的边界情况”。

**限制：** 审查意见不是最终正确性保证，仍要你自己看差异和测试结果。GitHub 上的自动审查是另一套设置。本轮未运行 `/review`，属 Unverified。

**来源与可信度：** Officially Documented。[Best practices](https://learn.chatgpt.com/guides/best-practices)、[Prompting](https://learn.chatgpt.com/docs/prompting)、[Codex CLI](https://learn.chatgpt.com/docs/codex/cli)。查询日期 2026-11-25。

## 元数据

- 更新时间：2026-11-25（Asia/Shanghai）
- 来源：上文各官方学习文档链接
- 信息可信度：部分核对。Plan 模式、沙箱与审批规则、`/review` 的用途为 Officially Documented。本轮未运行这些命令，属 Unverified。未核对手表价
- 平台：CLI、桌面应用和 IDE。GitHub 评论审查需额外设置。Windows 用户需先装 Git 才能使用部分差异功能。未实测
- 技能门槛：会切换 Plan 模式，并阅读差异。使用 `/review` 需要会在 CLI 或应用中输入斜杠命令。不需要先会写安全策略文件
- 费用：免费 / 付费 / API 计费。计划、修改和审查都会消耗用量；未核对手表价，故不写入金额
