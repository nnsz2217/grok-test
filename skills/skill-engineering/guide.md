# Skill Engineering 技术指南（第一批：基于官方规范与官方技能原文）

这份指南回答「怎样设计、编写、测试和维护一份合格的 Skill」。它与仓库根目录的 [AI Skill Engineering 简报](../../ai-skill-engineering-guide.md) 互补：简报按项目梳理生态与架构脉络，本文按操作问题展开，并尽量把每条规则落到**已经打开过的官方规范或官方 `SKILL.md`**。本文不替换、也不复制那份简报。

本批依据以开放规范与官方技能为主。文末仅用一小段说明两个**非官方平台技能包**、但讨论「如何改进技能文本」时经常被提到的项目，避免把它们误认为官方合集。

## 先分清五种东西

写技能或收藏资料时，先判断对象属于哪一类：

| 类别 | 它是什么 | 本批对应例子 |
| --- | --- | --- |
| 可安装 / 可加载的 Skill | 一个含 `SKILL.md` 的文件夹，智能体可按简介选用并执行其中的说明或脚本 | `anthropics/skills` 里的 `pdf`、`google/skills` 里的 `gemini-api` |
| 提示词 | 单次对话里粘贴的说明，通常没有标准目录和渐进加载 | 任何聊天框里的临时指令 |
| Agent 框架 | 用来编排多步骤智能体的软件，本身不是一份技能 | 例如 Agents SDK（官方有一份**教你使用该框架**的技能，框架和技能仍是两层） |
| MCP 工具 | 对外系统和受控操作的接口（列表、调用、鉴权） | 插件里的 MCP 服务器；`mcp-builder` 则是「教你写 MCP 服务器」的 Skill，不是 MCP 本身 |
| 教程 / 规范 | 给人读的说明 | [agentskills.io/specification](https://agentskills.io/specification)、本指南 |

OpenAI 文档的分工可以记一句：MCP 提供实时数据、鉴权和受控动作；Skill 提供步骤、决策点、输出要求和模板。没有 MCP 时，技能也可以只靠说明和打包资源工作。

## 1. 一个优秀的 Skill 应该具备什么结构？

开放规范的最低要求只有一项：目录里有一份带 YAML frontmatter 的 `SKILL.md`。推荐（不是强制）再按用途放三类资源：

```
skill-name/                 # 目录名必须与 frontmatter 的 name 一致
├── SKILL.md                # 必填：name + description，以及被激活后才加载的指令
├── scripts/                # 可选：重复的、需要确定性的操作，写成可执行脚本
├── references/             # 可选：只在特定分支才需要的详细文档
├── assets/                 # 可选：模板、图片、数据文件，给输出使用，不必读进上下文
└── evals/evals.json        # 官方评测指南建议的测试用例位置，不是规范必填
```

Anthropic 的 `skill-creator` 把这三层叫做渐进披露，并给出可操作的体量感（原文是约数，允许必要时写得更长）：

1. 元数据（`name` + `description`）始终在上下文里，大约一百词量级。
2. `SKILL.md` 正文只在触发后进入上下文，理想情况下少于 500 行（规范另外建议少于约 5000 tokens）。
3. 打包资源按需加载；脚本可以执行而不必把源码读进上下文。量上几乎没有硬顶。

**对照真实官方技能：**

- `template-skill` 只有一份几乎空白的 `SKILL.md`，适合当骨架，本身还不是优秀技能。
- `pdf` 在主文件里只保留概览、快速开始和常用库，把高级说明放到 `REFERENCE.md`，把填表流程放到 `FORMS.md`，并把可重复的处理放到 `scripts/`。这是「主文件精瘦、细节按需」的生产级例子。
- `skill-creator` 把评测查看器、子代理说明和 schema 参考分到 `eval-viewer/`、`agents/`、`references/`，主文件负责流程导航。
- Google 的 `google-cloud-recipe-onboarding` 将主流程放在 `SKILL.md`，附加材料放在 `references/`。
- OpenAI 的 `openai-api-troubleshooting` 只有 49 行，再加 `references/` 与 `agents/`，说明「优秀」首先是结构清楚、边界清楚，不是篇幅长。

规范允许技能目录里出现推荐三文件夹之外的其他文件。作者讨论里有人担心这会让实现各不相同；写自己的技能时，仍应优先使用约定目录，并在 `SKILL.md` 里用相对路径、只往下指一层，避免参考文件再去指更深层参考。

## 2. 如何编写清晰、有效的 SKILL.md？

### Frontmatter：先让技能被认出来

规范的必填项只有 `name` 和 `description`。`name` 用小写字母、数字和连字符，不能首尾是连字符，不能出现 `--`，不能超过 64 字符，且必须等于目录名。

`description` 不超过 1024 字符，必须同时说明**做什么**和**何时用**，并带上有助于匹配的关键词。[Optimizing skill descriptions](https://agentskills.io/skill-creation/optimizing-descriptions) 还建议：用祈使语气（「在……时使用本技能」），写用户意图而不是内部实现，适当列出用户可能没说出领域名词的场合，并保持短到中等长度——它会进入启动时的技能清单。

可选字段按需添加，不要为了「看起来完整」全写上：

- `license`、`compatibility`、`metadata`（可放 `author`、`version`）：来自开放规范。
- `allowed-tools`：规范中的**实验性**字段，各客户端支持可能不同。
- 产品扩展（不要误当成规范必填）：Claude Code 的 `when_to_use`、`disable-model-invocation`、`user-invocable`、`disallowed-tools` 等；Cursor 的 `paths`、`icon`、`color`；OpenAI 的 `agents/openai.yaml`（例如 `allow_implicit_invocation`）。若技能要跨产品分发，先保证规范必填项正确，再按目标客户端加扩展字段。

注意一个已核对的差异：Claude Code 文档写「所有 frontmatter 字段都可选，只是强烈建议写 description」；开放规范则要求 `name` 与 `description` 必填。跨产品分发时按规范写全。

### 正文：只补模型缺的，并写清步骤与输出

[Best practices](https://agentskills.io/skill-creation/best-practices) 的核心是：有效技能来自真实任务、纠正和项目约定，而不是让模型仅靠通用知识生成一套「请妥善处理错误」式空话。正文应聚焦模型没有这份技能就不知道的东西：项目约定、领域步骤、非显而易见的边界、该用哪套工具。不必解释 PDF 是什么、HTTP 是什么。

`skill-creator` 的写作模式与官方指南一致：

- 指令用祈使语气。
- 需要固定输出时，给出明确模板。
- 用少量完整例子说明格式；例子要能推广，不要把技能写死在某一个文件名上。
- 尽量解释「为什么这样做」，而不是堆砌 `ALWAYS` / `NEVER`。官方评测指南也写：带理由的说明，往往比僵硬禁令更容易被稳定执行。
- 写完初稿后用新鲜视角删掉套话。

OpenAI 的技能文档要求正文说清：期望输入、步骤、用户应得到什么输出、哪些事实不得臆造、何时该提问 / 停止 / 拒绝、应查阅哪些附属文件。

Google 已读技能还有一个值得模仿的习惯：在 description 里用 “Don't use / Skip when” 把活交给兄弟技能，避免几个技能抢同一句话。`gemini-api`、`google-analytics-data-api-basics`、`finding-google-skills` 都是这样写的。

## 3. 如何让 Skill 准确触发？

触发几乎完全靠 `description`（加上产品里可能追加的 `when_to_use` 等）。启动时模型通常看不到正文。

官方指南里有一条容易被忽略的限制：对于模型用基本工具就能完成的一步请求（例如「读一下这个 PDF」），即使 description 匹配得很好，也未必会触发 PDF 技能。触发评测所用的查询，应该是「有技能会明显更稳」的任务，而不是「读文件 X」这种过轻的句子。

提高触发质量的做法（摘自官方优化指南，不是本批自创实验）：

1. 准备大约 20 条真实用户口吻的查询：8–10 条应当触发，8–10 条不应当触发。
2. 应当触发的句子要变化措辞、是否点名领域、细节多少和步骤复杂度。最有价值的是「技能用得上，但用户没把领域名词说出来」的句子。
3. 不应当触发的句子要用近邻干扰项，而不是风马牛不相及的句子。官方举的对比：对「CSV 分析」技能来说，「写一个斐波那契函数」几乎测不到边界；「改 Excel 预算表里的公式」「把 CSV 每一行上传到 Postgres」才是好的负例。
4. 每条查询跑多次（指南建议从 3 次起），算触发率；用训练集改写 description，用预先留出的验证集决定哪一版真正更好，避免把失败例句里的关键词逐个塞进 description。
5. 改完后再用从未参与优化的 5–10 条新查询做一次抽查。

官方给的改写示例：

```yaml
# 改前（过窄、过空）
description: Process CSV files.

# 改后（做什么 + 何时用 + 即使用户没说“CSV”）
description: >
  Analyze CSV and tabular data files — compute summary statistics,
  add derived columns, generate charts, and clean messy data. Use this
  skill when the user has a CSV, TSV, or Excel file and wants to
  explore, transform, or visualize the data, even if they don't
  explicitly mention "CSV" or "analysis."
```

如果某次交互需要「只有用户点名才运行」（例如危险操作、或只是一条斜杠命令），应使用产品提供的显式调用，并考虑 `disable-model-invocation: true`（Claude Code / Cursor）或 OpenAI `agents/openai.yaml` 里的 `allow_implicit_invocation: false`。这是触发策略，不是规范必填。

产品侧的排障步骤也可直接用：Claude Code 文档建议检查 description 关键词、询问「现在有哪些技能」、改写请求、或直接 `/skill-name`；若设置了 `paths`，还要确认当前文件落在匹配范围内。

## 4. 如何避免指令冗余？

冗余有两种，官方材料都警告过：

**把模型已经知道的常识写进去。** 最佳实践文档的反例就是从「PDF 是 Portable Document Format……」开始讲起。这会占用激活后的上下文，并和对话历史、系统提示、其他已激活技能抢注意力。

**把很少一起用到的分支全部堆进主文件。** 规范与 `skill-creator` 都要求：主文件接近 500 行时，增加一层，并写清「什么情况下读哪份文件」。互斥的领域（例如 AWS / GCP / Azure 的部署细节）应拆到 `references/` 下的分文件，让模型只读当前这一支。`pdf` 不把填表说明写进主文件，就是这个道理。

迭代时还要主动删。官方评测指南写：如果「有技能」的轨迹里出现大量无用校验或多余中间产物，就删掉那些指令；如果加规则后面分数不再提升，试着减规则，看结果是否仍然站得住。更少、更准的指令，常常优于一份穷尽的手册。

`skill-creator` 特别劝阻用大量 `ALWAYS` / `NEVER` 把技能收得很死，除非那是安全或格式上的硬约束（例如 OpenAI `openai-platform-api-key` 里「不要暴露明文密钥」这种规则，就应该写死）。

## 5. 如何管理大型 Skill 的参考资料？

原则就三句，都来自规范或 `skill-creator`：

1. 主 `SKILL.md` 只保留工作流、选择逻辑，以及「何时读哪份参考 / 何时跑哪个脚本」的指针。
2. 参考文件各自聚焦一个主题。单份很长（`skill-creator` 写的是超过 300 行）时，在文件开头加目录。
3. 用相对于技能根目录的路径，并且尽量只从 `SKILL.md` 指向一层。

Anthropic 工程文章用 PDF 技能说明：上下文几乎因此变得「容量不封顶」——不是一次读完，而是像手册的目录、章节、附录那样按需打开。脚本还可以充当「不必读进上下文的确定性工具」，例如先跑脚本抽出表单字段列表，再决定怎么填。

Google 的 `finding-google-skills` 则演示了另一种「大资料」：官方技能目录 `index.json` 大约数十 KB，正文要求必须取回未截断、未改写的原始 JSON，再在本地过滤。它把「大目录」留在仓库里按需下载，而不是复制进 `SKILL.md`。这是管理会增长的目录型资料时，值得模仿的做法。

`assets/` 放模板和要拷贝、要改写的文件，不必当作说明来读。脚本的依赖应写在脚本自身或 `compatibility` 里，不要假设运行环境什么都有：Google 入门技能和 Analytics 技能都会在缺少 `gcloud` 时要求先提示安装。

## 6. 如何设计可复用的工作流程？

可复用，首先是「一份技能只服务一个可识别的用户目标」。OpenAI 文档写：触发条件、输入或成功标准不同，就拆成不同技能。Google 用 description 里的 Don't use 完成同样的拆分。

其次，把工作流写成可检查的步骤，而不是一段散文。官方最佳实践对「会改文件或做破坏性操作」的任务，建议 **计划 → 用脚本或对照表校验 → 再执行**。它用填 PDF 表单举例：先抽出字段清单，再写拟填值，校验名称和类型，失败就改，最后才真正写入。关键是第 3 步那个校验脚本，要能告诉模型「哪个字段名不存在、可用字段有哪些」。

已读官方技能里可直接观察的工作流写法：

- `google-cloud-recipe-onboarding`：先检查本机工具，再认证、选项目、校验账单，然后才链式进入后续技能，并单独写 Validation Logic。
- `skill-creator`：抓意图 → 写草稿 → 跑测试 → 和人一起看结果 → 改写 → 必要时再优化 description。
- `analyze-data-quality`（`openai/plugins` 示例）：先规定相关技能，再进入工作流和分级标准，最后给出输出规范。
- `agents-sdk`：Intake、Build、Eval、Deploy，并以 Done Criteria 收尾。

脚本方面，官方 [Using scripts](https://agentskills.io/skill-creation/using-scripts) 要求：不要交互式提问（智能体无法回答 TTY 提示，脚本会一直挂起）；用参数、环境变量或 stdin 取输入；提供简洁的 `--help`；错误信息写清期望值；结构化结果走 stdout，进度和警告走 stderr；尽量幂等；破坏性操作提供 `--dry-run` 或显式确认；输出过大时默认给摘要或分页，以免被工具输出截断。

如果每次评测里模型都在现场重写同一个辅助脚本，官方建议：这说明该把脚本固化进 `skills/scripts/`。

## 7. 如何测试 Skill 的实际效果？

把测试分成两件独立的事，Google 的工程博文和开放规范的两份指南都是这样分的：

1. **有没有被选中**（触发评测，见第 3 节）。
2. **选中之后做得好不好**（输出评测）。

输出评测的官方最小起步是：在 `evals/evals.json` 里先放 2–3 个真实提示词、成功标准，以及可选的输入文件。不必一上来就设计完备断言；先跑，再根据实际输出补检查项。提示词要换措辞和详细程度，并至少覆盖一个边界情况。

每次测试建议跑两遍：有该技能，以及没有技能（或上一版本）。官方工作区结构是 `iteration-N/eval-.../with_skill|without_skill/`，里面放输出、耗时和评分。改进时要推广问题，而不是只为某一条测试加补丁。`skill-creator` 还支持盲比两个输出。

Google 2026-10-28 博文把这套做法产品化：每次行为变更都要带评估报告；新技能对比「未安装该技能的智能体」，改技能对比上一版本。他们还用确定性门禁（结构、lint、链接、版本号）挡下明显坏变更，再跑昂贵的模型评估。你可以在自己的仓库里采用同样的分层，不必一开始就上完整 CI。

本批没有代替你跑这些评测。上面是官方方法，不是本库实测分数。

## 8. 如何防止 Skill 出现错误行为？

从已读材料里，可以归纳成可执行的几条：

- **写清不得臆造、必须停下来提问的情形。** OpenAI 文档把这一点列为技能边界的一部分；其官方示例 `tabletop-dice` 写明：除非用户要求，否则不得发明、替换或重掷结果。`finding-google-skills` 把「截断的目录、错误页、证书失败」明确标成失败，而不是让模型凭记忆补全目录。
- **用校验门挡住执行。** 填表、改基础设施、改账单之前，先对照事实源检查计划。
- **用「不要用于」划界**，减少技能在错误任务上自信地乱走。
- **从真实失败里回写技能。** Anthropic 工程文章建议：先看智能体在哪些任务上卡住，再增量补技能；观察它是否过度依赖某一段上下文；跑偏时让它复盘，把成功路径和常见错误写回去。
- **解释原因，但把安全规则写死。** 例如密钥不得进入明文输出，这类规则不应写成「尽量注意」。
- **不要用技能去做让用户吃惊的事。** `skill-creator` 的 Principle of Lack of Surprise：技能里不得包含恶意软件、利用代码，或协助未授权访问、数据外泄；技能的实际行为应与它所宣称的意图一致。

## 9. 如何设计安全的文件和工具权限？

这一点必须写清楚：**开放规范不能代替你对运行环境的权限控制。** `allowed-tools` 仍是实验性字段，社区里还出现过不同写法、不同客户端解析不一致的讨论。不能假设写了 `allowed-tools` 就在所有产品里生效。

已核对的产品级做法：

- **Claude Code**：`allowed-tools` 可在该技能被调用的这一轮里预批准工具，下一条消息后清除；`disallowed-tools` 可在技能活跃时拿掉某些工具。另外还可用权限规则允许或拒绝 `Skill(...)` 这类调用。文档提醒：只从信任来源安装。
- **Cursor**：用 `paths` 把技能限制在匹配的文件上，降低它在无关目录里出主意的机会。`disable-model-invocation` 可禁止自动启用。
- **OpenAI**：把需要受控动作的部分放到 MCP（鉴权与授权在服务端），技能只描述调用顺序。`openai-platform-api-key` 把「先检查、再询问、永不暴露明文」写成强制步骤。
- **脚本**：避免交互式提权；破坏性操作要显式标志；不要在技能里要求连接不明外部地址。Anthropic 工程文章写：恶意技能可能在环境中引入漏洞，或驱使模型外泄数据。安装前通读文件，尤其是脚本、依赖，以及会发起网络请求的指令。只从信任来源安装。

一条实用规则：技能可以建议命令，但把「能否写文件、能否访问网络、能否花费云资源」留给客户端的权限系统和用户确认。Google 入门技能把账单绑定做成显式步骤，就是在承认：技能一旦执行，可能产生真实费用。

## 10. 如何让 Skill 方便维护和升级？

规范本身尚未版本化，也没有官方的技能 `version` 字段；若要标记版本，官方示例是放在 `metadata.version` 里。Google 已读技能普遍带有 `metadata.version`（例如 `finding-google-skills` 为 `1.1.0`，`gemini-api` 为 `1.0.4`）。2026-10-28 博文要求：**行为变更必须提高版本号**，并把版本检查做成合并门禁。

可复用的维护习惯：

- 一次只改一类行为，并留下对照评测（有/无技能，或新旧版本）。
- 链接要检查。Google 博文把链接校验同时放在合并时和定期任务里。
- 用语义化版本表达「这次是否改变了智能体的行为」，而不是只改措辞却不留记录。
- 分发渠道要选对并锁住来源：Google 官方用 `npx skills add` / `update`；Anthropic 用插件市场；OpenAI 用插件目录。不要一边用已弃用的 `openai/skills`，一边以为自己跟的是现行官方源。
- 跨产品字段放在扩展位置，避免为了一个客户端把技能写成无法被其他客户端解析的格式。
- 许可证写在技能目录里（Anthropic 文档技能用 `license: Complete terms in LICENSE.txt`）。不要假设单仓库根许可证覆盖每一个子技能；OpenAI 的 `openai-developers` 在清单里声明 Proprietary，尤其不能想当然地再分发。

## 优秀设计与糟糕设计对照

以下对照都锚定已读来源，不是虚构的「最佳实践清单」。

| 问题 | 较差（或应避免） | 较好（已在官方材料中出现） |
| --- | --- | --- |
| description 过空 | 规范反例：`Helps with PDFs.` | 规范正例：写清提取、填表、合并，以及用户提到 PDF / 表单时就用 |
| description 只有实现细节 | 「运行 `foo.py` 处理输入」 | 官方建议写用户意图；脚本名放正文 |
| 边界不清 | 多个技能都写「和数据有关就用我」 | `gemini-api`、Analytics 技能用 Don't use 把活交给兄弟技能 |
| 主文件膨胀 | 把所有语言、所有边缘情况写进一份 2000 行的 `SKILL.md` | `pdf` 把 FORMS / REFERENCE 拆走；多云细节按文件拆分 |
| 触发测试太容易 | 负例用「今天天气怎么样」 | 用共享关键词但目标不同的近邻请求 |
| 过拟合 | 把某次失败提示词里的独特文件名写进 description | 官方要求针对类别做推广，并用验证集选拔版本 |
| 空泛指令 | 「请遵循最佳实践并妥善处理错误」 | 来自真实任务的纠正、约定和失败案例（Best practices） |
| 破坏性操作直接执行 | 一上来就改文件、调云 API | 计划 → 校验 → 执行；缺 `gcloud` 先停下来让用户安装 |
| 脚本设计 | 交互式提问、错误只说 invalid input | 无 TTY 提问、`--help`、把期望值写进报错、stdout/stderr 分离 |
| 安全 | 把来路不明的技能连同脚本一起装上就用 | 只从信任源安装；先审计；密钥类技能禁止明文；MCP 负责受控动作 |
| 维护 | 改了行为却不留版本、不跑对照 | Google 的「行为变更必须升版本 + 评估报告」 |

## 可复用模板

下面是可以复制后改写的骨架，字段含义以开放规范为准。尖括号需要换成你的真实内容。

### 目录骨架

```
<skill-name>/
├── SKILL.md
├── scripts/           # 没有确定性步骤可先不建
├── references/
├── assets/
├── evals/
│   ├── evals.json
│   └── files/         # 测试用输入，可选
└── LICENSE.txt        # 若许可不写在 frontmatter 里
```

### SKILL.md 骨架

```markdown
---
name: <skill-name>
description: >
  <用一两句话说清本技能做什么。>
  Use when <用户会怎样描述这件事，包括没说出术语的情况>。
  Don't use for <应交给其他技能或应拒绝的邻近任务>。
license: <Apache-2.0 或 Complete terms in LICENSE.txt>
# compatibility: <仅当确有环境要求时再写，最多 500 字符>
metadata:
  author: <your-name-or-org>
  version: "0.1.0"
# allowed-tools: <实验性字段，确认目标客户端支持后再写>
---

# <标题>

<一段话说明目标，以及成功时用户应拿到什么。>

## 何时使用 / 何时不用

- 使用：<两条以上真实说法>
- 不用：<邻近但目标不同的任务>

## 前置条件

- 缺少 <工具或凭证> 时，先说明如何安装或登录，不要假装环境已就绪。

## 工作流

1. <收集输入；不确定就提问，不要臆造>
2. <如有破坏性或批量操作：先写出计划并校验>
3. <执行：需要确定性时运行 `scripts/...`，需要细节时阅读 `references/...`>
4. <按下面的输出格式交付，并列出限制或未验证项>

## 可用脚本与参考

- `scripts/<name>`：<何时运行，输入输出是什么>
- `references/<name>.md`：<何时阅读，不要提前整份读入>

## 输出格式

<给出小标题模板，或一个短例子。>

## 安全与拒绝条件

- 不得 <臆造数据、暴露密钥、连接未说明的外部地址等>。
- 出现 <某类风险> 时停止并询问用户。
```

### 触发评测查询骨架

```json
[
  {"query": "<应当触发：口语化、带真实文件路径或背景>", "should_trigger": true},
  {"query": "<应当触发：没说出术语，但目标明显属于本技能>", "should_trigger": true},
  {"query": "<不应当触发：共享关键词，但其实是另一件事>", "should_trigger": false}
]
```

### 输出评测用例骨架（官方指南中的 `evals/evals.json` 形态）

```json
{
  "skill_name": "<skill-name>",
  "evals": [
    {
      "id": 1,
      "prompt": "<真实用户会打出的那句话>",
      "expected_output": "<人能看懂的成功标准，而不是一句‘做得很好’>",
      "files": ["evals/files/<optional-input>"]
    }
  ]
}
```

先用这份技能跑一遍，再用不装它的同一模型跑一遍，对比后再改 `SKILL.md`。不要把「看起来像那么回事」当成评测结果。

## 附录：非官方、但谈设计方法时可能遇到的项目

下列项目**不是**某一家模型平台的官方技能包，本批也不把它们写入「官方 Skills」推荐安装名单。只有在讨论「怎样迭代技能文本」时作为方法线索：

- [Microsoft SkillOpt](https://github.com/microsoft/SkillOpt)：把技能文档当作可训练参数，用轨迹驱动修改，并在验证集提升后才接受，导出可部署的技能文本。方法上接近「评测门禁 + 迭代改写」，但是研究/工具项目，不是官方平台目录。
- [obra/superpowers](https://github.com/obra/superpowers)：一套可安装的技能工作流与方法论。它也出现在 `openai/plugins` 的示例目录名单里，但这只说明该官方示例仓库收录了它，**不等于**它变成 OpenAI 第一方技能包。对它的源码与质量评估留给后续非官方批次。

根目录简报里对这两项的项目级介绍仍然有效，需要引用时请看那篇，不要在本目录复制。

## 元数据

- 更新时间：2026-11-25（Asia/Shanghai）
- 来源：
  - [Agent Skills Specification](https://agentskills.io/specification) 及 [best practices](https://agentskills.io/skill-creation/best-practices)、[optimizing descriptions](https://agentskills.io/skill-creation/optimizing-descriptions)、[evaluating skills](https://agentskills.io/skill-creation/evaluating-skills)、[using scripts](https://agentskills.io/skill-creation/using-scripts)
  - 已打开的官方技能：Anthropic `skill-creator`、`pdf`、`template`；Google `finding-google-skills`、`google-cloud-recipe-onboarding`、`gemini-api`、`google-analytics-data-api-basics`；OpenAI `openai-platform-api-key`、`openai-api-troubleshooting`、`agents-sdk`、`evaluate-skill`、`analyze-data-quality`
  - [Equipping agents for the real world with Agent Skills](https://www.anthropic.com/research/equipping-agents-for-the-real-world-with-agent-skills)
  - [How we ship Google Agent Skills like products](https://cloud.google.com/blog/topics/developers-practitioners/behind-the-scenes-two-months-later-how-we-ship-google-agent-skills-like-products)（2026-10-28）
  - [Claude Code Skills](https://code.claude.com/docs/en/skills)、[Cursor Agent Skills](https://cursor.com/docs/skills)、OpenAI Build skills 文档（后者 curl 复查 403，见官方 Skills 笔记）
- 信息可信度：部分核对。设计规则已对照上述官方文本和已读 `SKILL.md`；模板是按规范重组的骨架，不是某一个官方文件的逐字拷贝；本批没有实际跑触发评测或输出评测；`allowed-tools` 的跨客户端行为未实测。
- 平台：以开放规范为基准；产品扩展字段已标明来源，未实测跨客户端兼容。
- 技能门槛：会编辑 Markdown 和 YAML；若要做官方建议的评测，还需能在终端里运行相应客户端或脚本。
- 费用：阅读本指南无需付费。运行评测会消耗所使用模型或云产品的额度，具体价格未知。
