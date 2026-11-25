# API 模型选择、官方价格与成本优化

适用产品：OpenAI API，以及需要对照的 ChatGPT 订阅价格。用于在 API 里选对模型、按官方单价控制费用，并弄清订阅套餐和 API 账单的关系。ChatGPT 网页里按思考等级选模型，仍以已有笔记 [Chat、Work 与模型选择](./work-and-model-selection.md) 为准，本篇不改写那一篇。

以下价格和规则均来自 2026-11-25（Asia/Shanghai）核对的官方页面，状态为 Officially Documented。价格会变，使用前须打开原文。本轮没有登录，没有实际扣费，不能标为 Verified。未核对清楚的金额只写未知，不用旧报道或旧博客里的数字冒充现行价。

## 1. 在 API 里按任务难度选模型，而不是默认旗舰

**用途：** 官方模型页的起点建议是：最难的项目用 GPT-6.2 Astra；日常工作用 GPT-6.2 Sol；大量、成本敏感的任务用 GPT-6 Luna。先选对模型，往往比微调一句提示词更能控制费用。

**2026-11-25 官方旗舰系列（标准、短上下文，每百万 tokens，美元）：**

| API 模型 ID | 官方定位（摘要） | 输入 | 输出 | 缓存命中输入 | 30 分钟缓存写入 | 12 小时缓存写入 |
| --- | --- | --- | --- | --- | --- | --- |
| `gpt-6-luna` | 高用量、更省成本的高效模型 | $0.10 | $0.50 | $0.01 | $0.125 | $0.25 |
| `gpt-6.1-terra` | 价目表中的中间档（模型目录页对其介绍不完整，本表以价目为准） | $1.00 | $5.00 | $0.05 | $1.25 | $2.50 |
| `gpt-6.2-sol` / `gpt-6.1-sol` / `gpt-6-sol` | Sol：日常工作和规模化任务的常用档 | $2.00 | $10.00 | $0.10（`gpt-6-sol` 为 $0.20） | $2.50 | $5.00 |
| `gpt-6.2-astra` | 最强旗舰，面向最难的项目 | $8.00 | $40.00 | $0.40 | $10.00 | $20.00 |
| `gpt-6-astra` | 同系列更早的 Astra 档，短上下文标准价更高 | $10.00 | $50.00 | $1.00 | $12.50 | $25.00 |

上表「缓存命中输入」是请求命中已有缓存时的读入价格。「30 分钟 / 12 小时缓存写入」是官方价目中的 cache write 栏目，不是在输入价之外再叠加一笔同样数量的费用：官方 Prompt Caching 文档写明，缓存写入价不是附加费，输入 token 按未缓存输入、缓存命中输入或缓存写入三者之一计价。

其他仍列在价目表上的较旧模型（如 GPT-5.6 系列、GPT-5、GPT-4.1、GPT-4o 等）以当天价目页为准。新项目优先考虑上表的 GPT-6 系列，不要把第三方评测里的旧模型名当成当前默认。

**操作方法：**

1. 试验、短问答、大量重复的分类或改写，先用 `gpt-6-luna`。
2. 日常解题、较长写作、需要更稳的推理，再用 Sol（若你要跟进最新的 Sol，官方当前强调 `gpt-6.2-sol`）。
3. 只有确实很难、可接受高单价时才用 Astra。官方 Quickstart 示例里的 `gpt-6.2-astra` 不应直接当成学生试验的默认值。
4. 价目表把短上下文和长上下文分开。长上下文的输入、输出和缓存价格更高（例如 `gpt-6-luna` 长上下文输入 $0.20、输出 $0.75）。部分较旧模型在表中写明以 272K 为分界；GPT-6 系列请直接查看当天价目表的 Short / Long 列，本篇不自行推定未在行名中写明的分界数字。
5. 官方模型页写明：最新模型普遍支持文本和图像输入、文本输出，并可通过 Responses API 和官方 SDK 使用。具体工具（网页搜索、文件搜索等）是否对某一模型开放，以模型页为准。

**适用场景：** 写自己的调用脚本时选择 `model` 参数；对比“同一个任务用 Luna 还是 Astra”。

**限制：** 本批未做质量评测，不能声称某个更便宜的模型在你的作业上一定够用。知识截止日期、最大输出和上下文窗口以模型页为准（例如官方列出 `gpt-6.2-astra` 上下文 1.05M、最大输出 128K，知识截止 2026-05-18；`gpt-6.2-sol` 知识截止 2026-06-01）。这些规格也会更新。

**来源与可信度：** Officially Documented。[Models](https://developers.openai.com/api/docs/models)、[Pricing](https://developers.openai.com/api/docs/pricing)、[Prompt caching](https://developers.openai.com/api/docs/guides/prompt-caching)。查询日期 2026-11-25。

## 2. 用提示缓存、批量接口或可等待的处理档降低 API 费用

**用途：** 在必须用 API 时，减少重复输入的费用，并把不急的任务放到更便宜的处理方式里。

**操作方法：**

1. **减少请求和 token：** 官方成本优化指南的基本原则是：能少调用就少调用，缩短输入和输出，并优先用更小、足够用的模型。不要每次都把整本讲义加上很长的“请你扮演……”再问一句短问题——若必须带长材料，把固定部分放在最前面并保持不变。
2. **提示缓存（Prompt caching）：** 对受支持模型默认开启。前缀相同的后续请求，可按该模型的缓存命中价计费，官方写明缓存输入最多可优惠至约 95%。要提高命中率：系统说明、工具定义和固定参考材料放在最前面且不要改动；改模型、改工具列表、改推理强度等，都可能让前缀对不上。缓存命中仍计入每分钟 token 限额。官方还写明无法手动清空缓存。查看命中情况可用官方的 Prompt Caching Dashboard 与诊断工具（本轮未登录，界面为 Unverified）。
3. **Batch API：** 把不需要立刻返回的请求写成 `.jsonl`，提交后异步处理。官方写明：相对同步接口有 **50%** 折扣，有单独的排队限额，并且每个批次在 24 小时内完成（常常更快）。单个批次最多 50,000 个请求，输入文件最大 200 MB；每小时最多创建 2,000 个批次。不支持把 `stream=true` 的请求放进批次。适合以后慢慢跑的评测或整理，不适合你正在等答案的作业。
4. **Flex processing：** 在 Chat Completions 或 Responses 请求里设置 `"service_tier": "flex"`，官方写明按 Batch 费率计费，并可叠加提示缓存优惠，但响应更慢，且可能因资源不足返回 429（此时不扣费）。**重要限制（查询当日）：** 官方写明 Flex 正在收尾测试，**不适用于 GPT-6.2 Astra 和 GPT-6.2 Sol，也不会加入后续模型**；退役日期将另行公布。因此不要把它当作新旗舰模型的主要省钱手段。
5. **Responses API 的后台完成窗口：** 官方成本优化与 Flex 文档写明，对可以等待首次回复的工作，2 小时窗口比标准价低 30%，8 小时窗口低 40%；优惠适用于符合条件的请求（含后续请求）。具体参数见官方“completion window”说明。本批不展开工作流代码。

**配置示例（Flex，仅适用于仍支持 Flex 的模型，例如官方示例中的 `gpt-6.1-sol`）：**

```python
from openai import OpenAI

client = OpenAI(timeout=900.0)
response = client.with_options(timeout=900.0).responses.create(
    model="gpt-6.1-sol",
    instructions="请列出并解释这份材料中的三个关键定义。",
    input="<在这里粘贴较长的固定材料>",
    service_tier="flex",
)
print(response.output_text)
```

该示例结构来自官方 Flex 文档，本轮未运行。若模型不受支持，不要强行加 `flex`。

**适用场景：** 同一份讲义连续提问（缓存）；周末才需要的批量摘要（Batch）；仍支持 Flex 的旧一点的模型上的非紧急任务。

**限制：** 省钱方法都改变了等待时间或可用性。不要为了省钱把正在截止的作业丢进 24 小时批次。缓存不改变输出生成方式，相同输入也不保证相同输出。

**来源与可信度：** Officially Documented。[Cost optimization](https://developers.openai.com/api/docs/guides/cost-optimization)、[Prompt caching](https://developers.openai.com/api/docs/guides/prompt-caching)、[Batch API](https://developers.openai.com/api/docs/guides/batch)、[Flex processing](https://developers.openai.com/api/docs/guides/flex-processing)、[Pricing](https://developers.openai.com/api/docs/pricing)。示例未经本轮运行。查询日期 2026-11-25。

## 3. 对照 ChatGPT 套餐价和用量，决定继续用订阅还是另开 API

**用途：** 大多数课程问答在 ChatGPT 产品里完成即可；只有需要程序调用，或订阅额度不够且任务适合按 token 付费时，再为 API 单独付费。

**已在官方帮助中核对的订阅价格（查询日期 2026-11-25，美元，按月）：**

| 套餐 | 官方帮助中写明的月费 | 备注 |
| --- | --- | --- |
| Free | 免费使用（有工具限额） | 日常文本对话官方写明为不限次数，但仍受防滥用限制；上传、绘图、语音、数据分析等另有限额 |
| Go | 现行美元标价：未知（见下） | 低价订阅；帮助中心不列出固定美元数字，要求查看定价页，并写明价格可能随时间调整 |
| Plus | $20 / 月 | 比 Free 有更高限额和更多模型档；帮助中心写明目前不提供年付 |
| Pro 100 | $100 / 月 | 现行 Pro 分三档 |
| Pro 200 | $200 / 月 | 用量高于 Pro 100 |
| Pro 500 | $500 / 月 | 三档中最高的包含用量；含 Ultrafast 等更高能力（细则见 Pro 帮助页） |

**关于 Go 的标价，必须把时间和来源写清：** 2026-01-16 的官方介绍文章写过，美国地区 Go 为每月 8 美元，其他市场可能本地化定价，并指向 chatgpt.com/pricing。那篇文章里把当时的 Pro 只写成 $200 / 月，这已与 2026-11 现行的 Pro 100 / 200 / 500 分档不符，说明套餐结构已经变过。现行 [What is ChatGPT Go?](https://help.openai.com/en/articles/11989085-what-is-chatgpt-go) 只说价格见定价页、可能调整，且均为美元结算、部分国家提供本地货币账单。本轮抓取 [定价页](https://chatgpt.com/pricing/) 时，页面没有给出可稳定复制的现行 Go 美元数字（内容多半由脚本渲染）。因此 **2026-11-25 的现行 Go 标价记为未知**，请以登录后的定价页或结算页为准，不要继续把 2026-01 的 8 美元当成已经核对的现行价。

**用量方面（产品，不是 API）：**

- Free 与 Go：官方写明日常文本对话不限次数；Go 在符合条件的功能上（如图片、上传、数据分析）限额高于 Free。Go 可使用 Think（由 GPT-5.6 Luna 驱动），不包含 GPT-5.6 Sol。
- Plus：帮助中心写明可能有消息上限，尤其在高峰期，具体随系统情况变化。API 仍须另付。
- Work 与 Codex 共用套餐内额度。Plus 在 5 小时窗口内的官方估算（本地消息，不是保证次数）为：GPT-6 Astra 约 5–45 条，GPT-6.1 Sol 约 15–160 条，GPT-6 Sol 约 15–150 条，GPT-6 Luna 约 350–3,000 条。Pro 100 / 200 / 500 当前在 Work / Codex 没有 5 小时窗口上限，但仍有包含用量，可在 Settings → Usage 查看剩余和重置时间。这些数字已出现在官方帮助中，详情和限制见已有的 Work 笔记，本篇不展开 Codex 操作。
- 用尽某一档后，应改用其他可用模型或等待重置；官方写明客服不会重置用量。

**可操作的选择建议（基于官方规则，不是实测对比）：**

1. 只在 ChatGPT 里提问、改稿、用项目和学习模式：优先把钱花在你需要的那一档订阅，而不是另开 API。
2. 已经有订阅，又只是偶尔在自己的脚本里试几句话：先确认订阅是否附带可用的 API credits（若有，规则见定价页脚注）；没有的话，API 会另出账单，试验请用 `gpt-6-luna` 并看 usage。
3. 需要稳定、可预期的按次调用，或要把模型接到订阅无法覆盖的程序：使用 API，并用上一节的缓存 / Batch 控制费用。
4. 不要假设「Plus 的 $20 一定比 API 便宜」或相反：两者计费单位不同，本批没有你的真实用量，不能替你算出哪一种更省。

**适用场景：** 开学时决定要不要升级订阅；开始写脚本前估计 API 会不会另产生一笔可观费用。

**限制：** 定价页上还有 Business、Enterprise、Edu、部分地区广告测试等，本篇面向个人学习，不展开企业合同价。任何未在上方标明来源和查询日期的金额都不要当作现行价。

**来源与可信度：** Officially Documented（已列出的现行 Plus / Pro 价格和用量规则）。Go 的现行美元标价为未知。[What is ChatGPT Plus?](https://help.openai.com/en/articles/6950777-what-is-chatgpt-plus)、[About ChatGPT Pro tiers](https://help.openai.com/en/articles/9793128-about-chatgpt-pro-tiers)、[What is ChatGPT Go?](https://help.openai.com/en/articles/11989085-what-is-chatgpt-go)、[ChatGPT Free Tier FAQ](https://help.openai.com/en/articles/9275245-chatgpt-free-tier-faq)、[Managing usage with GPT-6 Astra in Work and Codex](https://help.openai.com/en/articles/20001516-managing-usage-with-gpt-6-astra-in-work-and-codex)、[Plans and Pricing](https://chatgpt.com/pricing/)、[Introducing ChatGPT Go, now available worldwide](https://openai.com/index/introducing-chatgpt-go/)（2026-01-16，其中部分套餐结构已过时）。查询日期 2026-11-25。

## 元数据

- 更新时间：2026-11-25（Asia/Shanghai）
- 来源：上文各官方开发者文档与帮助中心链接
- 信息可信度：部分核对。API 旗舰单价、缓存 / Batch / Flex 规则，以及 Plus / Pro 帮助中心标价为 Officially Documented。Go 现行美元标价未知。本轮未登录、未扣费，不能当作实测
- 平台：OpenAI API 与 ChatGPT 个人套餐说明。未实测具体账号
- 技能门槛：已阅读 [openai-api-usage.md](./openai-api-usage.md)，能看懂“每百万 tokens 的美元单价”，并会把固定材料放在提示词前部
- 费用：ChatGPT 为免费 / 付费订阅；API 为 API 计费。本文已写入 2026-11-25 核对过的官方数字，使用前须复核原文
