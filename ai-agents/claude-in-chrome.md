# Claude in Chrome

Claude in Chrome 是装在桌面版 Google Chrome 里的扩展。你描述一件要在网页上完成的事，它可以读取当前页面，并在这个浏览器里点击、输入、跳转和填写表单，包括你已经登录的网站。官方把它写成会替你操作浏览器的工具，而不是只在对话框里回答问题。

## 能做什么

帮助中心和 Chrome 网上应用店写明的用法：

- 在 Chrome 侧边栏里对着当前页面工作：总结或对比已经打开的标签，把页面上的信息整理出来，或按步骤走完一个网站上的流程。
- 从 Claude 桌面应用里的聊天、Claude Cowork 或 Claude Code 发起，让 Claude 打开 Chrome 去点击、输入和填表。商店页写明，涉及本机文件和其他电脑上的工具时，使用 Mac 或 Windows 上的 Claude 桌面应用，并保持它开着。
- 官方写它对 Slack、Google Calendar、Gmail、Google Docs 和 GitHub 有现成的操作知识，像「安排会议」「更新文档」这样的短指令可以不用逐步教学。这是厂商说明，本批没有在这些网站上试过。
- 定时任务：按你设定的周期重复做浏览器里的事。
- 录制工作流：你自己做一遍，它记住步骤以后重放。帮助中心写明，这项只在经典侧边栏里可用。侧边栏如果已经是 Cowork 会话，录制不可用，需要从侧边栏菜单切回经典模式。
- 多标签：把标签拖进 Claude 的标签组后一起处理。
- 可以读取浏览器控制台里的报错、网络请求和页面结构，用来查看网页问题。普通填表用不到这一项。

帮助中心写「Claude in Chrome 可用于所有公开模型」。本批没有在扩展里打开模型菜单，不列具体模型名。

## 怎么开始

1. 使用 Claude 的付费方案。帮助中心和商店页都写：Pro、Max、Ultra、Team、Enterprise 可用，免费方案没有这项。Team 和 Enterprise 可以由管理员决定是否开放，Enterprise 还要管理员打开云端 Cowork，否则侧边栏会停在经典体验。
2. 打开电脑上的 Google Chrome。帮助中心和商店页写明：不支持其他 Chromium 浏览器，也不支持手机。
3. 在 [Chrome 网上应用店](https://chromewebstore.google.com/detail/claude/fcoeoabgfenejglbffodgkkbkcdhcgfn) 安装扩展，用 Claude 账号登录，并把图标钉到工具栏。
4. 点图标打开侧边栏，直接说出要它在当前页面做的事。只处理当前标签时，帮助中心写明不必另开软件。任务要用本机文件、本机其他程序，或从别的界面指挥 Chrome 时，需要打开并连上 Claude Desktop。
5. 不需要编程。

权限有三种，在侧边栏或桌面应用的输入框旁切换：

- 手动批准：每一步先问你。
- 自动批准：Cowork 侧边栏的默认。它会检查每个动作，认为不安全就拦住或改问你。你换过模式后，侧边栏会记住选择。
- 全部跳过：不再自动检查动作。官方写明，只在你完全信任这次任务涉及的网站、连接器和文件时使用。

无论哪种模式，下载文件、向网页填入可能敏感的信息、授予授权、永久删除，帮助中心写明仍要你明确同意。购买和金融交易、新建账号、处理银行卡或证件、投资建议和交易、修改系统文件，以及照着邮件或网页内容里夹带的指令行事，属于禁止动作。

Windows 上用桌面版 Chrome 即可安装扩展。要让它同时处理本机文件，再连接 Claude Desktop。本批没有在 Windows 上安装。

中国大陆：需要一个能登录的 Claude 付费账号，并且能打开官方帮助页和 Chrome 网上应用店。本文不判断所在网络是否打得开。

## 能力边界

- 官方说明提示注入仍有残余风险。网页、邮件或表单里可以藏着你看不见的指令，试图让它做你没要求的事。厂商在公开文章里报告了自己的测试结果，并写明防护要持续更新。那些百分比是厂商测试，本批没有复现。涉及付钱、以你的身份发消息或改重要文件时，官方建议留在旁边看，或改回手动批准。
- 商店页在本次打开时显示评分 3.6（页面写作 2K ratings）、用户数 24,000,000、版本 1.0.109、更新日期 2026-11-23。这是商店汇总，不是本批统计。本批没有逐条阅读评论，不转述任何一条评论文字。
- 登录时可以请 1Password 代填。帮助中心写明该功能处于 beta，并且是 macOS。本批没有试用。
- 月费金额本批没有打开 Anthropic 的价格页，不写数字。方案名称以帮助中心列出的 Pro、Max、Ultra、Team、Enterprise 为准。

## 元数据

- 更新时间：2026-11-25（Asia/Shanghai）
- 来源链接：
  - [Get started with Claude in Chrome](https://support.claude.com/en/articles/12012173-get-started-with-claude-in-chrome)
  - [Claude in Chrome permissions guide](https://support.claude.com/en/articles/12902446-claude-in-chrome-permissions-guide)
  - [Claude in Chrome is generally available](https://claude.com/resources/articles/claude-in-chrome-generally-available)
  - [Chrome 网上应用店：Claude](https://chromewebstore.google.com/detail/claude/fcoeoabgfenejglbffodgkkbkcdhcgfn)
- 信息可信度：部分核对。上述四页在 2026-11-25 打开并对照了方案名称、桌面 Chrome 范围、侧边栏与桌面应用的关系、权限模式、禁止动作、录制与定时任务、内置网站名单和提示注入说明。没有安装扩展，没有用付费账号走完一次真实任务，没有逐条阅读商店评论，没有打开 Anthropic 价格页，因此不写月费，也不把厂商安全测试百分比当作本机结果。
- 平台：桌面版 Google Chrome。商店页同时写到 Mac 与 Windows 上的 Claude 桌面应用。官方写明不支持其他 Chromium 浏览器和手机。本批未在 Windows 上安装。
- 技能门槛：会给 Chrome 安装扩展并登录账号。不需要编程。
- 费用：付费。官方列出的方案为 Pro、Max、Ultra、Team、Enterprise；免费方案不可用。具体月费未知。
