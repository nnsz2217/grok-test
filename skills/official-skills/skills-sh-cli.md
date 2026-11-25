# 安装工具：npx skills（vercel-labs/skills / skills.sh）

这不是官方技能合集，而是一个用于发现、安装、更新 Agent Skills 的命令行工具。把它单独记下，是因为 Google 官方仓库的安装说明直接依赖它：`npx skills add google/skills`。不要在技能目录里把它当成「又一个可安装的官方 Skill 包」。

## 基本信息

- **名称**：skills（CLI for the open agent skills ecosystem）
- **网站**：[skills.sh](https://skills.sh)（2026-11-25 复查，站点会落到 `https://www.skills.sh/`，HTTP 200）
- **GitHub**：[github.com/vercel-labs/skills](https://github.com/vercel-labs/skills)
- **作者**：Vercel Labs（README 带 Vercel Labs Product 标识）
- **开源许可证**：MIT（GitHub API SPDX 与 README 徽章一致）
- **最近推送**：`2026-11-17T00:58:04Z`（2026-11-17 08:58，Asia/Shanghai）。未归档。
- **最新 Release**：GitHub Releases API 返回 **v1.9.0**，`published_at: 2026-11-16T10:28:13Z`（2026-11-16 18:28，Asia/Shanghai），页面：https://github.com/vercel-labs/skills/releases/tag/v1.9.0
- **热度快照**：2026-11-25 查询时 40,813 stars、3,608 forks。

## 它做什么

README 的定位是：给支持 Agent Skills 的编码智能体安装可复用说明。它把技能装进当前项目（默认）或用 `-g` 装到全局，并用自己的命令做查找、更新、删除。它**不负责**推理期的技能路由——装好之后，仍由各智能体按 `name` / `description` 决定是否加载。

README 写明需要 **Node.js 22.20 或更高版本**。常用命令（均摘自 README，本批未实际执行）：

```bash
npx skills add vercel-labs/agent-skills
npx skills add vercel-labs/agent-skills --skill web-design-guidelines -a claude-code
npx skills find
npx skills list
npx skills update
npx skills remove
npx skills init [name]
```

Google 官方技能的安装命令是 `npx skills add google/skills`，见 [google-skills.md](google-skills.md)。

README 还提到实验性命令（如 `experimental_sync`、`experimental_install`），名称和行为可能随时改变。不要把实验性命令写成稳定工作流。

关于支持哪些智能体：README 写 “Supports OpenCode, Claude Code, Codex, Cursor, and 75 more”，并指向仓库内 `docs/agents.md`。本批没有打开那份完整名单，不转述 75 个名字。

## 和本批其他材料的关系

| 对象 | 关系 |
| --- | --- |
| 开放规范 | 本工具安装符合 Agent Skills 格式的文件夹，不替代规范 |
| google/skills | 官方 README 用它作为主安装入口 |
| anthropics/skills | Anthropic 官方主路径是 Claude Code 插件市场，不是必须用本 CLI |
| openai/plugins | OpenAI 官方主路径是 ChatGPT / Codex 的插件目录与 `$skill-installer` 等产品内机制 |
| 本工具 README 示例里的 `vercel-labs/agent-skills` | 那是 Vercel 的示例技能源，**不是本批要评测的官方平台技能包**，此处不展开 |

## 费用、Windows、门槛

- **费用**：CLI 源码为 MIT。通过它安装的具体技能，许可证与费用以该技能仓库为准。运行 `npx` 不另收本工具的许可费；是否需要 Node.js 环境由你本机准备。
- **Windows**：只要能安装符合版本要求的 Node.js 并运行 `npx`，命令形式相同。本批未在 Windows 实测。
- **技能门槛**：会在终端安装 Node.js 并运行 `npx` 即可；属于「简单配置」，不是编写技能。
- **安全**：它会把远程仓库中的技能（可能含脚本）装到你的项目或用户目录。只应从你信任的源安装，并先阅读即将装入的 `SKILL.md` 和脚本。这不是本工具独有的风险，但对「一键 add」特别重要。

## 元数据

- 更新时间：2026-11-25（Asia/Shanghai）
- 来源：
  - [vercel-labs/skills README](https://github.com/vercel-labs/skills)
  - [v1.9.0 Release](https://github.com/vercel-labs/skills/releases/tag/v1.9.0)
  - [google/skills README](https://github.com/google/skills)（安装命令依赖本工具）
  - GitHub API `https://api.github.com/repos/vercel-labs/skills`（2026-11-25）
- 信息可信度：部分核对。README、许可证、Release 与 star / 推送时间已核对；未实际运行 `npx skills`；未打开 `docs/agents.md` 完整客户端名单。
- 平台：命令行；README 声称支持多种编码智能体，完整名单待核实。
- 技能门槛：会安装 Node.js 22.20+ 并使用终端。
- 费用：CLI 为 MIT。被安装技能的许可证和运行费用另计。
