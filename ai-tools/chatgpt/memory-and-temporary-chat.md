# 记忆与临时对话

适用产品：ChatGPT。记忆用来减少重复介绍自己的背景；临时对话用来进行不想写入历史、也不想用来更新记忆的单次提问。以下为官方说明，状态为 Officially Documented。本轮没有登录实操，不能当作已经实测成功。

## 1. 定期查看记忆用了什么，错了就改

**用途：** 避免它长期记错你的专业、年级、写作偏好或正在进行的课题，从而在后续回答里反复用错背景。

**操作方法：**

1. 打开 Settings → Personalization → Memory。不同帐户可能看到 Memory、Reference saved memories、Reference chat history、Memory summary、Manage 或 Saved memories 等不同控件。
2. 若有记忆摘要（memory summary），可以在文本框里改正，或选中一段后提交更正。也可以对某条选择 **Don't mention this again**（以后不要再提）。
3. 可以直接问：“你现在记得我的哪些信息？哪些会影响到学习辅导？”
4. 当回复用到了个人背景时，下方有时会出现 **Sources**（来源），可能指向过去的对话、已保存记忆、自定义指令、文件或已连接的邮箱。可据此打开、改正或删除对应来源。
5. 已保存记忆和聊天记录是分开的：删除原对话不一定删除由此产生的已保存记忆；关闭「引用聊天记录」也不会删除已保存记忆。
6. 删除和更新可能需要一段时间才会完全生效。官方写明，已删除的已保存记忆日志可能因安全与调试保留最多 30 天。

**可复制的提示词示例：**

```text
请列出你当前可能用来个性化回答的、和我有关的信息。
分成：学习背景、写作偏好、正在进行的任务、你不确定是否仍然正确的条目。
不要补充我没说过的内容。如果某条可能已过时，请标出来，我来确认是否删除。
```

**适用场景：** 换了专业方向或课程安排；发现它总按错误的年级或文风回答；把敏感个人信息误说进普通对话后，需要检查是否被记住。

**限制：**

- 记忆功能随方案、地区、平台和工作区设置而变。看不到某项控件，不代表操作错误，可能是尚未对你的帐户开放。
- 记忆不会保留每段对话的全部细节。摘要也不等于它可能引用的全部来源。
- 关闭 Memory 不会删除过去的聊天。之后若重新打开，它可能再从仍保留的历史中形成新的记忆。
- 连接 Gmail 等应用后，记忆也可能用到来自这些应用的内容。**Gmail 需要谷歌帐户。** 没有谷歌帐户就不要连接 Gmail；可改用临时对话或不连接邮箱。
- 共享对话链接不会包含记忆来源。

**来源与可信度：** Officially Documented。[Memory in ChatGPT](https://help.openai.com/en/articles/8590148-memory-in-chatgpt)。查询日期 2026-11-25。

## 2. 需要额外隐私时用临时对话，并在开始前选好是否个性化

**用途：** 进行一次不想出现在历史里、也不想用来更新记忆的提问，例如练习用一份敏感案例，或先试探一个不想留下记录的问题。

**操作方法：**

1. 新建对话，选择 **Temporary**（临时）。
2. 发送第一条消息前，选择 **Personalized**（使用已有记忆、自定义指令和插件）或 **Unpersonalized**（不使用这些个性化）。开始后不能再改这一选择。
3. 临时对话在保持临时状态期间，既不会创建也不会更新记忆；也不会用于改进模型。
4. 若之后选择保存，它会变成普通对话，并开始遵循帐户的个性化与模型改进设置。若 Memory 处于开启状态，这次保存后的对话可能被用于以后的个性化。
5. 不保存并离开后，无法再从历史里打开它。

**适用场景：** 不想把某次讨论写入历史；想用已有偏好来写一封信，但不想让这次的内容进入长期记忆；需要短暂关闭个性化，避免旧记忆干扰。

**限制：**

- 官方写明：即使不保存，OpenAI 仍可能因安全目的保留临时对话副本最多 30 天。临时对话不是“发送后立即从所有系统消失”。
- 帐户和工作区的限制优先于单次临时对话的个性化选择。
- 关闭记忆或个性化，不会关闭在少数高风险情形下出于安全目的使用有限上下文的机制。
- 可以在临时对话中使用 GPT。若该 GPT 会通过 actions 把数据发给第三方，则按对方的隐私政策处理，保留时间可能超过 30 天。
- 学习模式不能在临时对话中开启。
- 在 Temporary Chat 里对写作块或代码块的编辑，对话结束后可能不会保留。
- 临时对话中创建的文件不会保存到 Library。

**来源与可信度：** Officially Documented。[Temporary chat in ChatGPT](https://help.openai.com/en/articles/8914046-temporary-chat-in-chatgpt)、[Memory in ChatGPT](https://help.openai.com/en/articles/8590148-memory-in-chatgpt)、[Using study mode in ChatGPT](https://help.openai.com/en/articles/11780217-using-study-mode-in-chatgpt)、[Working with writing blocks and code blocks in ChatGPT](https://help.openai.com/en/articles/20001246-working-with-writing-blocks-and-code-blocks-in-chatgpt)、[Creating and editing documents, spreadsheets, and presentations with ChatGPT Work](https://help.openai.com/en/articles/20001278-creating-and-editing-documents-spreadsheets-and-presentations-with-chatgpt-work)。查询日期 2026-11-25。

## 元数据

- 更新时间：2026-11-25（Asia/Shanghai）
- 来源：上文各官方帮助中心链接
- 信息可信度：部分核对。对照官方文档的功能与限制为 Officially Documented。本轮未登录，帐户里实际可见的记忆控件为 Unverified。未核对手表价
- 平台：官方文档中的网页、桌面和移动应用。未实测具体机型
- 技能门槛：会打开设置并阅读记忆或临时对话选项。不需要编程
- 费用：免费 / 付费。记忆是否对某一帐户开放随方案和地区而变；未核对具体价格，故不写入金额
