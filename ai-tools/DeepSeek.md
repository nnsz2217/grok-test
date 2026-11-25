# DeepSeek

这篇说明怎样进入 DeepSeek、它适合帮大学生做什么，以及官方已经写明的限制。不展开模型原理。API 单价来自 2026-11-25（Asia/Shanghai）核对的官方价目页，并写明查询日期；营销页上不一致的数字已单独标明，不以营销页为准。ChatGPT、Grok、Claude、Codex 的已有笔记不在本篇范围内。

## 入口

- **网页对话：** [chat.deepseek.com](https://chat.deepseek.com)。官方更新日志把网页版与 App 一并称为 DeepSeek App（含网页版），其中的对话能力包括网页搜索、文件输入、网址阅读、语音互动和内容安全审核。
- **官方客户端（手机）：** 官方下载页提供 [iOS 应用](https://apps.apple.com/cn/app/deepseek/id6737597349) 和 [Android 安装包](https://download.deepseek.com/apk/deepseek.apk)。下载页写明：这是官方推出的 AI 助手，可「免费体验与全球领先 AI 模型的互动交流」。这里的「免费体验」是官网原文，不等于官方公布了无上限、永不调整的配额；网页或 App 的具体每日条数，本批未在公开帮助文档中找到，也未登录核实。
- **API 开放平台：** 文档与产品入口指向 [platform.deepseek.com](https://platform.deepseek.com) 和接口地址 `https://api.deepseek.com`（OpenAI 兼容格式）以及 `https://api.deepseek.com/anthropic`（Anthropic 兼容格式）。API 按 token 和部分按次接口计费，与网页/App 的「免费体验」不是同一套账。申请密钥、充值的说明见 [deepseek/api-usage.md](./deepseek/api-usage.md) 和 [deepseek/api-pricing-and-cost.md](./deepseek/api-pricing-and-cost.md)。
- **DeepSeek Harness 桌面端：** 官方下载页将其单独列为桌面端，写明支持后台运行和本地文件读写，便于处理较长时间、较复杂的任务；并提供 [macOS 版](https://download.deepseek.com/desktop/dsh-latest-macos-arm64.dmg)（Apple 芯片、macOS 13 或更高）和 [Windows 版](https://download.deepseek.com/desktop/dsh-latest-windows-x64.exe)。API 文档同时写明 Harness 开发者预览面向全球 Harness 开发者开放测试。本篇只记录入口，不写上手步骤；实测留给本库的 Agent 研究方向。
- **开始方法（网页/App）：** 打开后登录或注册账号，在输入框写出问题或任务即可。官方用户协议写明，可用手机号等方式注册，并提到「联网搜索」：开启后会先检索互联网公开信息，再据此生成内容。2025 年 1 月的 App 介绍还提到过电子邮箱 / Google 帐户 / Apple ID 登录。**没有谷歌帐户时，不要把 Google 登录当作主要路径**；以当前登录页实际提供的方式为准。本轮没有登录，登录页实况见文末访问记录。

## 适合什么任务

对非计算机专业的学生，可以先把网页或官方 App 当作日常学习助手，需要自己写程序或按量付费时再使用 API。

- **日常问答与课程学习：** 解释概念、梳理讲义、把草稿改清楚。简单问题可关闭思考模式，以减少等待；较难的推导再打开思考模式。官方默认思考模式是开启的，思考强度默认为 `high`。
- **需要核对近况或出处的问题：** 使用网页搜索；若同时开启思考，则对应官方所说的「深度思考搜索」：模型可在多步推理中自行搜索、打开页面并在页面中查找。答案仍可能不准确，关键事实要自己对照来源。
- **带着自己的材料提问：** 官方写明 API 的文件解析「与 DeepSeek 网页端上传文件一致」，支持 PDF、Word、PowerPoint 和图片等。问指定页或指定图表时，把要求写清楚，并声明不要编造材料里没有的内容。
- **API 调用：** 适合需要稳定按量使用、或把 DeepSeek 接到已有 OpenAI/Anthropic 兼容软件里的情况。现行推荐模型名是 `deepseek-flash`（当前由 DeepSeek-V4.1-Flash-1017 提供服务，支持图像理解）和 `deepseek-v4-pro`（文本，不支持图像理解）。不要再把已经下线的 `deepseek-chat`、`deepseek-reasoner` 或旧名 `deepseek-v4-flash` 当作当前首选名称。

更细的操作、模型选择、API 示例和官方价格，见 [deepseek/](./deepseek/) 目录，并收入 [advanced-usage-index.md](./advanced-usage-index.md)。那些笔记对照官方文档整理，本轮没有登录产品，也没有实际发出 API 请求，不能当作已经实测成功。

## 限制

- **会说错。** 用户协议提醒：输出可能不准确。作业、引用、数据、日期必须自己对照可靠来源。
- **网页/App 与 API 不是同一套计费。** 下载页对官方客户端使用「免费体验」的表述；API 需在开放平台充值或使用赠金，按官方价目计费。不要把网页能免费问，理解成 API 也可以不花钱。
- **公开文档没有给出网页/App 的固定每日条数。** 高峰时 API 可能返回 503（服务器繁忙）。网页端是否也会排队或拒绝，本轮未登录，不能写成已核实的配额。
- **地区和账号规则以官方协议为准。** 用户协议适用中华人民共和国大陆地区法律。本篇不讨论绕过任何访问限制的方法。
- **功能名称和模型会更新。** 2026-10-17 起，官方网页和 App 使用的模型已更新为 DeepSeek-V4.1-Flash-1017；API 继续用 `deepseek-flash` 调用。旧教程里的 V3、R1、`deepseek-chat`、`deepseek-reasoner` 不能直接当成现行界面或现行 API 名称。
- **本篇不把 Harness 写成已经上手的用法。** 桌面端仍在迭代；需要登录和实跑的内容不在本批范围。

## 本轮访问情况（2026-11-25，Asia/Shanghai）

- **官方文档与产品页：Officially Documented。** 本批核对了官方 API 文档、用户协议、官网首页、下载页和开放平台介绍页。价格以 [模型 & 价格](https://api-docs.deepseek.com/zh-cn/quick_start/pricing/) 为准。
- **此前同日未登录查看（已写入本库 `ai-tools/README.md`，此处只转述，不改原记录）：Unverified。** 2026-11-25，研究环境访问 https://chat.deepseek.com 时，页面重定向到 https://chat.deepseek.com/sign_in，可见手机号/短信、密码、Apple、微信登录选项。当时没有登录，也没有做功能测试。
- **本批补充的未登录请求：Unverified。** 同日稍后，研究环境对 https://chat.deepseek.com、https://chat.deepseek.com/sign_in 和 https://platform.deepseek.com 的 GET 请求返回 HTTP 403。没有登录，也没有做功能测试。这是该环境的访问结果，不是 DeepSeek 的官方声明，也不能据此否定上一则重定向到登录页的观察。不讨论绕过方法。
- **API 调用与网页功能：Unverified。** 本批没有创建密钥，没有发送对话或 API 请求，没有上传文件。

## 元数据

- 更新时间：2026-11-25（Asia/Shanghai）
- 来源：
  - [首次调用 API](https://api-docs.deepseek.com/zh-cn/)
  - [模型 & 价格](https://api-docs.deepseek.com/zh-cn/quick_start/pricing/)
  - [思考模式](https://api-docs.deepseek.com/zh-cn/guides/thinking_mode/)
  - [构建 Chatbot](https://api-docs.deepseek.com/zh-cn/guides/build_a_chatbot/)
  - [联网工具](https://api-docs.deepseek.com/zh-cn/guides/web_tools/)
  - [文件解析](https://api-docs.deepseek.com/zh-cn/guides/document_parsing/)
  - [更新日志](https://api-docs.deepseek.com/updates/)（2026-10-17、2026-11-13 等条目）
  - [DeepSeek 用户协议](https://cdn.deepseek.com/policies/zh-CN/deepseek-terms-of-use.html)（更新日期 2025-09-05）
  - [DeepSeek 官网](https://www.deepseek.com/)、[下载页](https://www.deepseek.com/download/)、[API 开放平台介绍](https://www.deepseek.com/platform/)
  - [Introducing DeepSeek App](https://www.deepseek.com/en/news/deepseek-app/)（2025-01-15，其中的登录方式可能已变化）
  - 本库技巧目录：[deepseek/](./deepseek/)、[advanced-usage-index.md](./advanced-usage-index.md)
  - 2026-11-25 研究环境访问：对 chat.deepseek.com 与 platform.deepseek.com 的未登录 HTTP 请求。不是官方文档。此前同日未登录查看记录见 [README.md](./README.md)。
- 信息可信度：部分核对。对照官方文档的入口、功能和 API 规则为 Officially Documented。2026-11-25 的未登录访问记录为 Unverified。本轮没有登录，没有发送 API 请求，不能当作上手使用或 Verified。开放平台介绍页上的部分标价与官方 API 价目页不一致，已在价格笔记中说明，总览不以介绍页金额为准。
- 平台：已核对官方文档中的网页 chat.deepseek.com、iOS / Android 官方客户端，以及 Harness 桌面端的 Windows / macOS 下载说明。2026-11-25 研究环境对部分网址返回 403 或此前观察到登录页，未做功能测试。未实测具体机型。
- 技能门槛：会用浏览器打开网站、注册或登录账号，并能用中文写出自己的任务。使用 API 需要另外会保存密钥、在 Windows 上设置环境变量，并按官方示例发出请求；见 API 笔记。使用 Harness 的门槛不在本篇展开。
- 费用：网页/App 官方表述为「免费体验」（免费档是否另有未公布限额：未知）。API 为 API 计费。Harness 桌面端在本批公开页未核对手续费，费用未知，不写入金额。
