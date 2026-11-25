# OpenAI API 用法（与 ChatGPT 网页的区别）

适用产品：OpenAI API（开发者平台），不是 ChatGPT 网页或 App 里的同一个开关。用于理解「订阅 ChatGPT」和「调用 API」的差别，并按官方步骤准备密钥、发出第一次请求。以下为官方说明，状态为 Officially Documented。本轮没有登录平台，也没有实际发出 API 请求，不能当作已经调通或 Verified。

本篇补的是现有 [Chat、Work 与模型选择](./work-and-model-selection.md) 没有展开的 **API 侧** 用法。ChatGPT 界面里的 Instant / Medium / High、Work 和 Codex 仍以那一篇为准，这里不重复。本篇也不写用 API 去做信息收集、批量处理文件或自动生成文档的工作流。

## 1. 先分清 ChatGPT 订阅和 OpenAI API：不是同一笔费用

**用途：** 避免以为开通了 Plus 就可以免费调用 API，或反过来以为付了 API 账单就等于升级了 ChatGPT。

**官方区分：**

- **ChatGPT（chatgpt.com 与官方应用）：** 按套餐使用对话、项目、学习模式、深度研究、Work 等产品功能。Free 可使用日常文本对话（另有上传、绘图等工具的单独限额）；Go、Plus、Pro 是付费订阅。官方帮助多次写明：**API 用量不包括在这些订阅里，需单独按 API 价格计费。**
- **OpenAI API（开发者平台）：** 用密钥按 token（以及部分工具的按次费用）调用模型。适合自己写的程序，或官方 SDK / 兼容工具。它没有 ChatGPT 里现成的项目说明、学习模式按钮或 Work 画布，那些能力要在产品里使用，或自行在程序中实现。
- **Pro 套餐中的“每月 API 额度”：** 官方定价页提到部分 Pro 方案可能包含每月 API credits，并注明需满足开通和资格要求，首笔按比例发放，未使用额度在计费周期结束时过期，且该权益可能调整或取消。具体金额在本轮打开的定价页里没有以可复制的固定数字出现，故不写入金额；是否到账以账户和官方说明为准（未登录，Unverified）。

**适用场景：** 只是提问、改稿、做课件提纲，继续用 ChatGPT；要把模型接到自己的脚本，或需要按量控制成本时，再开 API。

**限制：** ChatGPT 与 API 的可用模型名称也不完全相同。产品界面用思考等级和展示名（如 GPT-6、GPT-6.2），API 使用 `gpt-6-luna`、`gpt-6.2-sol`、`gpt-6.2-astra` 这类模型 ID。不要把网页选择器里的名字直接贴进 API 请求。地区限制二者共用官方支持名单：截至 2026-11-25，[官方支持国家和地区](https://help.openai.com/en/articles/7947663-chatgpt-and-openai-api-supported-countries-and-territories) 仍未列出中国大陆、香港特别行政区和澳门特别行政区。在名单以外访问或提供访问可能导致账号被限制或停用。不讨论绕过方法。

**来源与可信度：** Officially Documented。[What is ChatGPT Plus?](https://help.openai.com/en/articles/6950777-what-is-chatgpt-plus)、[What is ChatGPT Go?](https://help.openai.com/en/articles/11989085-what-is-chatgpt-go)、[ChatGPT Free Tier FAQ](https://help.openai.com/en/articles/9275245-chatgpt-free-tier-faq)、[Plans and Pricing](https://chatgpt.com/pricing/)、[ChatGPT and OpenAI API supported countries and territories](https://help.openai.com/en/articles/7947663-chatgpt-and-openai-api-supported-countries-and-territories)、[Developer quickstart](https://developers.openai.com/api/docs/quickstart)。查询日期 2026-11-25。

## 2. 在开发者平台创建密钥，只放在本机环境变量中

**用途：** 用官方要求的方式认证请求，并降低密钥泄露后被他人拿去扣费的风险。

**操作方法：**

1. 在官方开发者文档的指引下，到控制台创建 API key。官方 Quickstart 把「先创建密钥」作为第一步，并说明 SDK 会自动读取环境变量 `OPENAI_API_KEY`。
2. 把完整密钥保存在密码管理器或本机私密位置。官方写明：密钥是机密凭据；完整密钥通常只在创建时显示一次；不要把密钥写进浏览器前端、手机应用、源代码仓库、日志或会交给别人的作业。
3. 个人学习用与自己账号绑定的项目密钥即可。官方建议：不要把某一个人的密钥当作整个团队或长期运行程序的固定身份。
4. 在 Windows PowerShell 中按官方 Quickstart 设置环境变量：

```powershell
# 写入用户环境变量；需要新开一个终端后才生效
setx OPENAI_API_KEY "你的密钥"

# 若只想在当前窗口临时使用（官方文档以 setx 为例；这是同一变量在当前会话中的常用写法）
$env:OPENAI_API_KEY = "你的密钥"
```

在 macOS / Linux 上，官方示例为 `export OPENAI_API_KEY="your_api_key_here"`。

5. 怀疑密钥已泄露时，到控制台撤销旧密钥并新建一把，同时检查账单。不要把旧密钥再发到聊天里“请人帮忙测试”。

**适用场景：** 第一次配置 API，或换电脑后重新设置。

**限制：** 没有有效密钥的请求会失败。本轮未登录控制台，不能代为创建密钥，也不能核对照片级的菜单名称。平台能否在你所在地区打开，以官方支持名单和你自己的网络为准。

**来源与可信度：** Officially Documented。[Developer quickstart](https://developers.openai.com/api/docs/quickstart)、[API keys and service accounts](https://developers.openai.com/api/docs/guides/api-keys)。控制台点击路径为 Unverified。查询日期 2026-11-25。

## 3. 用官方 SDK 发出第一次请求，并先选用较便宜的模型做试验

**用途：** 确认密钥可用。官方示例默认使用旗舰模型，试验时若照抄可能很快产生较高费用。

官方 Python 示例如下（Responses API）。文档里的模型是 `gpt-6.2-astra`。按照 2026-11-25 官方价目，该模型短上下文标准价为每百万 tokens 输入 8 美元、输出 40 美元，适合最难的任务，**不适合当作第一次试验的默认模型**。把 `model` 改成 `gpt-6-luna`（官方定位为高用量、更省成本的高效模型；短上下文标准价为每百万 tokens 输入 0.10 美元、输出 0.50 美元）再试，通常更稳妥。下面第二段是同一官方调用方式，仅替换模型名，便于学习使用。两段都未经本轮运行。

```python
# 官方 Quickstart 的调用方式（模型为旗舰，试验前请先看费用）
from openai import OpenAI

client = OpenAI()
response = client.responses.create(
    model="gpt-6.2-astra",
    input="Write a one-sentence bedtime story about a unicorn.",
)
print(response.output_text)
```

```python
# 同一官方调用方式，仅将模型改为更适合试验的 gpt-6-luna
from openai import OpenAI

client = OpenAI()
response = client.responses.create(
    model="gpt-6-luna",
    input="用一句话解释什么是中位数。",
)
print(response.output_text)
```

安装官方 SDK：`pip install openai`。运行前需已设置 `OPENAI_API_KEY`。更完整的模型选择和省钱方法见 [api-models-pricing-and-cost.md](./api-models-pricing-and-cost.md)。

**适用场景：** 验证环境是否配置成功；随后再换正式任务和模型。

**限制：** 发出请求就会按 API 计费（若账户有额度和有效结算方式）。本轮未运行，不能保证你的网络和地区一定能连通。不要在示例里改用未出现在官方模型页的名称。

**来源与可信度：** Officially Documented。[Developer quickstart](https://developers.openai.com/api/docs/quickstart)、[Models](https://developers.openai.com/api/docs/models)、[Pricing](https://developers.openai.com/api/docs/pricing)。示例未经本轮运行，属 Unverified。查询日期 2026-11-25。

## 元数据

- 更新时间：2026-11-25（Asia/Shanghai）
- 来源：上文各官方帮助中心与开发者文档链接；产品界面的模型选择见 [work-and-model-selection.md](./work-and-model-selection.md)
- 信息可信度：部分核对。订阅与 API 分离、密钥规则、官方示例和地区名单为 Officially Documented。本轮未登录、未发请求，属 Unverified
- 平台：OpenAI API 与官方 Windows PowerShell 环境变量说明。ChatGPT 网页/App 仅用于对比。未实测具体机型
- 技能门槛：会在 Windows 上打开 PowerShell，安装 Python，并把密钥放进环境变量。不要求会写复杂程序
- 费用：API 计费。ChatGPT 订阅费用见价格笔记；API 不含在 Plus / Go 的常规权益中
