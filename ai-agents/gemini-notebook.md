# Gemini Notebook

Gemini Notebook 是 Google 的研究和学习工具，2026 年 7 月由 NotebookLM 改名而来。官方博客写明它仍是原来那个独立产品。你把课件、论文、笔记或网页放进一个笔记本，再针对这些材料提问；回答带引用，方便回到原文核对。工作室还能把同一批材料做成学习指南、测验、音频或幻灯片。它和开放式聊天的差别在于：帮助中心写明，聊天回答只用你选中的来源。

当前网页入口是 [notebook.google.com](https://notebook.google.com/)。本次请求 `https://notebooklm.google.com/` 时，最终地址也落到 `https://notebook.google.com/`。

## 能做什么

帮助学生直接用的部分，来自帮助中心「创建笔记本」和「来源」页：

- 每个笔记本是一组独立来源。帮助中心写明，它不能同时使用多个笔记本里的材料。
- 可以加入的来源包括：PDF、Microsoft Word、PowerPoint、Excel 所用的 csv、纯文本、Markdown、Google 文档、Google 幻灯片（帮助页写最多 100 页）、Google 表格（帮助页写目前单个文件最多约 10 万 token）、网页 URL、有字幕的公开 YouTube 视频、音频、图片、ePub、符合条件的 Play Books，以及粘贴的文字。每条来源最多约 50 万词，或上传文件最多 200 MB。网页只取正文，付费墙页面不支持；YouTube 只导入字幕文本。
- 聊天针对选中的来源回答，并用引文标出来源。悬停可以看摘录，点开可以回到原文。帮助中心建议你自己核对引文。若要求改写故事结局这类脱离来源的创作，可能得到「无法回答」。
- 工作室可以生成：笔记、音频概览、视频概览、思维导图、报告（含 FAQ、学习指南、简报，或由它建议的类型）、数据表、抽认卡、测验、幻灯片、信息图。报告可以导出到 Google 文档；带表格时可以导出到表格。导出后的文件不会再同步回笔记本。
- 来源页描述的 Deep Research：在来源面板打开网页和 Deep Research 后，它会浏览网站并写出一份报告，你再选择把报告和来源导入笔记本。帮助页写它可以浏览多达数百个网站。该段同时写明目前仅向 18 岁以上用户提供，并受来源数量限制。该段没有另写「必须购买某一档」。
- 聊天帮助还描述了一组实验性的代理动作：搜索网页、运行代码、生成可下载的 PDF、Word、Excel、PowerPoint、图片和表格。帮助页写明这些功能仍在早期，可能出错，需要你看着它做。

2026-07-16 的官方博客写，每个笔记本配一台安全的云端电脑，用来在来源范围内写和运行代码；当天提供给 Google AI Ultra，以及带有 AI Ultra Access、AI Expanded Access 的 Workspace 商业客户，并会在随后数周向网页版 Pro 推出。本次打开的聊天帮助已经描述「运行代码、生成文件」，却没有在同一段重复这张套餐名单。因此本文只记录这两处原文，不把「每个免费账号都已经有完整云端电脑」写成事实。以你登录后能否看到这些按钮为准。

## 怎么开始

1. 用个人 Gmail，或所在学校、公司已经开通的 Google 账号，打开 [notebook.google.com](https://notebook.google.com/)。套餐页写：不收费方案用 Gmail 注册即可；学校或工作账号要管理员打开权限。
2. 选择新建笔记本，上传或搜索来源。聊天面板会出现一份来源摘要，可以直接提问，也可以换成 Learning Guide 这类对话风格。
3. 需要学习资料时，到工作室生成学习指南、抽认卡、测验、音频或幻灯片。
4. 不需要编程。电脑浏览器即可使用，帮助页的操作说明写的是 computer。本批没有在 Windows 上亲手点过，也没有看到帮助页把 Windows 排除在外。
5. 创建、聊天和来源三篇帮助都写：手机应用目前可能缺少部分功能。手机上的国家名单也和电脑版分开，见可用性一节。

中国大陆与地区：套餐页和产品介绍页都写，浏览器版向达到所在地同意年龄的用户提供，范围是「支持的国家和地区」。电脑版国家名单在 [Learn about Gemini Notebook](https://support.google.com/gemininotebook/answer/16164461?hl=en)。本次从该页提取的名单里没有名为 China、Hong Kong 或 Macau 的条目。这只说明名单页面上的写法。请自己打开该页核对，并用自己的 Google 账号试 `notebook.google.com`。本文不把名单结果写成「你的网络一定打得开」或「一定打不开」。

## 能力边界

- 回答被帮助中心限定在选中的来源里。来源没写的内容，它可能直接拒绝，也可能答错。引文要自己点开看。
- 医疗、法律、金融建议，帮助页写明不能代替专业人士。
- 上传你没有权利使用的材料，帮助页要求不要这么做。
- Deep Research 和部分功能有 18 岁限制。18 岁以下还有更严的内容政策。
- 实验性的网页搜索、跑代码和生成 Office 文件，帮助页要求你监督。云端电脑的套餐范围，以 2026-07-16 博客和你账号里的实际入口一起看，见上文。
- 用量帮助写的是按计算量计的额度，大约每 5 小时刷新一次，直到周上限；具体能问多少句，页面没有给出绝对数字。不收费是 standard limits，AI Plus 为 2 倍，AI Pro 为 4 倍，AI Ultra 为 AI Pro 的 5 倍或 20 倍，视订阅而定。精确条数未知。
- Workspace 产品页的常见问题仍写「目前不保留聊天问答历史」。聊天帮助则写聊天记录会保留且只有你自己可见。两篇都在本次打开，说法不一致。使用时以你账号里能否看到历史为准。
- 手机应用的功能比帮助中心里的电脑步骤少，具体少哪些，本批没有把手机功能表逐项核对完。

## 费用与数量限制

不收费方案存在：套餐页写用 Gmail 注册即可。Plus、Pro、Ultra 是 Google AI 的付费升级，也可以走符合条件的 Workspace。本次没有打开 Google AI 的结算价格页，不写月费金额。

下面的个数来自 2026-11-25 打开的 [套餐帮助](https://support.google.com/gemininotebook/answer/16213268) 表格（页面列顺序为：不收费、Plus、Pro、Ultra 20 TB、Ultra 30 TB）：

| 项目 | 不收费 | Plus | Pro | Ultra 20 TB | Ultra 30 TB |
| --- | --- | --- | --- | --- | --- |
| 笔记本 | 100 / 用户 | 200 / 用户 | 500 / 用户 | 500 / 用户 | 500 / 用户 |
| 笔记以外的来源 | 50 / 笔记本 | 100 / 笔记本 | 300 / 笔记本 | 500 / 笔记本 | 600 / 笔记本 |
| 笔记类来源 | 500 / 笔记本 | 500 / 笔记本 | 500 / 笔记本 | 600 / 笔记本 | 600 / 笔记本 |

来源帮助里的「免费用户每个笔记本最多 50 个来源」，与上表「笔记以外的来源 50 个」对应。笔记另计。

## 元数据

- 更新时间：2026-11-25（Asia/Shanghai）
- 来源链接：
  - [notebook.google.com](https://notebook.google.com/)
  - [NotebookLM is now Gemini Notebook（2026-07-16）](https://blog.google/innovation-and-ai/products/gemini-notebook/notebooklm-gemini-notebook/)
  - [Create a notebook](https://support.google.com/gemininotebook/answer/16206563)
  - [Use chat](https://support.google.com/gemininotebook/answer/16179559)
  - [Add or discover sources](https://support.google.com/gemininotebook/answer/16215270)
  - [Plans](https://support.google.com/gemininotebook/answer/16213268)
  - [Usage limits](https://support.google.com/gemininotebook/answer/17670842)
  - [Learn about Gemini Notebook（含国家与地区）](https://support.google.com/gemininotebook/answer/16164461?hl=en)
  - [Workspace 产品页](https://workspace.google.com/products/gemini-notebook/)
- 信息可信度：部分核对。上列官方页在 2026-11-25 打开。笔记本个数和来源个数用帮助页原文表格核对过。`notebooklm.google.com` 本次跳转到 `notebook.google.com`。没有用 Google 账号创建笔记本，没有生成学习指南或 Deep Research 报告，没有核对 Google AI 的月费，没有在手机应用里逐项点功能。云端电脑的套餐范围，博客和现行聊天帮助没有写成同一句话，已在正文并列。
- 平台：电脑浏览器。帮助页没有排除 Windows。手机应用功能可能较少。本批未在 Windows 或手机上操作。
- 技能门槛：会使用 Google 账号并上传文件。不需要编程。
- 费用：有不收费方案（Gmail 注册）。Plus、Pro、Ultra 以及符合条件的 Workspace 为付费升级。月费金额未知。个数限制见正文，来源为 2026-11-25 的套餐帮助。
