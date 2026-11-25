# Chat、Work 与模型选择

适用产品：ChatGPT 的普通 Chat（对话）、ChatGPT Work，以及同一应用里的 Codex 入口。先选对工作区，再选思考程度，通常比反复改一句提示词更省事。以下为官方说明，状态为 Officially Documented。本轮没有登录实操，不能当作已经实测成功。

官方另有一篇帮助写明：**ChatGPT agent（代理模式）已不再提供**，较长的多步骤任务和成品交付应使用 ChatGPT Work。不要再按旧教程寻找 `/agent` 或 agent mode。查询日期 2026-11-25。

## 1. 先分清 Chat、Work 和 Codex

**用途：** 避免用普通闲聊去交一份要反复改的报告，或把写代码的任务丢在不带仓库上下文的对话里。

**官方区分：**

- **Chat：** 快速对话、日常提问、头脑风暴、把一个问题谈清楚。
- **Work：** 面向更长的多步骤任务和可交付成品，例如报告、幻灯片、表格、项目计划。它会规划步骤、调用工具，并给出你能预览和修改的结果。具体能力随方案、平台、地区、是否逐步开放以及工作区管理员设置而变。
- **Codex：** 面向软件开发和偏技术的工作。它在桌面应用中提供，Codex Cloud 也可从桌面、网页或手机继续编程任务。详细用法见本库的 [Codex 总览](../Codex.md) 和 [codex/](../codex/) 目录，本篇不展开命令行操作。

在桌面应用中：从菜单选择 ChatGPT 或 Codex；在 ChatGPT 里用开关选择 Chat 或 Work。Chat 与 Work 的记录会出现在 Recents，可用筛选查看；Codex 是单独视图，历史不与 ChatGPT 历史混在一起。在手机上，若看到 Explore，从 Home 开新对话后，点输入框上的模型名称来选择 Chat 或 Work。

**适用场景：** 问概念、改一句表述，用 Chat；要一份可下载或可继续改的文档、表格或幻灯片，用 Work；要在代码仓库里改文件或查错，用 Codex。

**限制：** Work 的用量结构与 Codex 相同，额度说明见官方 Codex 定价页；该页示例以编程任务为基础，Work 的实际消耗会因任务而异。本篇不写入未核对的价格或额度数字。云端 Work 与桌面应用里访问本地文件的能力可能分批开放，且受工作区权限影响。

**来源与可信度：** Officially Documented。[ChatGPT Work and Codex](https://help.openai.com/en/articles/20001275-chatgpt-work-and-codex)、[ChatGPT agent](https://help.openai.com/en/articles/11752874-chatgpt-agent)、[What is ChatGPT: FAQ](https://help.openai.com/en/articles/12677804-what-is-chatgpt-faq)。查询日期 2026-11-25。

## 2. 按任务难度选择思考等级，而不是只追最新模型名

**用途：** 简单问题用更快的档，较难的推理再用更长思考，减少不必要的等待和额度消耗。模型名称会随时间更新，官方选择器里的思路更稳定：Instant / Medium / High / Extra High，以及符合条件时的 Pro。

**操作方法（以 2026-11-25 的官方说明为准）：**

1. 在 Chat 的模型选择器中查看当前显示的是 Latest、GPT-6、GPT-6.2 还是 GPT-5.6 Sol。选项因方案和工作区而异，也在逐步开放中。
2. 用思考滑杆或同等控件选择力度：
   - **Instant：** 日常快问快答。Free 和 Go 使用 GPT-5.6 Luna。
   - **Medium：** 常规思考。
   - **High：** 更长的思考。
   - **Extra High：** GPT-6 Sol 可用的最高思考等级。
   - **Pro：** 更困难、耗时更长的任务。可选模型包括 GPT-5.6 Sol Pro，以及符合条件时由 GPT-6 Astra 驱动的 GPT-6 Pro。
3. 若选择器显示 GPT-6.2，则 Latest 在可用时会把 Instant、Medium、High、Extra High 放到 GPT-6.2 上。若仍显示较旧选择器，GPT-6 会在同一思考等级上替代 Latest。若你明确选了 GPT-5.6 Sol，会保持在 GPT-5.6。
4. Free 和 Go 没有 Medium、High、Extra High 和 Pro；较难的问题可使用 Think，它由 GPT-5.6 Luna 驱动，不是 GPT-5.6 Sol。未登录用户也不能使用 GPT-5.6 Sol。
5. Plus 包含 Medium 和 High，不包含 Extra High 和 Pro。Pro、Business、Enterprise 在官方对照表中包含 Extra High 和 Pro。托管工作区还取决于管理员的模型权限。
6. Chat 与 Work / Codex 的可选模型并不完全相同。例如 GPT-6.2 Astra 和 GPT-6.2 Sol 在 Work 模型选择器或 Codex 选择器中选择；GPT-6.1 Sol、GPT-6.1 Terra、GPT-6 Luna 出现在 Work 和 Codex，不作为普通 Chat 里的单独 Sol / Terra / Luna 选项。普通 Chat 里的 GPT-6 由 GPT-6 Sol 驱动，选择器上不一定单独标出 Sol。
7. 用尽某一思考档或 Pro 模型额度后，官方写明可能改用其他可用模型，或需等到重置。客服不会重置用量。具体额度因方案而异，本篇不写数字。

**适用场景：** 解释一个概念或改措辞，用 Instant 或 Medium；要比较多种证据、分多步推导，再用 High 或更高档（若你的方案包含）。

**限制：** 模型名单和默认项仍在滚动更新，本页以查询当日官方说明为准，过几个星期可能又会变。不要把第三方评测里的旧模型名当成当前选择器内容。GPT-6 在 Chat 中的 Intelligent UI（可把文字、视觉和交互元素结合在回答里）只适用于 Instant 到 Extra High，不适用于由 GPT-6 Astra 驱动的 Pro 档；旧版 macOS / Windows 桌面应用不支持这些能力，官方建议改用网页。可在网页 Settings 中关闭 Layout and visuals 以减少视觉元素，但不会变成完全的纯文本模式。

**来源与可信度：** Officially Documented。[GPT-6 and other models in ChatGPT](https://help.openai.com/en/articles/20001354-gpt-6-and-other-models-in-chatgpt)、[ChatGPT Work and Codex](https://help.openai.com/en/articles/20001275-chatgpt-work-and-codex)。查询日期 2026-11-25。本轮未登录查看选择器实况，属 Unverified。官方文档出现了 Pro 方案的分档名称，本篇不转写任何价格。

## 3. 用 Work 生成可再编辑的文档、表格或幻灯片

**用途：** 把“最后要交出一份文件”说清楚，并让它按你的材料或模板来做，而不是只得到一段聊天文本。

**操作方法：**

1. 打开 Work，说明要做什么文件、给谁用、必须保持不变的内容（例如公式、版式、语气、页序）。
2. 附上源材料。对表格，说明需要哪些工作表、列、公式和图表；对演示文稿，说明章节、幻灯片类型和你要检查的视觉要求。
3. 若已有样例，明确告诉它“版式和结构跟这份走，内容换成我附上的新材料”。只用一次时，附上参考文件即可；经常重复的格式，可做成模板。
4. 在网页版 Work 或桌面应用的 Codex 中，可用 `@Template-Creator` 根据一份 Word / Excel / PowerPoint 或 Google 文档链接创建模板。之后用 `@Documents`、`@Spreadsheets` 或 `@Presentations` 打开模板库。选择模板不会自动开始任务，还需要补充这次的材料和说明。
5. 网页上创建的模板与 Codex 保存在本地的模板是分开的，不会自动同步。
6. 完成后检查内容、版式、公式和图表，再分享或使用。

**必须有谷歌帐户的部分：** 官方写明，在相应 Google Workspace 应用已启用并可连接时，Work 可以创建或编辑原生的 Google Docs、Sheets、Slides；用 Google 文件作为模板参考时，也需要能打开该文件的谷歌帐户。**没有谷歌帐户时，改用上传的 Word / Excel / PowerPoint 文件，不要走 Google 原生文档流程。** ChatGPT 桌面应用还可通过 ChatGPT for Excel 加载项处理打开的 Excel 工作簿；官方写明该桌面流程在上线时不包含 PowerPoint。

**可复制的提示词示例：**

```text
请在 Work 里做一份 8 页左右的课程报告幻灯片，给 10 分钟课堂汇报用。
材料只使用我附上的两份 PDF。
请包含：研究问题、方法、主要发现、局限、两个讨论问题。
每页标题明确，正文不要超过 5 条要点。
不要编造材料里没有的数据和文献。
先给出大纲让我确认，我同意后再生成幻灯片。
```

**适用场景：** 课程报告、一周读书摘要、把问卷结果做成图表和简短说明。

**限制：** 能否使用取决于方案、工作区设置、文件类型和使用入口（网页或桌面）。云端 Work 生成的文件可能保存到 Library 或 Space；桌面本地输出可能只留在本地项目或文件夹，不会自动出现在网页或手机。Temporary Chat 中创建的文件不会保存到 Library。分享由模板新建的 Google 文件前，应在 Google Workspace 中检查位置和共享设置。本轮未实测模板和导出效果。

**来源与可信度：** Officially Documented。[Creating and editing documents, spreadsheets, and presentations with ChatGPT Work](https://help.openai.com/en/articles/20001278-creating-and-editing-documents-spreadsheets-and-presentations-with-chatgpt-work)、[ChatGPT Work and Codex](https://help.openai.com/en/articles/20001275-chatgpt-work-and-codex)。查询日期 2026-11-25。

## 元数据

- 更新时间：2026-11-25（Asia/Shanghai）
- 来源：上文各官方帮助中心链接
- 信息可信度：部分核对。Chat / Work / Codex 的区分、代理模式已退出、思考等级和 Work 做文件的步骤为 Officially Documented。本轮未登录查看选择器和 Work 界面，属 Unverified。未核对手表价或具体额度
- 平台：官方说明覆盖网页、手机和桌面应用（含 Windows）。Intelligent UI 在旧版桌面应用不可用。未实测具体机型
- 技能门槛：会在 Chat 和 Work 之间切换，并能说明要交付的文件格式。使用 Google 原生文档需要谷歌帐户；否则可使用上传的 Office 文件。不需要编程
- 费用：免费 / 付费。思考等级和 Work 能力随方案而变；未核对手表价，故不写入金额
