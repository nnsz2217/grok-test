# API 用法

适用产品：DeepSeek 官方 API。用于在自己的程序或兼容 OpenAI / Anthropic 的软件里调用 DeepSeek 模型。以下为官方说明，状态为 Officially Documented。本轮没有申请密钥，也没有实际发出请求，不能当作已经调通或 Verified。本篇只说明官方用法，不写信息收集、批量改文件或自动生成文档一类的工作流实现。

## 1. 先在开放平台申请密钥并充值，再把密钥放到环境变量里

**用途：** 完成调用前的必要准备，同时避免把密钥写进作业、聊天记录或代码仓库。

**操作方法：**

1. 打开官方开放平台 [platform.deepseek.com](https://platform.deepseek.com)。官方错误码文档把「创建 API key」和「充值」作为解决 401、402 的步骤。本轮对该地址的未登录 GET 请求返回 HTTP 403，故无法核对照片级的点击路径；创建和充值的具体按钮以登录后的平台界面为准（Unverified）。
2. 按平台提示创建 API key，并立刻复制保存。密钥只应出现在你本机的安全位置，不要发给其他人，也不要写进将要提交的作业或公开仓库。
3. 官方写明：费用从充值余额或赠送余额中扣减；两者同时存在时优先扣赠送余额。可用 [查询余额](https://api-docs.deepseek.com/zh-cn/api/get-user-balance) 接口查看是否还有可调用余额（`is_available`），以及人民币或美元的总余额、赠金和充值余额。
4. 调用前，在当前终端把环境变量 `DEEPSEEK_API_KEY` 设为你的密钥。这是官方示例使用的变量名。
5. 在 Windows 的 PowerShell 中，官方 DeepSeek 文档没有单独截图。可参照 OpenAI 官方 Quickstart 为 Windows 提供的做法，用下面两种方式之一（把引号中的内容换成你的密钥）：

```powershell
# 仅对当前窗口有效
$env:DEEPSEEK_API_KEY = "你的密钥"

# 写入用户环境变量；需要新开一个终端后才生效
setx DEEPSEEK_API_KEY "你的密钥"
```

Windows 环境变量步骤本身来自 OpenAI 对 `setx` 的官方说明，迁移到 DeepSeek 变量名；DeepSeek 官方只写明“在当前终端设置 `DEEPSEEK_API_KEY`”。若你不熟悉终端，也可以先只用官方网页或 App，不必急着开 API。

**适用场景：** 第一次使用 API，或在新电脑上配置调用环境。

**限制：** 没有密钥或密钥写错会返回 401；余额不足返回 402。研究环境在 2026-11-25 未能打开平台页面，不能替你完成注册或充值，也不应把密钥交给他人或机器人代为保管。

**来源与可信度：** 创建密钥、充值和余额规则为 Officially Documented。[首次调用 API](https://api-docs.deepseek.com/zh-cn/)、[错误码](https://api-docs.deepseek.com/zh-cn/quick_start/error_codes/)、[模型 & 价格](https://api-docs.deepseek.com/zh-cn/quick_start/pricing/) 的扣费规则、[查询余额](https://api-docs.deepseek.com/zh-cn/api/get-user-balance)。Windows `setx` 写法见 [OpenAI Developer quickstart](https://developers.openai.com/api/docs/quickstart)（Officially Documented 的 Windows 做法，用于同类环境变量）。平台页面点击路径和本轮访问结果为 Unverified。查询日期 2026-11-25。

## 2. 用官方地址和模型名发出第一次对话请求

**用途：** 用最少的配置确认接口能返回回答。把 `base_url` 指到 DeepSeek，而不是 OpenAI。

**官方参数（查询日期 2026-11-25）：**

| 参数 | 值 |
| --- | --- |
| base_url（OpenAI 格式） | `https://api.deepseek.com` |
| base_url（Anthropic 格式） | `https://api.deepseek.com/anthropic` |
| api_key | 在开放平台申请 |
| model | `deepseek-flash` 或 `deepseek-v4-pro` |

日常学习建议先用 `deepseek-flash`。下面的非流式示例来自官方文档；把 `stream` 设为 `true` 可改为流式输出。本轮没有运行这些命令。

```bash
curl https://api.deepseek.com/chat/completions \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer ${DEEPSEEK_API_KEY}" \
  -d '{
        "model": "deepseek-flash",
        "messages": [
          {"role": "system", "content": "You are a helpful assistant."},
          {"role": "user", "content": "Hello!"}
        ],
        "thinking": {"type": "enabled"},
        "reasoning_effort": "high",
        "stream": false
      }'
```

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
    messages=[
        {"role": "system", "content": "You are a helpful assistant"},
        {"role": "user", "content": "Hello"},
    ],
    stream=False,
    reasoning_effort="high",
    extra_body={"thinking": {"type": "enabled"}},
)
print(response.choices[0].message.content)
```

用官方 Python SDK 时，`thinking` 必须放在 `extra_body` 里。最终回答在 `message.content`；若开启思考，思维链在 `message.reasoning_content`。多轮对话时，把返回的助手消息和你的新问题一起再发送；是否回传思维链，见 [模型与思考强度怎么选](./model-selection.md)。

请求发出后，若服务器还没开始返回正文，非流式请求可能持续收到空行，流式请求可能收到 `: keep-alive` 注释。自己解析 HTTP 时不要把这些当成错误。若 10 分钟后仍未开始推理，服务器会关闭连接。

**适用场景：** 验证密钥和网络是否可用；作为以后自己改提示词的起点。

**限制：** 本篇不演示如何把它扩建成自动处理作业、抓取网页或批量生成文档的程序。那一类方案属于自动化研究方向。兼容 OpenAI 格式不等于所有 OpenAI 参数、模型名或控制台功能都能原样使用。

**来源与可信度：** Officially Documented。[首次调用 API](https://api-docs.deepseek.com/zh-cn/)、[思考模式](https://api-docs.deepseek.com/zh-cn/guides/thinking_mode/)、[限速与隔离](https://api-docs.deepseek.com/zh-cn/quick_start/rate_limit/)。示例未经本轮运行，属 Unverified。查询日期 2026-11-25。

## 3. 先看官方错误码，再决定是改请求、充值还是等待

**用途：** 遇到失败时按官方原因处理，而不是反复重试或怀疑“模型坏了”。

**官方错误码（摘要）：**

| 错误码 | 官方说明的原因 | 官方建议 |
| --- | --- | --- |
| 400 | 请求体格式错误 | 按报错修改请求体 |
| 401 | API key 错误 | 检查密钥，或先创建密钥 |
| 402 | 余额不足 | 确认余额并前往充值页 |
| 408 | 上传过慢（如 OCR、语音） | 检查网络后重试，并查看对应接口限制 |
| 413 | 请求体或文件过大 | 减小文件 |
| 422 | 参数错误 | 按报错修改参数 |
| 429 | 速率或并发达到上限 | 降低并发；限额见限速文档 |
| 500 | 服务器内部故障 | 稍后重试；若持续出现再联系官方 |
| 503 | 服务器负载过高 | 稍后重试 |
| 504 | 网关超时（如 OCR 或文档上传） | 稍后重试或减小文件 |

个人学习最常见的是 401（密钥）、402（没钱）和偶发 503（繁忙）。429 在默认并发（Flash 2500、Pro 500，按账号计）下，单人手工调用通常不易碰到。

**适用场景：** 第一次调用失败，或高峰时段请求没有返回。

**限制：** 错误码不能代替余额和用量记录。具体账单以开放平台为准。本轮未触发这些错误，属于文档整理。

**来源与可信度：** Officially Documented。[错误码](https://api-docs.deepseek.com/zh-cn/quick_start/error_codes/)、[限速与隔离](https://api-docs.deepseek.com/zh-cn/quick_start/rate_limit/)。查询日期 2026-11-25。

## 元数据

- 更新时间：2026-11-25（Asia/Shanghai）
- 来源：上文各官方链接；Windows `setx` 参见 [OpenAI Developer quickstart](https://developers.openai.com/api/docs/quickstart)
- 信息可信度：部分核对。地址、参数、示例和错误码为 Officially Documented。本轮未登录开放平台、未创建密钥、未发送请求，执行结果为 Unverified
- 平台：官方 API（`https://api.deepseek.com`）。Windows 环境变量步骤参考 OpenAI 官方 Windows 说明。未实测具体机型
- 技能门槛：会在 Windows 上打开 PowerShell，安装 Python 或使用 curl，并把密钥放进环境变量。不要求会写复杂程序
- 费用：API 计费。调用会产生费用；单价和时段见 [api-pricing-and-cost.md](./api-pricing-and-cost.md)
