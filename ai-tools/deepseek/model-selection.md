# 模型与思考强度怎么选

适用产品：DeepSeek 网页/App 与官方 API。先选对入口和模型，再决定思考强度，通常比反复改一句提示词更省事、也更省钱。以下为官方说明，状态为 Officially Documented。本轮没有登录，也没有实际调用 API，不能当作已经实测成功。

## 1. 日常学习优先用官方网页或 App，只有要按量接入程序时才用 API

**用途：** 避免把本来可以在免费体验的对话里完成的作业提问，误开成一直计费的 API 调用。

**官方区分：**

- **网页和官方 App：** 下载页写明可「免费体验与全球领先 AI 模型的互动交流」。2026-10-17 起，官方网页和 App 使用的模型已更新为 DeepSeek-V4.1-Flash-1017。适合提问、上传讲义、联网搜索和一般写作。
- **API：** 按输入/输出 token 计费（另有文件解析、独立 Search/Fetch 等按次或按页项目）。接口与 OpenAI / Anthropic 格式兼容。适合接到自己的脚本，或官方已经写明支持的第三方软件。API 与 ChatGPT 订阅、DeepSeek 网页额度都不是同一笔账单。

**适用场景：** 解释概念、改作业草稿、复习上传的 PDF，用网页或 App；要在自己的程序里反复调用，再用 API。

**限制：** 「免费体验」不是官方公布的无限配额保证。API 必须先有可用余额（充值余额或未过期赠金），余额不足返回 402。不要在提示词或作业文档里粘贴 API 密钥。

**来源与可信度：** Officially Documented。[下载页](https://www.deepseek.com/download/)、[更新日志 2026-10-17](https://api-docs.deepseek.com/updates/)、[首次调用 API](https://api-docs.deepseek.com/zh-cn/)、[模型 & 价格](https://api-docs.deepseek.com/zh-cn/quick_start/pricing/)、[错误码](https://api-docs.deepseek.com/zh-cn/quick_start/error_codes/)。查询日期 2026-11-25。

## 2. 在 API 里默认用 deepseek-flash；只有明确需要 Pro 时再改

**用途：** 用对模型名，避免调用已经下线的旧名称，或在不需要时使用更贵的 Pro。

**现行官方模型（查询日期 2026-11-25）：**

| API 模型名 | 当前服务版本 | 上下文 / 最大输出 | 图像理解 | 思考模式 | 说明 |
| --- | --- | --- | --- | --- | --- |
| `deepseek-flash` | DeepSeek-V4.1-Flash-1017 | 1M / 最大 384K | 支持 | 支持关闭或开启（默认开启） | 官方推荐的当前调用名 |
| `deepseek-v4-pro` | DeepSeek-V4-Pro-0813 | 1M / 最大 384K | 不支持 | 同上 | 仍提供服务，单价更高 |

两者都支持 JSON 输出、工具调用、Responses API、Anthropic API 和对话前缀续写（Beta）。FIM 补全（Beta）仅在非思考模式下支持。

**操作方法：**

1. 新请求把 `model` 写成 `deepseek-flash`，不要写 `deepseek-v4-flash` 或 `deepseek-v4-flash-vision-exp`。后两个旧名仍可被接受，但对应模型已下线，请求会由 V4.1-Flash-1017 处理，并按 Flash 价格计费。
2. 需要看图、读带图表的扫描件或截图时，必须用 `deepseek-flash`。`deepseek-v4-pro` 不支持图像理解。
3. 不要在现行代码里继续写 `deepseek-chat` 或 `deepseek-reasoner`：这是更早世代的 API 名称，已不在 2026-11-25 的价目表中。
4. 官方在 2026-09-10 发布 V4.1-Flash 时曾预告将逐步淘汰 V4-Pro，并计划从 2026-09-14 起把 `deepseek-v4-pro` 请求转到 Flash。随后在更新日志中改口：应需求继续提供 V4 Pro 的 API 服务，计费方式不变，若有变化会再通知。因此本批仍把它列为可用模型，但默认建议先用 Flash。
5. 并发上限按账号计算，与使用哪一把 API Key 无关：`deepseek-flash` 为 2500，`deepseek-v4-pro` 为 500。超过返回 429。这对个人学习通常足够，但不要误以为限额是按密钥分开计算的。

**适用场景：** 作业问答、读讲义、看截图、大多数写作和推理，用 Flash。只有在你已经对比过质量、并接受 Pro 的更高单价时，再改模型名。

**限制：** 模型版本和价格会变，以价目页为准。本批未做质量评测，不能声称 Flash 一定优于或劣于 Pro。官网开放平台介绍页上的部分价格与 API 价目页不一致，选型时以 API 文档为准，见价格笔记。

**来源与可信度：** Officially Documented。[模型 & 价格](https://api-docs.deepseek.com/zh-cn/quick_start/pricing/)、[首次调用 API](https://api-docs.deepseek.com/zh-cn/)、[限速与隔离](https://api-docs.deepseek.com/zh-cn/quick_start/rate_limit/)、[更新日志](https://api-docs.deepseek.com/updates/)（2026-09-10、2026-10-17）。查询日期 2026-11-25。

## 3. 简单问题关闭思考或降低强度，难题再用 high 或 max

**用途：** 思考模式会先输出思维链再给答案，有助于提高准确性，但会增加输出长度、等待时间和 API 费用。不是每个问题都需要默认的 `high`。

**操作方法（API，OpenAI 兼容格式）：**

1. 思考模式默认开启，默认 `reasoning_effort` 为 `high`。
2. 关闭思考：在请求中设置 `"thinking": {"type": "disabled"}`。使用官方 Python SDK 的 Chat Completions 时，需把 `thinking` 放进 `extra_body`。
3. 开启并调节强度：`"thinking": {"type": "enabled"}`，同时设置 `reasoning_effort` 为 `low`、`high` 或 `max`。
4. 官方映射：`minimal` 会当成 `low`；`medium` 和 `xhigh` 会当成 `high`；`ultra` 会当成 `max`。想精确控制时，直接写 `low` / `high` / `max`。
5. 在 Responses API 中，用 `"reasoning": {"effort": "none/low/high/max"}`，其中 `none` 表示关闭思考。
6. 思考模式下，`temperature`、`presence_penalty`、`frequency_penalty` 不生效（为兼容不会报错）。思维链在 `reasoning_content` 字段中返回。若请求没有带 `tools`，下一轮不必回传思维链，回传了也会被忽略；若带了 `tools`，则必须完整回传，否则可能返回 400。

网页/App 中的对应开关名称和档位，请以界面为准（未登录，Unverified）。

**配置示例（关闭思考，适合短问答）：**

```bash
curl https://api.deepseek.com/chat/completions \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer ${DEEPSEEK_API_KEY}" \
  -d '{
        "model": "deepseek-flash",
        "messages": [
          {"role": "user", "content": "用一句话解释什么是中位数。"}
        ],
        "thinking": {"type": "disabled"},
        "stream": false
      }'
```

**配置示例（开启较高思考，适合多步推导）：**

```python
# pip install openai
import os
from openai import OpenAI

client = OpenAI(
    api_key=os.environ.get("DEEPSEEK_API_KEY"),
    base_url="https://api.deepseek.com",
)
response = client.chat.completions.create(
    model="deepseek-flash",
    messages=[{"role": "user", "content": "请逐步说明应怎样判断这道题该用哪一种假设检验。"}],
    reasoning_effort="high",
    extra_body={"thinking": {"type": "enabled"}},
)
print(response.choices[0].message.content)
```

以上示例来自官方文档的调用方式，本轮没有实际运行，不能当作已经调通。

**适用场景：** 翻译、改病句、回忆一个已给出的定义，可关闭思考或用 `low`；证明、比较多种方法、容易算错的数量关系，再用 `high` 或 `max`。

**限制：** 思维链不等于已经核对过的解题过程，关键步骤仍要自己验算。本批未实测各档在时间或费用上的具体差异，不能写入“能省多少钱”的数字。

**来源与可信度：** Officially Documented。[思考模式](https://api-docs.deepseek.com/zh-cn/guides/thinking_mode/)、[首次调用 API](https://api-docs.deepseek.com/zh-cn/)。示例未经本轮运行，执行结果为 Unverified。查询日期 2026-11-25。

## 元数据

- 更新时间：2026-11-25（Asia/Shanghai）
- 来源：上文各官方链接
- 信息可信度：部分核对。模型名、默认思考档位和能力对照表为 Officially Documented。网页/App 的具体档位开关为 Unverified。本轮未做模型质量对比
- 平台：API 以 `https://api.deepseek.com` 为准；网页/App 的模型更新见官方更新日志。未实测具体机型
- 技能门槛：阅读本篇前最好先看 [产品总览](../DeepSeek.md)。调整 API 参数需要会复制官方示例并设置环境变量，不要求会写复杂程序
- 费用：网页/App 为「免费体验」（限额未知）。API 为 API 计费；Flash 与 Pro、思考开关都会影响费用，见 [api-pricing-and-cost.md](./api-pricing-and-cost.md)
