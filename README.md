# nnsz2217 的个人 AI 知识与工具库

这个仓库是 [nnsz2217](https://github.com/nnsz2217) 的个人 AI 知识与工具库。用来存放已经核对过的 Skills、提示词、工具用法、可直接使用的 Agent、自动化工作流，以及前沿动态笔记。

知识库的七个分类目录已经建立。第一批研究（官方 Skills 与 Skill Engineering）已经写入 [skills/](skills/)。其余分类目前仍主要是索引，主题笔记会按后续批次补入，不在索引页里编造内容。

## 面对一个任务时怎么用

先判断手头缺的是哪一类材料，再打开对应目录：

1. **要一套可复用的能力或写法** → [skills/](skills/)。找开源 Skill、官方 Skill，或 Skill 的编写与工程方法。若要先看官方来源：从 [skills/official-skills/](skills/official-skills/) 进入规范与各厂商仓库；若要自己写技能：看 [Skill Engineering 技术指南](skills/skill-engineering/guide.md)，并保留根目录那篇 [生态简报](ai-skill-engineering-guide.md) 作对照。推荐安装顺序见 [skills/recommended-skills.md](skills/recommended-skills.md)。
2. **要一段能直接改的提示词** → [prompt-engineering/](prompt-engineering/)。找设计方法、复杂任务、结构化输出、长任务、优化测试和可复制案例。
3. **要某个产品的高级用法** → [ai-tools/](ai-tools/)。按 ChatGPT、Codex、Grok、DeepSeek、Claude、Gemini 等工具进入。
4. **要一个拿来就能用的 Agent** → [ai-agents/](ai-agents/)。优先浏览器、桌面、搜索、文档和个人效率。
5. **要把一件事做成可重复的流程** → [automation/](automation/)。
6. **要知道最近出现了什么** → [ai-frontier/](ai-frontier/)。记新模型、新功能、新工具和重要突破。
7. **要跨分类的文档、教程或本库约定** → [resources/](resources/)。

一篇笔记只放在一个目录里。任务跨了两类时，在另一份索引上加链接，正文不复制。

## 目录

| 目录 | 收录什么 | 当前状态 |
| --- | --- | --- |
| [skills/](skills/) | 全球 AI Skills 生态：开源 Skills、官方 Skills、Skill Engineering、可复用编写方法、平台兼容性 | 第一批已入库：官方 Skills、Skill Engineering 指南、推荐分级。开源合集与分类专题、完整跨平台比较尚未检索 |
| [prompt-engineering/](prompt-engineering/) | 高级提示词：设计方法、复杂任务、结构化输出、长任务、优化与测试、可复制案例 | 仅索引，尚无主题笔记 |
| [ai-tools/](ai-tools/) | ChatGPT、Codex、Grok、DeepSeek、Claude、Gemini 等工具的高级用法 | 仅索引，尚无主题笔记 |
| [ai-agents/](ai-agents/) | 可直接使用的实用 Agent（浏览器、桌面、搜索、文档、个人效率），重实际价值 | 仅索引，尚无主题笔记 |
| [automation/](automation/) | 可复用的 AI 自动化工作流 | 仅索引，尚无主题笔记 |
| [ai-frontier/](ai-frontier/) | 新模型、新功能、新工具与重要突破，不深挖底层实现 | 仅索引，尚无主题笔记 |
| [resources/](resources/) | 跨分类的官方文档、教程、目录与约定 | 索引已建立；含笔记约定，尚无外部资料汇编 |

## 已完成的研究笔记

- [AI Skill Engineering / Agent 工具开发简报](ai-skill-engineering-guide.md)

  这是本库第一篇完成的研究笔记，保留在仓库根目录，已有链接可以继续使用。检索截止 2026-11-25（Asia/Shanghai）。它按规范、方法论、训练、安装工具、工程教程整理了五条 Skill Engineering 材料，文末附两篇对照文章和 MCP Tools 规范作为背景。具体仓库、日期和热度以该文自己的核对为准。[skills/](skills/) 只链接到它，不另存副本。

- [Skill Engineering 技术指南（第一批）](skills/skill-engineering/guide.md)

  与上一篇简报互补：按「如何写、如何触发、如何测、如何维护」展开，并附可复制模板。依据官方规范和已读官方 `SKILL.md`，不替换根目录简报。

- [官方 Skills 索引](skills/official-skills/)

  第一批核对的第一方来源：开放规范、Anthropic、Google、OpenAI（含已弃用的 `openai/skills` 说明）、Cursor 内置技能，以及安装 Google 官方技能用到的 `npx skills` CLI。

- [第一批推荐与分级](skills/recommended-skills.md)

  只对第一批已核实材料做 A/B/C/D 分级，不是开源技能总榜。

## 使用约定

- **优先改已有文件。** 同一主题已经有笔记时，更新那份文件，并改它的更新时间。只有独立的新主题才新建文件。
- **每篇笔记都要带元数据。** 来源链接、更新时间（时区 Asia/Shanghai）、信息可信度。适用时再写平台、技能门槛，以及免费 / 付费 / API 费用。费用只写已经核对到的，不知道就标明未知。细则见 [resources/conventions.md](resources/conventions.md)。
- **通过 Pull Request 进入 `main`。** 不要直接推送到 `main`。
- **研究按批次入库。** 以后的开源 Skills 合集、提示词库、工具深挖、Agent 写法、自动化流程和前沿笔记会分批提交。第一批只覆盖官方 Skills 与 Skill Engineering。

## 元数据

- 更新时间：2026-11-25（Asia/Shanghai）
- 来源：仓库既有结构；第一批研究笔记见 `skills/official-skills/`、`skills/skill-engineering/guide.md`、`skills/recommended-skills.md`；根目录 `ai-skill-engineering-guide.md` 本批未改
- 信息可信度：目录状态已按第一批成果更新。各主题事实以对应笔记自己的核对范围为准；除 `skills/` 第一批外，其他分类内容仍待后续研究补充
