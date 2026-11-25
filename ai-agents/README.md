# AI Agent

收录可以拿来就用的实用 Agent，看重实际价值。范围是浏览器、桌面、搜索、文档和个人效率。

这里记「用哪一个、解决什么具体事、怎样开始」。复杂的多 Agent 架构不放在本目录。Skill 的写法放在 [skills/](../skills/)，把 Agent 嵌进固定流程时放在 [automation/](../automation/)。

## 当前内容

第一批写了四篇。都是对照官方页面整理的使用说明，没有亲手把产品装完并跑通任务。价格和额度以各篇自己的来源和日期为准，本页不重复金额。

- [Claude in Chrome](claude-in-chrome.md)

  桌面版 Chrome 里的浏览器代理。付费 Claude 账号安装扩展后，它可以在你已经登录的网页上阅读、点击、输入和填表。免费方案不可用。

- [Perplexity Comet](perplexity-comet.md)

  Perplexity 的 Chromium 浏览器，带侧边助手，官方把「替你操作网页」计为 Browser Agent 查询。帮助中心对系统要求和手机版的说法不一致，笔记里并列了原文。

- [Gemini Notebook](gemini-notebook.md)

  原 NotebookLM。把 PDF、文档、网页或视频放进笔记本后，针对这些材料提问，并生成学习指南、测验、音频和幻灯片。有不收费的 Gmail 注册方式。

- [AutoClaw（澳龙）](autoclaw.md)

  智谱的桌面智能体，有中文官网和中文文档。装到自己的电脑上处理文件和浏览器任务，调用模型需要联网。Windows 10 及以上在官方下载页中。

## 本批评估但未收录

- Manus（[manus.im](https://manus.im)，官方快速开始仍在 [quickstart](https://manus.im/docs/introduction/quickstart)，该页描述网页、以及 macOS / Windows 的 Studio）。本次打开的快速开始没有停服声明。中文媒体另有报道：澎湃转载的《IT时报》写「1 月 4 日晚，Manus 宣布 1 月 5 日起停止对中国境内用户服务」（[报道](https://www.thepaper.cn/newsDetail_forward_32401072)）；《21 世纪经济报道》写 Meta 发言人称公司将终止中国服务和运营，并写记者在 2026-01-08 检索时已不对国内用户开放（[报道](https://www.21jingji.com/article/20260108/herald/c141d33622ba04e3d2d6177867dde0e7.html)）。这些是二次来源，不是本批找到的 Manus 官方公告页。信息可信度：部分核对。面向希望在中国大陆直接试用的读者，本批不为它单开笔记。

## 以后怎么加笔记

1. 一个可独立使用的 Agent（或同一类里的一组，且来源已经核对）写成一篇。已有笔记覆盖的对象，更新原文件。
2. 文末按 [笔记约定](../resources/conventions.md) 写来源链接、更新时间（Asia/Shanghai）、信息可信度。适用时写平台、技能门槛和费用；费用未知就写未知。
3. 笔记里写明它实际替你完成的那件事。只讲编排原理、没有可执行入口的材料不放进来。
4. 回到本页「当前内容」，加上相对链接和一两句这篇覆盖什么，并更新本页的更新时间。
5. 通过 Pull Request 合并，不要直接推送到 `main`。

## 以后可能补的主题（尚未检索、尚未核实）

本批已经写过的场景改成勾选，只表示「有一篇笔记」，不表示能力已经实测。未勾选的仍是空位，没有链接，也不能当资料用。

- [x] 浏览器里能直接用的 Agent（本批：Claude in Chrome、Perplexity Comet）
- [x] 处理文档和学习材料的 Agent（本批：Gemini Notebook）
- [x] 有中文官网的桌面 Agent（本批：AutoClaw / 澳龙；它同时会操作浏览器）
- [ ] 其他只装在桌面、本批还没写的 Agent
- [ ] 专门处理个人邮件、日程或待办的 Agent（本批只在浏览器类笔记里提到官方举例，没有单独成篇）
- [ ] 只做搜索、不附带浏览器操作的 Agent

## 元数据

- 更新时间：2026-11-25（Asia/Shanghai）
- 来源链接：本目录四篇笔记及其文末来源；Manus 未收录说明来自 [官方快速开始](https://manus.im/docs/introduction/quickstart)、[澎湃转载的《IT时报》](https://www.thepaper.cn/newsDetail_forward_32401072)、[21 世纪经济报道](https://www.21jingji.com/article/20260108/herald/c141d33622ba04e3d2d6177867dde0e7.html)。分类范围来自本目录既有索引。
- 信息可信度：部分核对。本页是索引，产品事实以各篇笔记为准。四篇都没有做端到端实测。Manus 的停服说法来自媒体报道，快速开始页本身没有这句话。本页不写价格。
- 平台：不适用（见各篇）
- 技能门槛：不适用（见各篇）
- 费用：不适用（索引页不写价格；未知项留在各篇）
