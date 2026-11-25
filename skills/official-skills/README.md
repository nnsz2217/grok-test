# 官方 Skills

本目录收录**平台或厂商第一方**的 Skill 规范、公开技能仓库、产品内置技能说明，以及安装官方技能时必需提到的工具。这里不把社区 awesome 清单、非官方合集或普通提示词算作「官方 Skills」。

阅读顺序建议：先看开放规范，再按你实际使用的产品打开对应仓库笔记。若要用 `npx skills add` 安装 Google 官方技能，再看安装工具那一篇，以免把它误认为又一个技能包。

## 当前内容

- [Agent Skills 开放规范](agent-skills-specification.md)

  技能文件夹的标准格式、必填字段、渐进披露和官方写作指南入口。这是规范，不是安装包。

- [Anthropic 官方 Skills 与 Claude Code 内置技能](anthropics-skills.md)

  `anthropics/skills` 仓库结构、Claude Code 插件市场安装说明，以及本批实际打开过的 `skill-creator`、`pdf` 等 `SKILL.md`。另记录文档中列出、但未读到源码的 Claude Code 内置技能。

- [Google 官方 Agent Skills](google-skills.md)

  `google/skills` 的安装与更新、`index.json` 在 2026-11-25 核到的 219 个技能，以及已读的 `finding-google-skills` 等四份正文。附带 README 列出的其他 Google 官方技能仓库（仅核元数据）。

- [OpenAI 官方继任来源 Plugins，以及已弃用的 openai/skills](openai-plugins.md)

  现行示例仓库 `openai/plugins`、第一方插件 `openai-developers` 中已读技能，以及 2026-06 宣布弃用但仍未归档的旧目录。部分官方文档在本环境 curl 复查返回 403，文内已标明。

- [Cursor 官方 Skills 支持与内置技能](cursor-official-skills.md)

  官方文档中的目录约定、frontmatter 和内置技能表。未找到内置技能的公开 `SKILL.md` 仓库。

- [安装工具 npx skills（vercel-labs/skills）](skills-sh-cli.md)

  不是技能包。因 Google 官方 README 以 `npx skills add google/skills` 为安装入口，单独记录以免混淆。

## 本批明确不收入「官方技能包」的对象

- 社区 awesome 列表、独立开发者合集：留待后续批次。
- [Microsoft SkillOpt](https://github.com/microsoft/SkillOpt)、[obra/superpowers](https://github.com/obra/superpowers)：不是平台官方技能包。设计方法仅在 [Skill Engineering 指南](../skill-engineering/guide.md) 附录提及。
- MCP 服务器、Agent 框架、单次提示词：不属于本目录。

## 尚未检索、尚未核实

- [ ] 对 `google/skills` 其余技能、`openai/plugins` 中非已读插件、Anthropic 仓库中未打开的示例技能做源码级阅读
- [ ] 在 Claude Code、Codex、Cursor、Gemini CLI 上实际安装并调用
- [ ] 完整核对 Agent Skills Client Showcase 产品名单（该页在本环境几乎只有脚本渲染的外壳）

## 元数据

- 更新时间：2026-11-25（Asia/Shanghai）
- 来源：本目录各主题笔记（各文自行列出原始链接）
- 信息可信度：本页是索引。各项目的核对范围与未核实项，见对应笔记文末
- 平台：不适用（索引页）
- 技能门槛：不适用（索引页）
- 费用：不适用（索引页）
