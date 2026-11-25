# 项目、说明与记忆边界

适用产品：ChatGPT。把同一门课、同一份作业或同一项长期任务的对话、文件和说明放在一起，避免每次重新交代背景。下面几条都来自官方帮助中心，状态为 Officially Documented。本轮没有登录实操，不能当作已经实测成功。

## 1. 给一门课或一份作业建一个项目，并写清项目说明

**用途：** 让后续对话自动带上这门课的资料和你的要求，例如“按讲义出练习题，先不要直接给答案”。

**操作方法：**

1. 登录后，在侧边栏选择 **New project**（新建项目）。手机应用里通常点 **+**。
2. 输入项目名称，必要时选图标和颜色。
3. 在项目里上传 PDF、表格、文档、图片，或粘贴文本。官方举例：把课堂材料放进项目，请它做学习指南或练习题。
4. 打开更多选项（•••）→ **Project settings**（项目设置），写上只在这个项目里生效的说明。
5. 之后在这个项目里开新对话，而不是在普通聊天里重新上传全部资料。

项目和项目分享面向已登录用户，仍受方案和工作区设置影响。

**可复制的项目说明示例：**

```text
你是这门课的学习助手，不是代写工具。
只根据本项目里的讲义、大纲和我上传的资料回答。
如果资料里没有依据，明确说“讲义里没写”，不要编造页码、定义或文献。
回答用简体中文。先给要点，再问我是否要例题或自测。
出题时一次只出一题，等我作答后再讲解。
```

**适用场景：** 学期中反复问同一门课；一份课程论文要分多天改；小组作业需要长期保留同一批参考材料。

**限制：**

- 各方案能上传的项目文件数量不同。官方帮助在「Uploading files and audio to ChatGPT」中写明：Free 每个项目最多 5 个文件；Go 和 Plus 最多 25 个；Edu、Pro、Business 和 Enterprise 最多 40 个。查询日期 2026-11-25。数量以后可能调整，以账户界面为准。
- 若把 Google Drive 或 Slack 链接加为项目来源，需要先连接相应应用。**连接 Google Drive 必须有谷歌帐户。** 没有谷歌帐户时，请直接上传导出后的 PDF 或 DOCX，不要依赖云端链接。官方也写明：不能直接上传 `.gdoc`，需先导出为 PDF 或 DOCX。
- 学习模式（Study mode）不能在项目对话里开启，见本目录的学习模式笔记。

**来源与可信度：** Officially Documented。[Projects in ChatGPT](https://help.openai.com/en/articles/10169521-projects-in-chatgpt)、[Uploading files and audio to ChatGPT](https://help.openai.com/en/articles/8555545-uploading-files-and-audio-to-chatgpt)。查询日期 2026-11-25。

## 2. 项目说明会覆盖全局自定义指令

**用途：** 全局自定义指令适合写“我是谁、希望你怎样说话”；某一门课或某一类任务若有不同规则，应写在项目说明里，以免和全局偏好打架。

**操作方法：**

1. 全局自定义指令在网页或桌面应用中位于 Settings → Personalization；手机位于 Settings → Customize ChatGPT。打开 Enable customization 后填写。
2. 所有方案都可以使用自定义指令，适用于 Web、Desktop、iOS 和 Android。修改后会立即作用于全部对话（包括已有对话的后续回复）。
3. 字符上限官方写明：Free 和 Go 最多 1,500 字符；Plus、Pro、Enterprise、Business 和 Education 最多 5,000 字符。查询日期 2026-11-25。
4. 项目说明只在该项目内生效，并且**会覆盖**全局自定义指令。

**可复制的全局自定义指令示例：**

```text
我是非计算机专业的大学生。请默认用简体中文回答。
先给我能直接用的结论或步骤，再补必要的解释。
不确定时请明确说不确定，并告诉我应该核对什么。
不要为了听起来完整而编造引用、数据或链接。
```

**适用场景：** 希望大多数对话都简洁、谨慎；但某门课要求严格按讲义术语回答，就把这条写进该课的项目说明。

**限制：** 自定义指令可能随插件或应用把相关信息发给第三方，只使用你信任的插件。共享对话链接的查看者看不到你的自定义指令。本轮未实测设置界面的具体文案。

**来源与可信度：** Officially Documented。[ChatGPT Custom Instructions](https://help.openai.com/en/articles/8096356-chatgpt-custom-instructions)、[Projects in ChatGPT](https://help.openai.com/en/articles/10169521-projects-in-chatgpt)。查询日期 2026-11-25。

## 3. 选对项目记忆：默认记忆或仅项目记忆

**用途：** 决定这个项目能不能用到你在别处存下的偏好，以及项目里的内容会不会渗到项目外的对话。

**操作方法：**

1. 创建项目时可选择记忆设置；之后也可在项目设置里更改。
2. 可选 **Default memory**（默认记忆）或 **Project-only memory**（仅项目记忆）。
3. 更改可能需要几小时才完全生效。
4. 切换到仅项目记忆后，该项目中的信息会从项目外使用的记忆中移除；项目内的对话和文件仍留在项目里，可继续作为项目内上下文。
5. 共享项目会自动设为仅项目记忆，且不能改回默认记忆。共享项目也不能使用某个成员在项目外的自定义指令或记忆。官方还写明：仅项目记忆下，ChatGPT Work 在该项目中不可用。

**适用场景：** 课程项目、涉及个人偏好但不想和别的任务混在一起时，优先用仅项目记忆。需要它记住你一贯的写作风格、且不介意与普通对话互通时，再考虑默认记忆。

**限制：**

- 记忆功能随方案、地区、平台和工作区设置而变，界面里若没有某项开关，可能是当前帐户尚未提供。
- 在需要开启「引用已保存记忆 / 引用聊天记录」的帐户上，仅项目记忆也依赖这些设置；托管工作区还需要组织允许使用记忆。
- Enterprise 和 Edu 的默认记忆仍把项目内对话限制在项目内，不能引用项目外对话。细节以官方对照表为准。
- 本轮没有登录，无法核对自己帐户里实际看到的选项，相关界面观察为 Unverified。

**来源与可信度：** Officially Documented（功能规则）；帐户里是否出现某一开关为 Unverified。[Projects in ChatGPT](https://help.openai.com/en/articles/10169521-projects-in-chatgpt)、[Memory in ChatGPT](https://help.openai.com/en/articles/8590148-memory-in-chatgpt)。查询日期 2026-11-25。

## 4. 把有用的回复存成项目资料，而不是只留在聊天记录里

**用途：** 把一份已经核对过的摘要、决定记录、提纲或分析固定下来，之后的新对话可以把它当作来源，而不必翻很长的聊天记录。

**操作方法：**

1. 在项目对话里打开那条回复的消息菜单。
2. 选择 **Add to project sources**（添加到项目资料）。
3. 之后可在项目资料列表里找到它，供后续对话使用。

**社区经验（Community Reported，不是官方步骤）：** 有用户建议，在较长的课题研究中，定期把“当前掌握的结论和待核对问题”整理成一份总述，再存进项目资料，而不是只依赖记忆。这与官方“可把回复存为项目来源”相符，但“多久整理一次最有效”没有官方规定，也未经本轮实测。

**适用场景：** 文献阅读多天后需要一份可继续追问的总笔记；小组讨论后留下已确认的分工和截止日期。

**限制：** 存进去的内容不会自动变成经过核验的事实。若回复里有错误，应先改正确再保存。共享项目中删除文件会对该项目所有成员生效。定时任务即使在项目里创建，也不能访问该项目已上传或已保存的文件，见定时任务笔记。

**来源与可信度：** 操作步骤为 Officially Documented，见 [Projects in ChatGPT](https://help.openai.com/en/articles/10169521-projects-in-chatgpt)。定期整理总述的做法为 Community Reported。查询日期 2026-11-25。

## 5. 项目里几项容易忽略的功能边界

**用途：** 避免在项目里寻找实际不可用的功能，或误以为自定义 GPT、学习模式、定时任务会自动带上项目资料。

**官方已经写明的边界：**

- **学习模式不能在项目中开启。** 须在普通 ChatGPT 对话里使用；临时对话和 GPT 对话里同样不可用。
- **在项目里创建的定时任务，不能访问该项目已上传或存放的文件。**
- **可以在已有的项目对话里使用自定义 GPT；** 但如果第一条消息就使用自定义 GPT，这次对话会作为与该 GPT 的聊天开始，并出现在项目之外。
- **共享项目里的对话不能多人同时写同一条线程，** 但可以分支（branch）去尝试另一种写法，而不改原来的对话。

**适用场景：** 既想用项目保存讲义，又想用学习模式复习时，把讲义同时附到一则普通对话里开启学习模式，或先在项目里整理材料，再在普通对话中上传需要的部分。

**限制：** 自定义 GPT 本身正处在退役过渡期，个人帐户不能新建 GPT，详见插件与 GPT 过渡笔记。不要把上述边界理解成故障。

**来源与可信度：** Officially Documented。[Projects in ChatGPT](https://help.openai.com/en/articles/10169521-projects-in-chatgpt)、[Using study mode in ChatGPT](https://help.openai.com/en/articles/11780217-using-study-mode-in-chatgpt)、[Scheduled tasks in ChatGPT](https://help.openai.com/en/articles/10291617-scheduled-tasks-in-chatgpt)。查询日期 2026-11-25。

## 元数据

- 更新时间：2026-11-25（Asia/Shanghai）
- 来源：
  - [Projects in ChatGPT](https://help.openai.com/en/articles/10169521-projects-in-chatgpt)
  - [ChatGPT Custom Instructions](https://help.openai.com/en/articles/8096356-chatgpt-custom-instructions)
  - [Memory in ChatGPT](https://help.openai.com/en/articles/8590148-memory-in-chatgpt)
  - [Uploading files and audio to ChatGPT](https://help.openai.com/en/articles/8555545-uploading-files-and-audio-to-chatgpt)
  - [Using study mode in ChatGPT](https://help.openai.com/en/articles/11780217-using-study-mode-in-chatgpt)
  - [Scheduled tasks in ChatGPT](https://help.openai.com/en/articles/10291617-scheduled-tasks-in-chatgpt)
- 信息可信度：部分核对。文中对照官方文档的功能、限制和字数/文件数量为 Officially Documented。定期整理项目总述为 Community Reported。本轮未登录，界面文案和帐户里实际可见的开关为 Unverified，不能当作已经实测成功。未核对手表价
- 平台：官方文档中的网页、桌面应用和 iOS / Android。Windows 可用官方桌面应用或浏览器。未实测具体机型
- 技能门槛：会登录 ChatGPT、新建项目并上传文件。不需要编程
- 费用：免费 / 付费。项目对已登录用户开放，但文件数量等限制随方案而变；未核对具体价格，故不写入金额
