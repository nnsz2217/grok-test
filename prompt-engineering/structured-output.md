# 结构化输出

这篇说明怎样让模型按你指定的格式回答：例如固定小标题、表格，或可复制的 JSON。这样你更容易核对、摘录，也不容易得到一长段没有结构的散文。

## 正文

### 先分清两层做法

**1. 在聊天框里用提示词约定格式。**  
适合日常学习。你可以要求 Markdown 标题、表格、编号列表，或「只输出一段 JSON」。Google 明确说：你可以指定回答做成表格、要点、一句话或一段话；也可以先写出格式开头，让模型按这个模式续写（他们称为 completion strategy）。见 [Gemini prompt design strategies](https://ai.google.dev/gemini-api/docs/prompting-strategies)。Anthropic 则建议：多说「要写成什么样」，少说「不要写成什么样」；也可以要求把某一部分放进 XML 标签，例如 `<quotes>`。见 [Claude prompting best practices](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices) 的 “Control the format of responses”。

这一层**不能保证**每次都严格合法。模型仍可能多写开场白、漏字段，或给出不能解析的 JSON。

**2. 在 API 里用 Structured Outputs（结构化输出）约束格式。**  
当你真正需要「每次都是合法、且符合字段定义的 JSON」时，官方都建议用 schema（模式）去约束，而不是把希望全押在提示词上。

- OpenAI：Structured Outputs 会把已完成、且非拒答的输出，约束到你提供的 JSON Schema。好处包括：字段和枚举值按 schema 走、安全拒答可以被程序识别、提示词不必为了格式写得很强硬。他们建议：只要能用 Structured Outputs，就优先于只保证「是 JSON、但不保证字段」的 JSON mode。见 [OpenAI Structured model outputs](https://developers.openai.com/api/docs/guides/structured-outputs)。
- Anthropic：用 `output_config.format`，`type` 为 `json_schema`，通过受约束的解码来保证可解析、类型正确、必填字段存在。见 [Claude structured outputs](https://platform.claude.com/docs/en/build-with-claude/structured-outputs)。
- Google：对较复杂的 JSON Schema，建议使用 Gemini API 的 structured output，而不是只靠自然语言描述。见 [Gemini prompt design strategies](https://ai.google.dev/gemini-api/docs/prompting-strategies) 和 [Gemini structured outputs](https://ai.google.dev/gemini-api/docs/structured-output)。

ChatGPT、Grok、DeepSeek 等聊天界面通常不会让你提交一份完整的 JSON Schema 去强制校验。日常学习用第 1 层即可；只有在写程序调用 API 时，才需要第 2 层。本文不展开 SDK 代码，需要实现时请直接看上面的官方页面。

### 聊天里怎样把格式说清楚

把「输出长什么样」写成看得见的骨架，比只说「请结构化」有效。下面是一个可直接改用的聊天模板，依据的是 Google 的「指定 response format」、Anthropic 的「正向说明格式 / 可用 XML 标签」，以及 OpenAI「用 Markdown 或标签划分结构」的做法。它不是某个官方页面的原句模板。

```text
请只根据我给出的材料作答。不要加开场白、不要加结尾寒暄。

请严格按照下面的 Markdown 标题输出：

## 一句话结论
（不超过 40 字）

## 关键信息
- 项目：内容（材料中找不到就写「未说明」）

## 不确定或需要核对的地方
- ……

## 原文依据
请先摘录 2 到 4 句原文，再根据这些句子作答。用下面的标签包起来：

<quotes>
1. “……”
2. “……”
</quotes>

不要输出以上标题之外的内容。
```

如果这次你需要的是 JSON（例如要粘进笔记软件，或交给同学用表格整理），把格式段换成下面这样，并明确「不要用代码块以外的文字」：

```text
只输出一个 JSON 对象，不要输出解释，不要用 Markdown 代码块包裹。
如果某项在材料中找不到，请填 "未说明"，不要编造。

JSON 必须包含这些字段：
{
  "title": "材料的标题或主题",
  "audience": "这篇内容适合谁读",
  "key_points": ["要点1", "要点2", "要点3"],
  "open_questions": ["还没搞清的问题"],
  "source_quotes": ["从材料里摘的原句"]
}
```

即使用了上面的要求，也要自己看一眼：字段是否齐全、是不是真的只有 JSON。这是提示词约定，不是 API 的 schema 强制。

### 官方教学例子：按步骤讲一道数学题

OpenAI 在 Structured Outputs 文档里给过一个数学辅导的 schema 例子，用来让模型按步骤讲解，而不是只丢一个答案。核心结构是：

- `steps`：数组，每一步有 `explanation`（这一步在做什么）和 `output`（这一步得到什么）
- `final_answer`：最终答案

配套提示是一句很短的说明：`You are a helpful math tutor. Guide the user through the solution step by step.` 用户再发题目，例如 `how can I solve 8x + 7 = -23`。见 [OpenAI Structured model outputs](https://developers.openai.com/api/docs/guides/structured-outputs) 的 “Structured Outputs for chain-of-thought math tutoring”。

在聊天框里没有 schema 强制时，可以把同一结构改写成可见标题。下面是改写版，不是官方原模板；字段名称与官方例子一致，并改成了中文标题和「先写步骤、最后给答案」的聊天用法。

```text
你是耐心的讲解助手，请一步一步带我看懂这道题，不要只给最终答案。

请严格按照下面格式输出：

## steps
### 第 1 步
- explanation：
- output：

### 第 2 步
- explanation：
- output：

（需要几步就写几步）

## final_answer
（只写最终答案）

## 我想再确认的一点
（指出最容易算错或理解错的一步。如果没有，写「无」）

题目：
把题目粘在这里。
```

### 小结：怎么选

- 只要自己阅读、复习、做笔记：用固定小标题或表格即可。
- 要把结果复制到表格、问卷或自己的小工具：先在聊天里要 JSON，并人工检查。
- 要在程序里稳定解析：用各家 API 的 Structured Outputs / JSON Schema，不要指望「请一定输出 JSON」这类句子永远成功。

## 元数据

- 更新时间：2026-11-25（Asia/Shanghai）
- 来源：
  - [OpenAI Structured model outputs](https://developers.openai.com/api/docs/guides/structured-outputs)
  - [OpenAI Prompt engineering](https://developers.openai.com/api/docs/guides/prompt-engineering)
  - [Claude prompting best practices](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices)
  - [Claude structured outputs](https://platform.claude.com/docs/en/build-with-claude/structured-outputs)
  - [Gemini prompt design strategies](https://ai.google.dev/gemini-api/docs/prompting-strategies)
  - [Gemini structured outputs](https://ai.google.dev/gemini-api/docs/structured-output)
- 信息可信度：已核对（API 能力与官方数学辅导 schema 已对照上述文档；聊天模板是按这些方法改写，未在各聊天产品里逐条实测）
- 平台：聊天框格式约定（通用）；JSON Schema 强制仅适用于提供 Structured Outputs 的 API（文中已列 OpenAI、Anthropic、Gemini 官方文档）
- 技能门槛：会在对话框里粘贴并改一段提示词；不要求会写代码。若要使用 API schema，需能读对应官方文档
- 费用：不适用（本文讲格式控制，不涉及产品定价）
