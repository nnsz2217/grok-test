# AI 工具

收录具体工具的高级用法。计划覆盖的工具包括 ChatGPT、Codex、Grok、DeepSeek、Claude、Gemini；以后若核对过其他工具，也放在这里。

一篇笔记讲清一个工具里已经核对过的用法：入口在哪、适合什么任务、和本库其他笔记怎么接。不在这里展开模型结构，也不把未核对的价格和套餐写进来。新功能的短讯可以先记在 [ai-frontier/](../ai-frontier/)，用法稳定后再写成工具笔记。

## 当前内容

- [ChatGPT](./ChatGPT.md)：对照官方文档整理网页、手机和 Windows 入口，适合大学生的对话 / Work / 项目用法，以及地区、用量和准确性方面的限制。未写 Codex，也未核价格。「本轮访问情况（2026-11-25，Asia/Shanghai）」记录研究环境请求 https://chatgpt.com 返回 HTTP 403（未登录、未做功能测试，Unverified）；官方支持地区名单仍为 Officially Documented。Codex 本轮未做上手测试（Unverified）。
- [Claude](./Claude.md)：对照官方文档整理 claude.ai、桌面应用和手机入口，适合带资料提问和用项目做课程工作区的用法，以及年龄、地区、共用额度等限制。未写 Claude Code 操作步骤，也未核价格。同日访问记录：打开 https://claude.ai 返回 HTTP 200，并重定向到 https://claude.com/app-unavailable-in-region#_（未登录、未做功能测试，Unverified）；官方支持地点名单仍为 Officially Documented。
- [Grok](./Grok.md)：对照官方文档整理 grok.com 与 iOS / Android 入口，适合对话、上传材料和生成内容的用法，以及用量、水印和地区说明不完整等限制。以 grok.com / 官方应用为准，未评测 Grok Bot，也未核价格。官方写明的文件上传仍是 Officially Documented 的产品说明，不是已完成的上手测试。同日未登录访问中，附件控件没有打开文件选择器，文件上传问答未完成（Unverified）。

## 以后怎么加笔记

1. 一个工具一篇，文件名用工具的常用英文名。同一工具的新用法合并进已有文件，不另开平行笔记。
2. 文末按 [笔记约定](../resources/conventions.md) 写来源链接、更新时间（Asia/Shanghai）、信息可信度。适用时写平台、技能门槛，以及免费 / 付费 / API 费用；费用未知就写未知。
3. 回到本页「当前内容」，加上相对链接和一两句这篇覆盖什么，并更新本页的更新时间。
4. 通过 Pull Request 合并，不要直接推送到 `main`。

## 以后可能补的主题（尚未检索、尚未核实）

下面只是预定的笔记位置。没有链接，没有结论，不能当资料用。

Gemini 和 DeepSeek 仍没有单独笔记。2026-11-25 只做了未登录查看，没有上传文件，登录测试按要求没有继续，状态为 Unverified：https://gemini.google.com/app 有输入区，但 Upload files、Add from Drive、More uploads 为禁用，并显示 “Sign in to try tools”；https://chat.deepseek.com 重定向到 https://chat.deepseek.com/sign_in（手机号/短信、密码、Apple、微信）。本批不新建 Gemini.md 或 DeepSeek.md。

- [ ] Codex 的高级用法
- [ ] DeepSeek 的高级用法
- [ ] Gemini 的高级用法

## 元数据

- 更新时间：2026-11-25（Asia/Shanghai）
- 来源：本目录当前文件清单；ChatGPT、Claude、Grok 三篇的官方文档来源与 2026-11-25 访问记录见各篇文末。Gemini、DeepSeek 没有单独笔记；本页只记录同日未登录查看 https://gemini.google.com/app 与 https://chat.deepseek.com 的结果。其余工具名单仍来自知识库结构规划
- 信息可信度：部分核对。本页作为索引已与当前文件清单对齐。三篇笔记中对照官方文档的内容为 Officially Documented；2026-11-25 新增的地区访问和未登录入口观察为 Unverified，文件上传没有完成，不能当作已经完成的上手使用。Codex、DeepSeek、Gemini 仍在「尚未检索、尚未核实」清单中；其中 Gemini 与 DeepSeek 只在本页多记了未登录访问状态，没有新建笔记
