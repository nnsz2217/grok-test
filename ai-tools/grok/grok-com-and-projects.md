# 使用 grok.com 与 Projects 的文档现状

适用产品：Grok 消费端（grok.com 与官方应用）。先保证进入官方推荐的入口，再谈项目和其他高级功能。以下区分“官方已经写明的事实”和“本轮没有找到完整官方手册的部分”。本轮没有登录实操，不能当作已经实测成功。

## 1. 用 grok.com，并用 Chrome 或基于 Chromium 的浏览器

**用途：** 避免因为进错网址或用了不兼容的浏览器，而看不到 Projects 等功能，误以为产品本身没有这些能力。

**操作方法：**

1. 在电脑上打开 [grok.com](https://grok.com)。官方 FAQ 明确建议使用常规的 Chrome 或基于 Chromium 的浏览器（例如 Edge）。
2. 官方写明：部分用户在 grok.x.ai 或其他地址会碰到功能缺失，举例就包括 Projects。
3. Windows 没有单独列出的官方消费端桌面应用，请用浏览器打开 grok.com。手机请使用官方 iOS 或 Android 应用；登录一次后，对话、设置和订阅会在网页与应用之间同步。
4. 请始终使用同一个登录方式，避免误以为付了两次费。登录可用 X 账号或邮箱等，不是必须使用谷歌帐户。

**适用场景：** 第一次在电脑上使用 Grok，或发现别人截图里有 Projects 而自己看不到。

**限制：** 这是入口建议，不是对 Projects 本身的逐步教程。本轮未登录，不能核实某一浏览器里实际出现的菜单，属 Unverified。

**来源与可信度：** Officially Documented。[FAQ - Grok Website / Apps](https://docs.x.ai/grok/faq)、[Welcome to Grok](https://docs.x.ai/grok/overview)。查询日期 2026-11-25。

## 2. Projects 官方确认存在，但消费端缺少完整操作手册

**用途：** 如实记录目前能核对到的信息，避免把第三方教程写成官方步骤。

**截至 2026-11-25，能够对照官方材料核对的事实：**

- 官方 FAQ 把 Projects 列为在错误网址或非推荐浏览器上可能缺失的功能，说明消费端产品包含 Projects。状态：Officially Documented。
- 商业与企业文档把 projects 和 skills、conversations 并列为一类可管理分享范围的资源；默认情况下对话和项目可以在组织范围内分享，技能默认从 Private 开始；公开链接只适用于对话，项目和技能最高到 Organization。这是团队工作区的分享策略，不是个人免费帐户的操作说明。状态：Officially Documented（限于 Business / Enterprise 管理说明）。
- 存在产品地址 https://grok.com/project 。本轮未登录，页面内容未完整核对手册级说明，不能据此写出逐步点击路径。状态：Unverified（页面细节）。

**本轮没有在 docs.x.ai 的消费端文档中找到**与 ChatGPT「Projects in ChatGPT」相当的、关于如何创建项目、如何写项目说明、项目文件如何计入上下文、以及个人帐户分享规则的完整手册。因此，本篇**不编写未核对的点击步骤**，也不把第三方博客中的操作写成现行官方方法。

若你在已登录的 grok.com 侧边栏里看到 Projects，可以自行尝试：新建项目、放入相关文件、在项目里开始对话。这些界面观察若未对照官方手册，应记为 Unverified，直到官方补上文档或完成一次有记录的实测。

**适用场景：** 想把一门课的资料长期放在一起时，先确认自己走的是 grok.com 和推荐浏览器；具体怎么设置项目，以产品内说明为准，并保留“文档尚未写清”的预期。

**限制：** 不要用过时的或未标明来源的“Grok Projects 教程”代替官方说明。也不要把 Grok Build / 编程代理里的 `AGENTS.md` 项目规则，直接写成 grok.com 聊天项目的设置方法——那是另一套产品文档。

**来源与可信度：** 入口与分享策略为 Officially Documented，见 [FAQ - Grok Website / Apps](https://docs.x.ai/grok/faq)、[License & User Management](https://docs.x.ai/grok/management)。完整消费端操作手册：本轮未找到，相关逐步用法为 Unverified。查询日期 2026-11-25。

## 元数据

- 更新时间：2026-11-25（Asia/Shanghai）
- 来源：
  - [FAQ - Grok Website / Apps](https://docs.x.ai/grok/faq)
  - [Welcome to Grok](https://docs.x.ai/grok/overview)
  - [License & User Management](https://docs.x.ai/grok/management)
  - 产品地址 https://grok.com/project（未登录，未作为操作手册使用）
- 信息可信度：部分核对。推荐网址与浏览器、以及团队分享策略为 Officially Documented。个人 Projects 的逐步操作为 Unverified，因缺少对照用的官方手册。本轮未登录
- 平台：已核对官方文档中的 grok.com（建议 Chrome / Chromium）和官方移动应用。Windows 仅核对“用浏览器访问网页”。未实测具体机型
- 技能门槛：会用浏览器打开指定网址并登录。不需要编程
- 费用：免费 / 付费。未核对手表价，也不把团队分享策略写成个人免费功能的承诺
