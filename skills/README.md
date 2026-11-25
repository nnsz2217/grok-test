# Skills

收录全球 AI Skills 生态里已经核对过的材料：开源 Skills、官方 Skills、Skill Engineering、可复用的编写方法，以及同一份 Skill 在不同平台上的兼容性。

这里放「能力如何被写成、装上、验收」的笔记。单次对话里的提示词放在 [prompt-engineering/](../prompt-engineering/)，某个聊天产品的界面用法放在 [ai-tools/](../ai-tools/)。

## 当前内容

- [AI Skill Engineering / Agent 工具开发简报](../ai-skill-engineering-guide.md)（仓库根目录，只链接，不复制）

  本库第一篇完成的研究笔记，检索截止 2026-11-25（Asia/Shanghai）。正文按五条材料组织：Agent Skills 开放规范、可安装的技能工作流、把技能文档当作可训练参数、技能的安装与锁定、把技能当产品发布的工程门禁。文末另附两篇对照文章和 MCP Tools 规范作为背景。仓库名、日期和热度以该文自己的核对为准；本索引没有重做那次检索。

- [Skill Engineering 技术指南（第一批）](skill-engineering/guide.md)

  与根目录简报互补的写法指南：结构、触发、评测、安全、维护，以及可复制的 `SKILL.md` 模板。依据 2026-11-25 已读的官方规范和官方技能原文。索引见 [skill-engineering/](skill-engineering/)。

- [官方 Skills](official-skills/)

  第一批已核对的第一方规范与仓库：开放规范、Anthropic、Google、OpenAI（含已弃用的旧目录说明）、Cursor 内置技能，以及安装 Google 官方技能时用到的 `npx skills` CLI。不要把该 CLI 当成技能包。

- [第一批推荐与分级](recommended-skills.md)

  只对第一批已核实的官方材料分级（A/B/C/D）。不是跨所有开源技能的总榜。

## 以后怎么加笔记

1. 和根目录那篇简报是同一主题时，直接改根目录的 `ai-skill-engineering-guide.md`，不要在本目录再写一份副本。
2. 独立新主题（例如某一类官方 Skills、一份编写方法、一组平台兼容性）才在本目录新建文件。
3. 文末按 [笔记约定](../resources/conventions.md) 写来源链接、更新时间（Asia/Shanghai）和信息可信度。
4. 回到本页「当前内容」，加上相对链接和一两句这篇覆盖什么，并更新本页的更新时间。
5. 通过 Pull Request 合并，不要直接推送到 `main`。

## 以后可能补的主题（尚未检索、尚未核实）

下面只是按本目录的收录范围留下的空位。没有链接，没有结论，不能当资料用。第一批已完成「各平台官方 Skills 分别提供什么」和「与根目录简报互补的写法笔记」中属于官方范围的部分；其余仍待后续批次。

- [ ] 开源 Skills 的目录与挑选方式（计划中的 awesome-skills 等，本批未建空目录）
- [ ] 办公、学习、研究、编程类可安装 Skills 专题整理
- [ ] 浏览器、自动化和创作类 Skills
- [ ] 同一份 Skill 在不同客户端上的兼容性（完整横向比较）
- [ ] `skill-comparison.md` 跨项目对比表（本批只有官方材料的推荐分级，不做全面对比）

建议的后续目录名（尚未创建，避免先放空文件夹）：`awesome-skills/`、`productivity/`、`research/`、`coding/`、`browser-automation/`、`creative/`。

## 元数据

- 更新时间：2026-11-25（Asia/Shanghai）
- 来源：仓库根目录现有文件 `ai-skill-engineering-guide.md`（内容未改，本页只作索引）；第一批新增笔记见 `skill-engineering/`、`official-skills/`、`recommended-skills.md`
- 信息可信度：索引已按第一批成果更新。所链简报的事实以该文件自身的核对日期为准，本页没有重新检索该简报。第一批各主题笔记的核对范围见其文末元数据。其余主题待后续研究补充
- 平台：不适用（索引页）
- 技能门槛：不适用（索引页）
- 费用：不适用（索引页）
