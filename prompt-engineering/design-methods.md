# 提示词的设计方法

这篇说明怎样写出能看懂、能改着用的提示词：先把任务说清楚，再补上格式、例子和材料。方法来自 OpenAI、Anthropic 和 Google 的官方文档，不是来历不明的「万能模板」。

## 正文

### 先把任务写清楚

Anthropic 的建议是：把模型当成「很能干、但不了解你习惯的新同事」。你越清楚地说要什么，结果通常越好。他们还给出一个自测办法：把提示词拿给几乎不了解这件事的同学看，如果对方会懵，模型也容易懵。见 [Claude prompting best practices](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices)。

Google 也把「清楚、具体的指令」放在最前面：可以是一个问题、一组按步骤执行的任务，或更细的约束。见 [Gemini prompt design strategies](https://ai.google.dev/gemini-api/docs/prompting-strategies)。

因此，不要只写「帮我看看这篇论文」，而要写清：你是谁、要模型做什么、不要做什么、结果长什么样。

对比（改编自 Anthropic 对「说清楚输出和约束」的说明，原例是做分析仪表盘）：

```text
较差：帮我总结这篇文章。

较好：请用中文总结下面这篇文章，面向非专业读者。只根据原文，不要补充原文没写的背景。先给 3 条要点，每条不超过 40 字，再写一段不超过 150 字的总述。如果原文没给出结论，请写「原文未说明」，不要猜测。
```

### 一条提示词通常包含哪些部分

OpenAI 建议，给模型的稳定说明（在 API 里常放在 `developer` 消息，在聊天产品里相当于你先贴的「角色和规则」）通常按这个顺序组织，具体顺序可随模型微调：

1. **Identity（身份）**：你希望它扮演什么角色、说话风格、总目标。
2. **Instructions（指令）**：要做什么、不要做什么、必须遵守的规则。
3. **Examples（例子）**：输入长什么样、理想输出长什么样。
4. **Context（上下文）**：这次任务要用到的材料，例如文章、笔记、题目。OpenAI 写到，这部分常常放在提示词靠后的位置，方便每次更换材料。

见 [OpenAI Prompt engineering](https://developers.openai.com/api/docs/guides/prompt-engineering) 中的 “Message formatting with Markdown and XML”。

**材料放哪，官方说法并不完全一样，不要混成一条死规则：**

- OpenAI：在上述四段结构里，Context 通常靠近提示词末尾。
- Anthropic：处理很长的文档时（他们写的是 20k+ tokens），把长材料放在提示词**前面**，把问题放在**最后**；他们还写到，在多文档、较复杂的测试里，问题放在末尾最多可把回答质量提高约 30%。见同一份 [Claude prompting best practices](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices) 的 “Long context prompting”。
- Google 对 Gemini 3 的建议类似：先放数据，再把具体问题和指令放在后面，并用「根据前面的信息……」把推理锚在材料上。见 [Gemini 3 Developer Guide](https://ai.google.dev/gemini-api/docs/gemini-3)。

聊天时的实用折中：先粘贴文章或资料，最后再写你的问题和格式要求。

### 用例子教模型（few-shot）

OpenAI 把这叫做 few-shot learning：在提示词里放几个「输入 → 理想输出」的例子，让模型自己跟上模式，而不必先去微调模型。例子要覆盖不同情况，避免模型学到你不想要的固定套路。见 [OpenAI Prompt engineering](https://developers.openai.com/api/docs/guides/prompt-engineering) 的 “Few-shot learning”。

Anthropic 认为例子是引导格式、语气和结构最稳的办法之一，并建议用 3 到 5 个相关、多样、结构清楚的例子。见 [Claude prompting best practices](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices)。

Google 也建议尽量带上 few-shot 例子，并保持例子的格式一致（包括换行和标记）。他们甚至写到：如果例子已经把任务展示清楚，有时可以减少文字指令。见 [Gemini prompt design strategies](https://ai.google.dev/gemini-api/docs/prompting-strategies)。

聊天里不必一次塞 5 个长例子。先放 1 到 2 个短例子，如果格式仍不稳，再补到 3 个左右。

### 用 Markdown 或 XML 把材料和指令分开

当你的提示词里同时有规则、例子和整篇文章时，模型可能分不清哪一段是指令、哪一段是资料。OpenAI 建议用 Markdown 标题和列表划分层次，用 XML 标签标出一段参考材料的起止。Anthropic 同样建议用含义清楚、前后一致的 XML 标签，例如 `<instructions>`、`<example>`、`<document>`。

这不是「只有 Claude 才认 XML」。它的作用是把边界标清楚。在 ChatGPT、Grok、DeepSeek 的对话框里，用 Markdown 小标题通常就够；材料一多，再加上标签会更稳。

### 给角色，但角色不是魔法

Anthropic 写到：在系统说明里给一个角色，即使只有一句话，也能帮助聚焦语气和做法。角色要服务于任务，例如「你是会把难句改写成白话的阅读助手」，而不是空泛的「你是世界顶级专家」。更重要的仍是具体指令、例子和材料。

### 普通模型和推理模型，写法可以不同

这是 OpenAI 的官方区分，不要直接说成所有产品都一样：

- **推理模型（reasoning models）**：更像「资深同事」。给清目标和成功标准，让它自己补细节，往往更好。
- **GPT 类模型**：更像「需要说明书的同事」。把步骤和格式写明确，通常更好。

见 [OpenAI Prompt engineering](https://developers.openai.com/api/docs/guides/prompt-engineering) 的 “Prompting reasoning models” 和 “Choosing a model”。在 ChatGPT、Grok 或其他产品里，如果你选用了带「推理 / 思考」的模式，可以先给目标和验收标准；如果输出偏题或格式不稳，再补更细的步骤。本条没有核对这些产品各自的内部实现，只核了对 OpenAI 文档的转述。

### 可复制骨架（按官方结构改写）

下面这个骨架改写自 OpenAI 的 Identity / Instructions / Examples / Context 结构，并加上 Anthropic「写清格式和步骤」、Google「写清约束」的做法。它不是某个产品的官方原模板。在聊天框里整段粘贴，把尖括号里的内容换成你的任务即可。

```text
# 身份
你是面向大学生的学习助手。用简洁的中文解释，遇到术语先给一句白话定义。

# 指令
1. 只根据我提供的材料回答；材料里没有的，写「材料未说明」，不要编造。
2. 先给出结论，再给理由。
3. 按我指定的标题输出，不要加开场白或收尾寒暄。
4. 如果我的问题有歧义，先用不超过 3 个问题问清楚，再开始完整作答。

# 输出格式
- 结论：
- 依据：（引用材料里的原句或段落位置）
- 我还没搞懂的点：
- 下一步建议：（只给一个具体行动）

# 例子
输入：这篇摘要说实验人数很少，结论还能信吗？
输出：
- 结论：只能当初步线索，还不能当成已经证实。
- 依据：摘要写明样本只有 12 人，且没有对照组。
- 我还没搞懂的点：作者有没有报告效应量和局限性。
- 下一步建议：去正文的 Methods 和 Limitations 两节核对样本量和限制条件。

# 材料
把你的文章、笔记或题目粘在这里。

# 我的问题
把你真正想问的问题写在这里。
```

## 元数据

- 更新时间：2026-11-25（Asia/Shanghai）
- 来源：
  - [OpenAI Prompt engineering](https://developers.openai.com/api/docs/guides/prompt-engineering)
  - [Claude prompting best practices](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices)
  - [Gemini prompt design strategies](https://ai.google.dev/gemini-api/docs/prompting-strategies)
  - [Gemini 3 Developer Guide](https://ai.google.dev/gemini-api/docs/gemini-3)
- 信息可信度：已核对（方法与出处均对照上述官方文档；文末骨架是按这些方法改写的通用结构，不是官方原模板，也未在各聊天产品里逐条实测）
- 平台：通用聊天和 API 提示词写法；文中对推理模型与 GPT 模型的对比仅核自 OpenAI 文档
- 技能门槛：会在 ChatGPT、Claude、Grok 或同类对话框里粘贴并改一段文字
- 费用：不适用（本文讲写法，不涉及产品定价）
