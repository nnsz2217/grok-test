# Agent Skills 开放规范

这是目前多数官方 Skills 仓库共同遵守的开放格式说明，不是一份可以「安装」的技能包。它回答的是：一个 Skill 目录里必须有什么、可选什么，以及智能体如何按需加载。

## 它究竟是什么

Agent Skills 把可复用的专业知识和工作流程，打包成一个带 `SKILL.md` 的文件夹。智能体先只看到技能的名称和简介，匹配到任务后再读取完整说明，需要时再去执行脚本或打开参考文件。规范由 Anthropic 提出并开源，现由 [agentskills/agentskills](https://github.com/agentskills/agentskills) 维护，文档站点是 [agentskills.io](https://agentskills.io)。

它不是：提示词合集、Agent 框架，也不是 MCP 工具目录。MCP 负责对外系统和受控操作；Skill 负责「何时、按什么步骤、用哪些已有工具把一件事做完」。

## 真实目录结构（来自规范原文）

规范要求一个技能至少是如下目录，其中只有 `SKILL.md` 是必须的：

```
skill-name/
├── SKILL.md          # 必填：YAML 元数据 + Markdown 指令
├── scripts/          # 可选：可执行代码
├── references/       # 可选：按需阅读的文档
├── assets/           # 可选：模板、图片、数据文件
└── ...               # 还可以有其他文件或目录
```

`SKILL.md` 必须先写 YAML frontmatter，再写正文。规范里**必填**只有两项：

| 字段 | 是否必填 | 约束（摘自规范） |
| --- | --- | --- |
| `name` | 是 | 最长 64 字符；只能用小写字母、数字和连字符；不能以连字符开头或结尾；不能出现连续连字符；必须与父目录名一致 |
| `description` | 是 | 最长 1024 字符；非空；说明技能做什么、何时该用 |
| `license` | 否 | 许可证名称，或指向随附许可证文件 |
| `compatibility` | 否 | 最长 500 字符；环境要求（产品、系统软件包、网络等）。多数技能不需要这项 |
| `metadata` | 否 | 字符串到字符串的映射，用来放规范未定义的额外信息（例如 `author`、`version`） |
| `allowed-tools` | 否 | **实验性**字段：空格分隔的预批准工具列表。各客户端支持情况可能不同 |

规范给出的最小例子：

```markdown
---
name: skill-name
description: A description of what this skill does and when to use it.
---
```

带可选字段的例子里，`version` 写在 `metadata` 下，而不是独立的规范字段：

```markdown
---
name: pdf-processing
description: Extract PDF text, fill forms, merge files. Use when handling PDFs.
license: Apache-2.0
metadata:
  author: example-org
  version: "1.0"
---
```

注意：规范目前**没有**独立的 `version` 字段，也没有规范自身的版本号或正式 changelog。仓库在 2026-11-25 查询时没有 Git 标签或 Release。技能作者可以在 `metadata.version` 里自己标记版本，但不能把它理解成可以跨客户端锁定的「规范 1.0」。

## 渐进披露（触发机制）

规范把加载分成三层，这也是「如何让技能被准确用上、又不撑爆上下文」的核心：

1. **元数据（约 100 tokens）**：启动时只加载各技能的 `name` 和 `description`。
2. **指令（建议少于 5000 tokens）**：技能被激活后，才读入整个 `SKILL.md` 正文。
3. **资源（按需）**：`scripts/`、`references/`、`assets/` 等只在需要时加载；脚本还可以执行而不必把源码读进上下文。

规范建议把主 `SKILL.md` 控制在 500 行以内，把详细参考拆到单独文件。引用其他文件时用相对路径，并且尽量只从 `SKILL.md` 指一层，避免层层嵌套。

## 写作规则（规范原文中的好坏对比）

规范要求 `description` 同时写清「做什么」和「何时用」，并带上有助于匹配任务的关键词。

- 较好的写法（规范示例）：`Extracts text and tables from PDF files, fills PDF forms, and merges multiple PDFs. Use when working with PDF documents or when the user mentions PDFs, forms, or document extraction.`
- 较差的写法（规范示例）：`Helps with PDFs.`

无效的 `name` 示例包括：`PDF-Processing`（大写）、`-pdf`（以连字符开头）、`pdf--processing`（连续连字符）。

正文格式没有强制模板。规范建议写：分步说明、输入输出例子、常见边界情况。

校验可用参考实现：

```bash
skills-ref validate ./my-skill
```

该命令检查 frontmatter 是否合法，以及命名约定。工具在规范仓库的 `skills-ref/` 目录。本批没有在本地实际跑过这条命令。

## 官方还提供哪些写作指南

同一站点还有面向技能作者的补充文档，不是规范条款本身，但对「怎样写好」更具体：

- [Best practices for skill creators](https://agentskills.io/skill-creation/best-practices)：从真实任务和项目材料提炼技能；不要让模型只靠通用知识空写；少写模型已经知道的常识，多写项目约定和非常识性边界；破坏性操作采用「计划—校验—再执行」。
- [Optimizing skill descriptions](https://agentskills.io/skill-creation/optimizing-descriptions)：用大约 20 条正/负向真实提示词测试触发，跑多次算触发率，并把训练集和验证集分开，避免为某一句提示词「过拟合」。
- [Evaluating skill output quality](https://agentskills.io/skill-creation/evaluating-skills)：在 `evals/evals.json` 里放测试用例，对「有技能 / 无技能」或新旧版本做对照，再按断言打分并迭代。
- [Using scripts in skills](https://agentskills.io/skill-creation/using-scripts)：脚本不要交互式提问；提供 `--help`；错误信息要写清期望值；结构化输出走 stdout、诊断信息走 stderr；破坏性操作考虑 `--dry-run` 或明确确认标志。
- [Client Showcase](https://agentskills.io/clients)：声称展示支持该格式的产品。本环境打开该页时只看到标题和排序控件，产品名单由页面脚本渲染，**未能从该页核对完整客户端列表**。已在各厂商自己的文档里核对到的支持情况，见本目录其他笔记。

## 适用平台、安装与费用

- **类别**：开放规范 / 文档与参考实现，不是安装包。
- **平台**：任何声称兼容 Agent Skills 的客户端。具体行为以各产品文档为准；扩展字段（例如某些产品的 `paths`、`disable-model-invocation`）不属于这份规范的必填部分。
- **安装**：不需要安装规范本身。若要校验技能，需按仓库说明使用 `skills-ref`。具体安装步骤本批未实际执行。
- **是否需要 API Key / 付费**：阅读规范和仓库源码不需要。在某个产品里使用技能，通常还要有该产品的账号或额度，费用以各产品为准，此处不编造价格。
- **技能门槛**：能阅读英文文档、会编辑 Markdown 和 YAML。运行 `skills-ref` 需要按仓库说明准备开发环境。
- **开源许可证**：仓库代码为 Apache-2.0；文档为 [CC-BY-4.0](https://creativecommons.org/licenses/by/4.0/)。来源：仓库 README。
- **维护状态**：未归档。GitHub API 显示默认分支 `main`，最近一次推送 `2026-11-04T19:47:27Z`（换算为 2026-11-05 03:47，Asia/Shanghai）。2026-11-25（Asia/Shanghai）查询时 star 数为 27,616，fork 2,074。star 只是当天快照，不代表质量排名。

## 优点和局限

优点：格式简单，跨产品复用的基础就是同一个文件夹；渐进披露把「能装很多技能」和「上下文不被一次性塞满」分开处理；官方写作指南已经覆盖触发测试和输出评估。

局限：规范本身尚未版本化，实施细节（尤其是实验性的 `allowed-tools`）在不同客户端上可能不一致；`metadata.version` 只是作者自标，不能当成跨工具的锁定机制；Client Showcase 页在本环境无法核出完整名单。

## 元数据

- 更新时间：2026-11-25（Asia/Shanghai）
- 来源：
  - [Agent Skills Specification](https://agentskills.io/specification)
  - [agentskills/agentskills 仓库 README](https://github.com/agentskills/agentskills)
  - [Best practices](https://agentskills.io/skill-creation/best-practices)、[Optimizing descriptions](https://agentskills.io/skill-creation/optimizing-descriptions)、[Evaluating skills](https://agentskills.io/skill-creation/evaluating-skills)、[Using scripts](https://agentskills.io/skill-creation/using-scripts)
  - GitHub API `https://api.github.com/repos/agentskills/agentskills`（2026-11-25 查询：stars、license、pushed_at、是否归档）
- 信息可信度：已核对（规范正文、仓库 README 与 API 元数据已打开；Client Showcase 产品名单未能从该页核出，已在正文标明）
- 平台：跨客户端开放格式；已核对的具体产品见本目录其他笔记
- 技能门槛：能阅读英文规范并编辑 Markdown / YAML
- 费用：规范与仓库源码免费阅读（Apache-2.0 / CC-BY-4.0）；在具体产品中使用技能的费用未知，以各产品为准
