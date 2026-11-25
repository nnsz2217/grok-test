# Perplexity Comet

Comet 是 Perplexity 做的浏览器，内核是 Chromium，旁边有一个助手面板。你可以用它查正在看的网页，也可以让它在监督下点击、输入和填写表单，把多步网页操作做完。它和只返回一段答案的搜索聊天不同：官方帮助把「在网页上执行」单独算成 Browser Agent（Comet Assistant）查询。

本批直接打开 `https://www.perplexity.ai/comet` 和 `https://www.perplexity.ai/download-comet` 时，被 Cloudflare 拦住（HTTP 403）。下面能写死的句子，来自同日打开成功的帮助中心原文。产品营销页上如果还有别的口号，本文没有核到。

## 能做什么

已打开的帮助页写明：

- 助手面板贴在浏览器旁边。它可以读取你当前标签页的可见文字、标题和网站信息，也可以用 `@` 指到某个标签。官方示例包括总结这一页、抽出日期和地点、根据这一页起草邮件、总结最近五个标签。这些是帮助中心里的例句，不是本批测出来的成功率。
- 官方「建议与用例」页写它能在监督下点击、输入、提交表单，也能跨多个网站做调研、比较商品、起草或发送邮件。连上 Gmail 和 Google Calendar 之后，可以摘要邮件、起草回复、说明即将到来的会议。同样是厂商示例。
- 用例指南里还有收件箱、会议、购物清单、旅行行程一类例子。帮助页没有给出「从课程大纲生成学习计划」这句原话，本文不把它算成已核对的官方示例。
- 基于 Chromium，帮助中心写明可以安装 Chrome 网上应用店里的大多数扩展。依赖 Chrome 专有集成、或试图改掉默认起始页的扩展，可能不正常。
- 可以从另一个浏览器导入数据。安装页写的入口是 Comet 里的 Profile 或 Settings。

个人版免费方案的对比表里，Browser Agent（Comet Assistant）查询一栏是 No。也就是说，装好浏览器之后，这类「替你操作网页」的用量并不包含在 Free 里。

## 怎么开始

安装帮助的步骤：

1. 打开官方下载页 [perplexity.ai/download-comet](https://www.perplexity.ai/download-comet)。另一篇官方用例页还给出了 [comet.perplexity.ai](https://comet.perplexity.ai/)。本批两个产品页都没有得到正文，下载是否成功要以你自己的浏览器为准。
2. 下载安装包并运行。安装页写：适用于当前系统的安装包，按屏幕提示允许安装程序修改。
3. 打开 Comet，登录 Perplexity 账号并建立配置文件。是否可以完全不登录就浏览，对应帮助页本批没有打开，标为待核实。
4. 如需，从旧浏览器导入书签等数据，再打开助手面板。
5. 不需要编程。你要单独安装这一个浏览器，原来的 Chrome 或 Edge 不会自动变成 Comet。

官方有两篇要求不一致的系统说明，都在 2026-11-25 打开，本文并列，不把其中一篇改写成另一篇：

| 项目 | [安装 Comet](https://www.perplexity.ai/help-center/comet/en/articles/11583748-installing-comet) | [操作系统要求](https://www.perplexity.ai/help-center/comet/en/articles/11734730-operating-system-requirements) |
| --- | --- | --- |
| Windows | Windows 10 或更高 | Windows 10 和 11 的 64 位 x64 与 ARM64。Windows 7、8、8.1 和 32 位不支持 |
| macOS | macOS 11（Big Sur）或更高 | macOS 13（Ventura）或 macOS 14（Sonoma）及更高，Intel 与 Apple 芯片 |
| 内存 | 至少 4 GB，建议 8 GB | 至少 4 GB，建议 8 GB |
| 磁盘 | 500 MB | 安装至少 2 GB，长期使用建议 5–6 GB |
| 其他 | 安装和更新需要稳定网络 | 分辨率至少 1280×800；安装、更新和在线功能需要网络 |

系统要求页还把 Linux、ChromeOS、iOS、Android、Windows 10 以前的版本列为目前不官方支持。与此同时，[Android 快速入门](https://www.perplexity.ai/help-center/comet/en/articles/12875447-comet-for-android-quick-start-and-key-features) 写可以从 Play 商店安装，并写 Android 12 及以上，功能包括语音下任务、摘要和在应用保持打开时自动操作网页。两篇都是官方帮助，结论不一致。本批没有安装桌面版，也没有在手机应用商店搜索，不能判断你的设备上现在哪一篇生效。

Windows 在两篇桌面说明里都出现了。本批没有在 Windows 上安装。

中国大陆：请自己打开上面的官方下载页和帮助中心，用你自己的网络判断。本环境拿到的 403 只说明写作时的这次请求被 Cloudflare 拦住，不能用来判断你是否打得开。

## 能力边界

- 助手可以读取当前页和你点名的标签，也可以在官方描述里代为点击和填表。帮助页同时写明，购物车一类操作可以先给你检查再结账。本批没有测量它实际做对的比例。
- 扩展「大多数可用」是帮助中心的原话，并附有例外。
- 手机版与桌面支持名单互相矛盾，见上表和 Android 文。在矛盾消掉之前，把「官方确认的桌面系统」理解成：两篇里都写了 Windows 10 或更高，以及 macOS；macOS 的最低版本和磁盘空间以你安装时安装程序的实际提示为准。
- 个人版 Pro、Education Pro、Max 的 Browser Agent 次数，官方表只写「每月额度（平均使用）」或「每月额度（更高使用）」，没有给出具体次数。Max 的专文又写 Max 用户拥有各方案里最高的每周浏览器代理额度。周限额和月限额两套说法都在官方页上，本文不合成一个数字。

## 费用

数字来自 2026-11-25 打开的官方帮助中心，不是本批下单。

浏览器安装包本身有没有标价：安装帮助没有写价格。记为未知。

Browser Agent（Comet Assistant）查询，见 [哪一档订阅适合你](https://www.perplexity.ai/help-center/en/articles/11187416-which-perplexity-subscription-plan-is-right-for-you)：

| 方案 | 官方表里的 Browser Agent 查询 |
| --- | --- |
| Free | No |
| Pro | 每月额度（average use），无具体次数 |
| Education Pro | 同上，无具体次数 |
| Max | 每月额度（advanced use），无具体次数。专文另写「最高的每周额度」 |
| Enterprise Pro | 80 次/月 |
| Enterprise Max | 800 次/月 |

同一篇对比文里，和学生有关、且写了金额的还有：Education Pro 为经 SheerID 验证后每月 10 美元。Enterprise Pro 的席位价写的是每席每月 40 美元起，或每年 400 美元起。

[Perplexity Max](https://www.perplexity.ai/help-center/en/articles/11680686-perplexity-max) 写明 Max 为每月 200 美元，或每年 2000 美元；年付只在网页端、且新开 Max 订阅时可选。个人版 Pro 的月费，这篇对比文没有给出金额，记为未知。

## 元数据

- 更新时间：2026-11-25（Asia/Shanghai）
- 来源链接：
  - [Installing Comet](https://www.perplexity.ai/help-center/comet/en/articles/11583748-installing-comet)
  - [Operating System Requirements](https://www.perplexity.ai/help-center/comet/en/articles/11734730-operating-system-requirements)
  - [Assistant Panel](https://www.perplexity.ai/help-center/comet/en/articles/11734688-assistant-panel)
  - [Advice and Use Cases](https://www.perplexity.ai/help-center/comet/en/articles/11732243-advice-and-use-cases)
  - [Use Case Guide](https://www.perplexity.ai/help-center/comet/en/articles/11734483-use-case-guide-ideas-for-comet-use-cases)
  - [Extensions](https://www.perplexity.ai/help-center/comet/en/articles/11734716-extensions)
  - [Comet for Android](https://www.perplexity.ai/help-center/comet/en/articles/12875447-comet-for-android-quick-start-and-key-features)
  - [Which Perplexity Subscription Plan is right for you?](https://www.perplexity.ai/help-center/en/articles/11187416-which-perplexity-subscription-plan-is-right-for-you)
  - [Perplexity Max](https://www.perplexity.ai/help-center/en/articles/11680686-perplexity-max)
  - 产品页与下载页（本次请求返回 403，正文未读到）：[perplexity.ai/comet](https://www.perplexity.ai/comet)、[download-comet](https://www.perplexity.ai/download-comet)
- 信息可信度：部分核对。帮助中心上列文章在 2026-11-25 读到了正文，包括两套互相不一致的系统要求、Android 专文，以及套餐表里的 Browser Agent 额度和上文引用的价格。产品页和下载页本次是 403。没有安装 Comet，没有登录后发起一次 Browser Agent 任务，没有核对个人版 Pro 的月费，也没有核对「不登录能否使用」。
- 平台：帮助中心同时写到桌面 Windows 与 macOS；最低版本和磁盘空间两篇不一致，见正文。Android 有一篇安装说明，系统要求页又把它列为不支持。Linux 在系统要求页列为不支持。本批未安装。
- 技能门槛：会下载并安装一个新浏览器、登录账号。不需要编程。
- 费用：安装包标价未知。Browser Agent 查询在 Free 为 No；Pro、Education Pro、Max 有未写明次数的每月额度；Enterprise Pro 为 80 次/月，Enterprise Max 为 800 次/月。已核对到的金额：Education Pro 每月 10 美元（SheerID）、Max 每月 200 美元或每年 2000 美元、Enterprise Pro 每席每月 40 美元起或每年 400 美元起。个人版 Pro 月费未知。来源与日期见上文。
