# 自动化

收录可复用的 AI 自动化工作流：触发条件、步骤、用到的工具或 Skill、怎样算做完。目标是下次遇到同类任务时按笔记重做，而不是重想一遍。

单条提示词的写法放在 [prompt-engineering/](../prompt-engineering/)。某个工具的界面与设置放在 [ai-tools/](../ai-tools/)。这里保留把它们串起来的那条流程。

## 当前内容

- [用 Power Automate 桌面版自动归档课程资料](course-material-auto-filing.md)：在 Windows 上用 Power Automate 桌面版，按扩展名和文件名中的课程关键词，把投放文件夹（如「下载」）里的 PDF、PowerPoint、Word 文件移到对应课程文件夹。个人 Microsoft 帐户可在本地手动或按计划运行；不能当作「文件一出现就由云端立即触发」。
- [用 Google 快讯邮件跟踪课程、奖学金或论文更新](topic-update-monitoring.md)：只使用官方 Google 快讯页面创建邮件提醒，在 Google 搜索出现匹配的新结果时向邮箱发信。主路径不含 RSS；怎样算订阅到位见该篇完成标准。

## 以后怎么加笔记

1. 一条可以复用的流程一篇。同一流程的修订合并进已有文件。
2. 文末按 [笔记约定](../resources/conventions.md) 写来源链接、更新时间（Asia/Shanghai）、信息可信度。适用时写平台、技能门槛和费用；费用未知就写未知。
3. 步骤只写已经亲自核对或有来源支撑的部分。缺来源的步骤标成待核实，或先不写。
4. 回到本页「当前内容」，加上相对链接和一两句这条流程解决什么，并更新本页的更新时间。
5. 通过 Pull Request 合并，不要直接推送到 `main`。

## 以后可能补的主题（尚未检索、尚未核实）

下面只是按本目录的收录范围留下的空位。没有链接，没有结论，不能当资料用。

- [ ] 把已有 Skill 或提示词嵌进一条流程的写法
- [ ] 工作流失败时怎么检查（以已核对的流程为限）
- [ ] 其它可复用的个人工作流（仍须单独检索并按约定写来源）

## 元数据

- 更新时间：2026-11-25（Asia/Shanghai）
- 来源：本目录当前文件清单（本索引及下列主题笔记）；分类范围来自本次知识库结构规划；笔记格式见 [笔记约定](../resources/conventions.md)
  - [course-material-auto-filing.md](course-material-auto-filing.md)
  - [topic-update-monitoring.md](topic-update-monitoring.md)
- 信息可信度：索引结构已按当前文件清单核对；两篇主题笔记均为部分核对（对照官方文档起草，未在 Windows 或真实 Google 帐户上实跑），细节以各篇元数据为准。
- 平台：不适用（本页是索引）
- 技能门槛：会改一个 Markdown 文件并提交 Pull Request
- 费用：不适用（本页是索引，不写具体产品价格）
