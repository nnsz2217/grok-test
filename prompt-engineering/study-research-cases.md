# 学习与研究场景的可复制案例

这里给出 3 个可以直接复制、改一改再用的提示词：精读一篇长文或论文、整理考试复习提纲、分步讲一道题。它们都是根据官方方法改写的学习模板，不是网上流传、来历不明的「神级提示词」，也尚未在 ChatGPT、Claude、Grok 等界面里逐条实测。

使用前请先看 [提示词的设计方法](./design-methods.md) 和 [结构化输出](./structured-output.md)。把文中「把……粘在这里」换成你自己的材料即可。

## 正文

### 案例 1：精读一篇论文或长文

**适用：** 读课程论文、新闻长文、研报或教材章节，先抓住论点，再判断哪些话有依据。

**依据哪些方法：** Anthropic 建议处理长文档时，把材料放在前面、把问题放在最后；先要求摘录原文，再基于这些摘录分析，避免模型抛开材料自己发挥。他们还建议用 XML 标签分开多份文档。见 [Claude prompting best practices](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices) 的 “Long context prompting”。Google 在 [Gemini prompt design strategies](https://ai.google.dev/gemini-api/docs/prompting-strategies) 的 “Gemini 3”（“Core prompting principles”）中也建议：先提供全部上下文/材料，再把具体指令或问题放在提示词最末尾；可用 “Based on the information above...” / 「根据上面的信息……」作为过渡。

**改了什么：** Anthropic 原例是医疗助手根据病历先摘引再诊断，不适合直接给学生用。这里改成论文/长文精读，保留「材料在前、问题在后、先引原句再分析、用标签隔开」的结构，并加上中文输出标题和「材料未说明」的约束。

```text
<documents>
  <document index="1">
    <source>把文章标题或文件名写在这里</source>
    <document_content>
把全文、摘要，或你已经复制到的章节粘在这里。
    </document_content>
  </document>
</documents>

你是面向非专业读者的阅读助手。请只根据上面的材料回答，不要补充材料里没有的背景或结论。

请先从材料中摘录与我的问题最相关的 3 到 6 句原文，放进 <quotes> 标签，每句注明大概位置（例如「摘要」「第 2 节」）。然后只根据这些摘录作答。

按下面标题输出，不要加开场白：

## 这篇文章在说什么
（用不超过 120 字的白话说明）

## 作者的主要主张
- 主张：
  依据：（对应上面哪一句摘录）

## 证据和限制
- 作者用了什么证据：
- 作者自己承认的限制（没有就写「材料未说明」）：

## 我仍需核对的点
- （列出 2 个需要回到原文确认的问题）

我的问题：
这篇文章的核心主张是什么？证据够不够支撑？我读的时候最该注意什么限制？
```

如果要对比两篇，再增加一个 `<document index="2">...</document>`，并把最后的问题改成：「这两篇在主张和证据上有何异同？冲突时分别依据了什么？」不要把两篇文章混在同一个标签里。

### 案例 2：整理一份考试复习提纲

**适用：** 考前根据课堂笔记、课件或教材目录，整理「会什么、漏什么、下一步先复习什么」。

**依据哪些方法：** OpenAI 建议按 Identity、Instructions、Examples、Context 组织提示词，并用标题和列表规定输出。见 [OpenAI Prompt engineering](https://developers.openai.com/api/docs/guides/prompt-engineering)。Google 建议写明约束和回答格式，需要时用例子固定格式。见 [Gemini prompt design strategies](https://ai.google.dev/gemini-api/docs/prompting-strategies)。Anthropic 建议步骤用编号写出，并具体说明格式。见 [Claude prompting best practices](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices)。

**改了什么：** 官方文档里没有「大学生考试复习提纲」的现成原模板。下面是按上述结构新写的改写版：加入了课程信息和「只根据笔记、不编造考点」的约束，并用一个短例子锁定输出格式。

```text
# 身份
你是帮大学生整理复习提纲的助手。你不代替我考试，也不要假装知道我没提供的考点。

# 指令
1. 只根据我粘贴的笔记、课件摘录或目录整理，不要根据你的训练数据补充「常考」「一定会出现」这类判断。
2. 如果某项在材料里找不到，写「材料未说明」。
3. 先给提纲，再给一个最短的复习顺序。
4. 不要写鼓励的话，不要写超纲技巧。

# 输出格式
## 考试范围（按材料）
- ……

## 必须能独立讲清的概念
| 概念 | 一句话定义（根据材料） | 我还缺什么 |
| --- | --- | --- |

## 容易混的地方
- A 和 B 的差别：（根据材料）

## 建议的复习顺序（最多 5 步）
1. ……

# 例子
输入材料：「光合作用需要光；呼吸作用植物白天晚上都能进行。」
输出中「容易混的地方」应类似：光合作用依赖光，呼吸作用不限于白天；不要写成「考试必考光合作用」。

# 材料
课程：
考试日期：
我已经掌握的部分：
我最没把握的部分：

把笔记或课件摘录粘在这里。

# 我的问题
请根据这些材料，为我整理一份可直接用来复习的提纲。
```

### 案例 3：分步讲一道题

**适用：** 数学、统计、逻辑或其它需要步骤的课后题。目标是看懂每一步，而不是只抄答案。

**依据哪些方法：** OpenAI 在 Structured Outputs 文档里给过数学辅导例子：系统说明为 “You are a helpful math tutor. Guide the user through the solution step by step.” 输出结构包含 `steps`（每步有 `explanation` 和 `output`）和 `final_answer`。见 [OpenAI Structured model outputs](https://developers.openai.com/api/docs/guides/structured-outputs)。

**改了什么：** 官方例子是 API 的 JSON Schema，题目是 `8x + 7 = -23`。这里改成聊天可粘贴的中文版本，保留同样的字段，并增加「先不要直接报最终答案以外的捷径」「指出最容易错的一步」「我卡住时只提示下一步」这几条学习约束。

```text
你是耐心的讲解助手。请一步一步带我解题，不要只给最终答案，也不要跳步。

规则：
1. 每一步只做一件事，先说明为什么要这样做，再写出这一步的结果。
2. 用到公式或定理时，先用白话解释它在这道题里的作用。
3. 如果题目条件不够，指出缺什么，不要补造条件。
4. 如果我另外跟你说「我卡在某一步」，请只提示下一步该想什么，先不要把后面的步骤全部写完。

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

## 最容易错的一步
（指出哪一步最容易算错或理解错，并说明原因。如果没有，写「无」）

题目：
把完整题目粘在这里。

我目前的想法或卡点：
（没有就写「还没开始做」。）
```

若你使用带 API Structured Outputs 的编程环境，应直接采用官方 schema（`steps` + `final_answer`），而不是依赖上面的聊天标题。聊天版无法保证字段永远完整。

## 元数据

- 更新时间：2026-11-25（Asia/Shanghai）；同日复核 [Gemini prompt design strategies](https://ai.google.dev/gemini-api/docs/prompting-strategies) 的 “Gemini 3” 一节
- 来源：
  - [Claude prompting best practices](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices)（长文档：材料在前、问题在后、先摘录再分析）
  - [Gemini prompt design strategies](https://ai.google.dev/gemini-api/docs/prompting-strategies) 的 “Gemini 3”（先提供全部上下文/材料，具体指令或问题放在提示词最末尾；过渡可用 “Based on the information above...” / 「根据上面的信息……」）
  - [OpenAI Prompt engineering](https://developers.openai.com/api/docs/guides/prompt-engineering)（Identity / Instructions / Examples / Context）
  - [Gemini prompt design strategies](https://ai.google.dev/gemini-api/docs/prompting-strategies)（约束、格式、few-shot）
  - [OpenAI Structured model outputs](https://developers.openai.com/api/docs/guides/structured-outputs)（数学辅导 schema 与原提示）
- 信息可信度：部分核对（所用方法已对照官方文档；三个模板均为按这些方法改写的学习案例，不是官方原模板，也未在各聊天产品里逐条实测）
- 平台：通用聊天提示词；案例 3 的字段来自 OpenAI API 示例，聊天版没有 schema 强制
- 技能门槛：会把文章、笔记或题目粘贴进提示词，并按自己的课改几个空
- 费用：不适用（本文是提示词模板，不涉及产品定价）
