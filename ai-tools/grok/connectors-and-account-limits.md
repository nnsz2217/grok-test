# 连接器与谷歌帐户限制

适用产品：Grok 消费端的 Connectors（连接器）。让 Grok 在对话里读取你已授权的邮箱、云盘、日历等，而不必把内容先下载再上传。以下为官方文档说明，状态为 Officially Documented。本轮没有登录授权，不能当作已经实测成功。

**没有谷歌帐户的读者请先看这一段：** 连接 Gmail、Google Calendar 或 Google Drive **必须有谷歌帐户**。没有谷歌帐户时，不要把这些连接当成必做步骤。可以用邮箱登录 Grok 本身，并考虑官方列出的非 Google 连接，例如 Outlook 邮箱和日历、OneDrive、Microsoft Teams、SharePoint，或目录中的 Notion、GitHub 等（仍需你拥有对应服务的帐户）。

## 1. 只连接当前任务真正需要的服务

**用途：** 在提问“这周有哪些截止日期”或“云盘里那份大纲怎么改”时，让 Grok 直接查找已授权的来源。

**操作方法：**

1. 打开 [grok.com/connectors](https://grok.com/connectors)。官方写明连接器对所有 Grok 用户提供。若你使用 Grok Business 或 Enterprise，需要先由团队管理员在云控制台开通，成员才能使用。
2. 选择 **New Connector**，再选要连接的服务，完成 OAuth 登录。官方写明内置连接器由 xAI 维护，完成一次登录后即可按需访问，只需授予其声明需要的权限。
3. 官方列出的内置连接器包括：Gmail 与 Google Calendar、Google Drive、OneDrive、Outlook 邮件与日历、Microsoft Teams、SharePoint、Salesforce。
4. 另外还有预配置的目录连接器，官方举例包括 Box、Canva、Gamma、GitHub、Linear、Meltwater（需有效 Meltwater 订阅）、Notion、S&P Global、Vercel。完整目录以 grok.com/connectors 为准。
5. 连接完成后，官方写明：当问题与该服务相关时，Grok 可以自动使用相应工具。

**可复制的提示词示例：**

```text
请只在我已连接的 Outlook 日历和邮箱里查找：未来 14 天与课程、作业或考试有关的事项。
列成表：日期、事项、你依据的是日历还是某封邮件的主题。
不要打开或引用与课程无关的私人邮件。如果找不到，就说没找到，不要补造日程。
```

若你有谷歌帐户并已连接 Gmail / Google Calendar，可以把上面的 Outlook 换成对应的 Google 服务。没有谷歌帐户时，保持使用 Outlook 或其他非 Google 连接。

**适用场景：** 把已有的云盘资料或邮箱通知纳入一次复习计划；在不下载全部附件的前提下询问某份已授权文件。

**限制：**

- 连接器会访问你授权范围内的数据，只应连接当前需要、并且你信任的服务。用完高敏感权限后，可在该服务或 Grok 的连接设置里检查是否需要断开。本轮未核对手动断开的逐步界面，属 Unverified。
- 目录会变化，某一连接是否对你的地区或方案开放，以登录后的页面为准。
- 自定义 MCP 连接器面向需要自行提供 Model Context Protocol 服务器的高级用户：服务器必须能从公网访问，本机服务还需要隧道。这超出本库主要读者的日常范围，不应作为普通技巧来试用，也需要理解你在向 Grok 暴露哪些接口。本篇只记录官方提供这一选项，不写搭建步骤。

**来源与可信度：** Officially Documented。[Connectors](https://docs.x.ai/grok/connectors)。查询日期 2026-11-25。本轮未登录完成授权，实际自动调用效果为 Unverified。

## 元数据

- 更新时间：2026-11-25（Asia/Shanghai）
- 来源：[Connectors](https://docs.x.ai/grok/connectors)
- 信息可信度：部分核对。连接器种类、入口和对所有 Grok 用户开放的说明为 Officially Documented。授权后的实际调用和断开流程未实测，为 Unverified。未核对手表价
- 平台：官方文档以 grok.com/connectors 为主。未单独核对手动应用里的同等入口。未实测
- 技能门槛：会完成一次标准的第三方登录授权，并理解授权范围。不需要编程即可使用内置和目录连接器。自定义 MCP 需要额外的技术能力，本篇不作为入门步骤
- 费用：免费 / 付费。官方写明连接器对所有 Grok 用户提供，但团队帐户需管理员先开通；未核对手表价。部分目录连接器还要求你在对方服务上另有订阅（官方举了 Meltwater）
