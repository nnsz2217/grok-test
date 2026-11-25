# 插件、自定义 GPT 过渡与定时任务

适用产品：ChatGPT（以及部分与 Codex 共用的插件目录）。用于把可重复的说明和工具组合起来，或让 ChatGPT 在指定时间或事件后自动做一件事。以下为官方说明，状态为 Officially Documented。本轮没有登录实操，不能当作已经实测成功。

## 1. 自定义 GPT 即将退役：个人用途优先改用项目，可复用工作流改看插件

**用途：** 避免继续把“自建 GPT”当成长期方案；在退役前把常用的说明和资料迁到仍然得到支持的方式。

**官方在 2026-11-25 查询时写明的时间表和限制：**

- 自定义 GPT 计划于 **2026-12-11** 退役。FedRAMP 工作区，以及获得合格、已批准延期的 Enterprise 工作区，退役日期为 2027-02-28；这一较晚日期并不适用于所有工作区，以帐户或工作区通知为准。
- **个人 ChatGPT 帐户（包括 Free、Go、Plus 和 Pro）不能新建或发布 GPT。** 已有 GPT 在退役前仍可使用；编辑仍取决于原方案和权限。
- 受影响的 Enterprise 工作区已在 2026-10-26 停止新建 GPT（FedRAMP 工作区除外）。迁移后，原来的 GPT 变为只读，但在退役前仍可使用。
- 官方建议：若你主要是为了把说明和参考资料放在一起做长期任务，可以改用 **Projects（项目）**。若需要可安装、可分享、能搭配连接应用的可复用工作流，则改用 **Plugins（插件）**。新的可复用工作流应通过 Plugin Creator 创建，而不是再新建 GPT。
- 迁移可用时，创建者可把已发布的说明转为技能，并复制知识文件、带上已连接的应用；**自定义 actions 不会自动迁移**，需要另行重建和测试。公开分享不是迁移的前提。请以产品内通知和 [Custom GPT retirement and migration FAQ](https://help.openai.com/en/articles/20001519-custom-gpt-retirement-and-migration-faq) 为准。

**在退役前若仍使用已有 GPT，官方还写明：**

- GPT 不使用已保存记忆、自定义指令或以往对话，每次都是新的开始。
- 在网页对话中输入 `@` 可以把一个 GPT 拉进当前对话，而不必新开聊天；移动应用没有这一 @ 提及方式，需从 GPT 菜单或侧边栏打开。
- 若第一条消息就使用自定义 GPT，对话会作为与该 GPT 的聊天开始，并出现在项目之外。已有的项目对话里则可以使用自定义 GPT。

**适用场景：** 过去靠自建 GPT 保存课程要求的个人用户，把同样的说明和文件放进一个项目；需要安装别人做好的工具组合时，改为浏览插件目录。

**限制：** 过渡安排会影响所有 ChatGPT 方案，但迁移和插件权限因帐户或工作区而异。不要把第三方教程里“现在就去创建一个 GPT”当作 2026-11-25 之后的现行步骤。本轮未登录，无法核对迁移按钮是否已对某一帐户出现，属 Unverified。

**来源与可信度：** Officially Documented。[GPTs in ChatGPT](https://help.openai.com/en/articles/8554407-gpts-in-chatgpt)、[Creating and editing GPTs](https://help.openai.com/en/articles/8554397-creating-and-editing-gpts)、[Custom GPT retirement and migration FAQ](https://help.openai.com/en/articles/20001519-custom-gpt-retirement-and-migration-faq)、[Projects in ChatGPT](https://help.openai.com/en/articles/10169521-projects-in-chatgpt)。查询日期 2026-11-25。

## 2. 用插件安装可复用的技能和连接，而不是把长提示词每次粘贴一遍

**用途：** 把“说明 + 参考资料 + 可选的外部应用”打包，在相关提问时自动或按 @ 使用。

**操作方法：**

1. 在网页、桌面或手机的侧边栏打开 **Plugins**，按方案和工作区浏览可用插件。先读它包含的技能、应用和设置要求。标为 Desktop only 的插件需要桌面应用，不能在网页上运行。
2. 选择 Install plugin；若插件需要连接外部帐户，再完成授权。安装不会绕过该服务或工作区的权限。
3. ChatGPT 可在相关请求中自动使用已安装插件，也可用 `@` 提及、在 + 菜单里输入名称，或在输入框的 Plugins 中选择。
4. 在受支持的 Codex 任务视图中，可通过 Sources → Use plugins 选择已安装插件。
5. 部分插件带有 OpenAI Verified 标记，表示经过质量与可靠性方面的审核；这不能替代你或所在机构自己的隐私和安全评估。

**适用场景：** 需要连接日历、邮箱或团队工具来完成一项重复任务；希望把一套固定步骤做成可安装的工作流。

**限制：**

- 插件目录对各 ChatGPT 方案开放，但能否安装或使用某一插件，取决于方案、工作区、角色、地区及其包含的能力。
- 官方写明：Personal Skills（个人技能）一般面向 ChatGPT Business、Enterprise、Healthcare 和 Edu 用户，还取决于工作区设置、角色和产品界面。不要假定个人免费或 Plus 帐户一定能创建与工作区用户相同的个人技能。
- 连接 Gmail 或 Google Drive 等应用需要相应帐户。**这些 Google 应用需要谷歌帐户。** 没有谷歌帐户时，可寻找不依赖 Google 的插件，或只使用不含应用连接的技能型插件。
- 禁用某个应用不一定会卸载插件，也不一定关掉其中可独立使用的技能。
- 与 GPT 一样，通过应用发给第三方的数据按对方政策处理。

**来源与可信度：** Officially Documented。[Plugins in ChatGPT](https://help.openai.com/en/articles/20001256-plugins-in-chatgpt)。查询日期 2026-11-25。本轮未浏览插件目录实况，属 Unverified。

## 3. 用定时任务做提醒和监控，但不要指望它自动读取项目文件

**用途：** 在指定时间或特定事件后，让 ChatGPT 检查更新、发送提醒或重复完成一项已说清的任务。

**操作方法：**

1. 打开 Scheduled 页面创建任务并设置时间表；也可直接对 ChatGPT 说出要做的事，例如官方示例：“包裹送达时告诉我。”
2. 也可从 Settings → Notifications 进入 Manage tasks。在对话的更多选项（•••）里可查看已安排的任务。
3. 通知可在 Settings → Notifications 中选择推送、邮件或两者。要在手机上收推送，需在受支持的手机应用中创建任务并允许通知。
4. 可在任务面板中编辑、暂停或删除。免费用户最多把一次性或重复任务安排为每天一次，并使用较宽松的时间窗口（如上午、下午、晚上）；按小时或精确到点的时间需要符合条件的付费方案。
5. 事件触发任务在 Work 中运行，可响应受支持的 Gmail、Slack 或 GitHub 活动，面向符合条件的 Plus、Pro、Business、Enterprise、Edu 及部分 Healthcare 工作区；Free 和 Go 不能创建，FedRAMP 工作区也不可用。Gmail 相关任务**需要谷歌帐户**。没有谷歌帐户时，可考虑 Slack、GitHub 或其他不依赖 Google 的提醒方式，或只用按时间运行的任务。
6. 符合条件的任务可以通过链接分享一份快照（标题、说明、时间表和原时区等），不含你的聊天记录、记忆、附件或应用凭证。不要在标题或说明里写密码、账号或其他敏感信息。

**适用场景：** 每天提醒自己复习一章；监控某一公开页面是否更新；在付费方案下，用 Gmail 或 Slack 事件触发后续整理（需相应帐户）。

**限制：**

- 同时进行的任务数量因方案而异。官方写明：Free 和 Go 为 3 个，Plus 为 5 个，Business 和 Edu 为 10 个，Pro 和 Enterprise 为 15 个。查询日期 2026-11-25，以后可能调整。
- **在项目中创建的任务不能访问该项目已上传或存放的文件。**
- 定时任务不支持语音聊天、GPT 和已锁定的对话。锁定对话前，应先删除与之相关的任务（包括已暂停的）。
- 即使某次运行没有发出更新，完成后的 Chat 定时任务仍可能占用方案用量，因为它会在后台做模型处理。不再需要的任务应及时暂停或降低频率。
- 删除与任务相关的对话只会暂停任务，不会删除已分享的任务链接；删除任务也不会删除那条对话。
- 桌面应用是否显示 Scheduled 取决于应用和版本；若没有，请用网页。桌面应用可以显示已有的事件触发任务，但不能创建或编辑其触发条件。Codex 另有单独的 automations，与这里的定时任务不是同一套。

**来源与可信度：** Officially Documented。[Scheduled tasks in ChatGPT](https://help.openai.com/en/articles/10291617-scheduled-tasks-in-chatgpt)。查询日期 2026-11-25。本轮未创建任务，属 Unverified。

## 元数据

- 更新时间：2026-11-25（Asia/Shanghai）
- 来源：
  - [GPTs in ChatGPT](https://help.openai.com/en/articles/8554407-gpts-in-chatgpt)
  - [Creating and editing GPTs](https://help.openai.com/en/articles/8554397-creating-and-editing-gpts)
  - [Custom GPT retirement and migration FAQ](https://help.openai.com/en/articles/20001519-custom-gpt-retirement-and-migration-faq)
  - [Plugins in ChatGPT](https://help.openai.com/en/articles/20001256-plugins-in-chatgpt)
  - [Projects in ChatGPT](https://help.openai.com/en/articles/10169521-projects-in-chatgpt)
  - [Scheduled tasks in ChatGPT](https://help.openai.com/en/articles/10291617-scheduled-tasks-in-chatgpt)
- 信息可信度：部分核对。退役时间表、个人帐户不能新建 GPT、插件与定时任务规则为 Officially Documented。本轮未登录查看迁移入口、插件目录或 Scheduled 页面，属 Unverified。未核对手表价
- 平台：插件目录可用于网页、桌面和手机，但部分插件仅桌面可用。定时任务建议以网页为主；精确行为因应用版本而异。未实测
- 技能门槛：会安装一个插件或创建一个提醒。连接第三方应用时需要相应帐户。不需要编程即可使用官方目录中的常见插件；创建带自定义接口的复杂插件则超出本篇范围
- 费用：免费 / 付费。插件和定时任务的可用性、同时任务数量和精确日程因方案而异；未核对手表价，故不写入金额
