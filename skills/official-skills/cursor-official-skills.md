# Cursor 官方 Skills 支持与内置技能

Cursor 有第一方文档和一组**内置技能**，但本批没有找到类似 `anthropics/skills` 或 `google/skills` 那样、把内置技能以 `SKILL.md` 全文公开的官方目录仓库。因此本篇是「官方平台能力说明」，不是一份可克隆安装的技能包评测。内置技能的具体指令正文，本批未能打开。

## 基本信息

- **名称**：Agent Skills（Cursor 文档）
- **官方文档**：[cursor.com/docs/skills](https://cursor.com/docs/skills)（2026-11-25 复查 HTTP 200）
- **相关**：Changelog [2.4 Subagents, Skills, and Image Generation](https://cursor.com/changelog/2-4)（标注 2026-01-22）写明编辑器和 CLI 开始支持 Agent Skills。
- **作者 / 团队**：Cursor
- **类别**：官方平台文档 + 产品内置技能。不是开源技能合集。
- **许可证**：不适用（产品功能；文档页未提供可安装技能包的开源许可）。

## 它是什么，和普通对话有什么区别

文档把 Agent Skills 定义为开放标准上的可移植、可版本管理的能力包：技能可以带脚本、模板和参考资料，并按需加载。Cursor 启动时会从约定目录发现技能，由 Agent 根据上下文决定是否使用；也可以在 Agent 聊天里输入 `/` 按名称调用。用 `/` 调用的技能默认只附着在这一条消息上；若要在整段会话中保持开启，文档要求把它当作 Custom Mode，快捷键为 Mac 的 Option+Enter 或 Windows 的 Alt+Enter。

和始终生效的规则（Rules）相比，文档的定位是：技能更适合「按任务才需要的程序性说明」，以降低无关上下文。

## 内置技能（文档表格，非源码）

文档列出 Cursor 管理的一组内置技能，会和用户自行添加的技能一起出现。名称与文档中的说明如下（摘译说明，名称保持原文）：

| 技能 | 文档中的用途 |
| --- | --- |
| `/automate` | 创建由日程、Slack、GitHub 事件等触发的 Cursor Automations |
| `/autopilot` | 跟进 pull request：处理反馈、冲突、失败检查和后续工作 |
| `/canvas` | 创建可在对话旁渲染的交互式 React 产物 |
| `/create-hook` | 创建 Cursor hooks，并更新 `hooks.json` |
| `/create-rule` | 创建合适范围和说明的 Cursor rules |
| `/create-skill` | 创建 Agent Skills 及其目录和 `SKILL.md` |
| `/create-subagent` | 创建自定义子代理 |
| `/cursor-blame` | 调查 AI 写出的改动及其提示词 |
| `/loop` | 按指定间隔重复执行一段提示词或技能 |
| `/migrate-to-skills` | 把符合条件的动态规则和斜杠命令改写成 Agent Skills |
| `/review` | 选择并运行合适的代码审查代理 |
| `/review-bugbot` | 用 Bugbot 查找可能的缺陷和回归 |
| `/review-security` | 做安全审查 |
| `/sdk` | 帮助使用 Cursor SDK 做应用和集成 |
| `/shell` | 把提供的文本作为字面 shell 命令执行 |
| `/split-to-prs` | 把大改动拆成较小的 pull request |
| `/statusline` | 配置 Cursor CLI 状态栏 |
| `/update-cli-config` | 更新 `~/.cursor/cli-config.json` |
| `/update-cursor-settings` | 查找并更新 Cursor 或 VS Code 设置 |

文档写明：可在聊天中用 `/` 选择；当请求明显匹配时，Agent 也可能自动使用其中一些技能。本批没有在产品里逐个点开验证行为。

## 自定义技能放在哪里、格式是什么

文档给出的自动加载位置：

| 位置 | 范围 |
| --- | --- |
| `.agents/skills/` | 项目级 |
| `.cursor/skills/` | 项目级 |
| `~/.agents/skills/` | 本机用户级 |
| `~/.cursor/skills/` | 本机用户级 |

文档还写明，为兼容性也会加载 Claude 与 Codex 目录：`.claude/skills/`、`.codex/skills/`，以及对应的用户级目录。关于云端 Agent：未同步的 `~/.agents/skills/` 或未同步的本机技能，不会被复制到 Cloud Agents 或远程 SSH 会话；`~/.cursor/skills/` 在同步或发布给团队后才会到达这些环境。细节以文档当前说明为准。

`SKILL.md` 的必填字段（Cursor 文档表格）：`name`（须与父目录名一致，仅小写字母、数字和连字符）、`description`。可选字段包括：`paths`（按 glob 限制仅在匹配文件时出现）、`disable-model-invocation`（为 true 时只有显式 `/skill-name` 才会纳入）、`icon`、`color`、`metadata`。旧字段 `globs` 仍被接受，但新技能应写 `paths`。这些可选字段是 Cursor 文档中的产品字段；其中 `paths`、`disable-model-invocation` 等不属于开放规范的必填部分。

文档给出的最小结构示例：

```markdown
---
name: my-skill
description: Short description of what this skill does and when to use it.
---

# My Skill

Detailed instructions for the agent.
```

从 GitHub 仓库安装技能：文档写明技能不会单独被「导入」，需要打成 plugin，并通过 marketplace 发布或用 Customize 里的 From GitHub Repository 导入（仓库需有 `.cursor-plugin/marketplace.json`）。本批未实测该流程。

`/migrate-to-skills`（文档写明在 2.4 提供）可把「Apply Intelligently」且没有 `globs` 的动态规则，以及斜杠命令，改写成技能；`alwaysApply: true` 或带特定 `globs` 的规则、以及用户规则，不会被迁移。

## 安装、费用、Windows、门槛

- **有没有桌面或网页版**：Cursor 是桌面编辑器，并有云端 Agent。技能文档覆盖编辑器与 CLI。
- **是否需要编程**：使用内置 `/create-skill`、`/review` 等，按文档用 `/` 即可，不必须先写代码。自己写技能需要会编辑 Markdown。
- **是否需要自建服务器**：不需要为内置技能另搭服务器。
- **是否需要 API Key**：使用 Cursor 产品本身需要 Cursor 账号和其订阅方案。本批未核对本页以外的价格。
- **Windows**：文档明确写了 Alt+Enter 作为 Custom Mode 快捷键，说明产品考虑了 Windows。本批未做额外兼容性测试。
- **技能门槛**：会使用 Cursor Agent 聊天和 `/` 菜单即可试用内置技能；编写自定义技能还需会在项目里创建文件夹和 Markdown。

## 优点和局限

优点：若你已经在用 Cursor，内置技能无需另行寻找安装源；文档对目录、frontmatter 和与规则/命令的迁移说得比较具体；同时兼容若干 Claude / Codex 技能路径，有利于同一份 `SKILL.md` 被多个工具发现。

局限：没有找到内置技能的公开 `SKILL.md`，无法按源码评测指令质量；从 GitHub 安装需要走 plugin/marketplace，而不是只复制一个文件夹（与「随手丢一个 SKILL.md 到项目目录」是两条路径）；本批未实测云端同步边界。

## 元数据

- 更新时间：2026-11-25（Asia/Shanghai）
- 来源：
  - [Cursor Docs: Agent Skills](https://cursor.com/docs/skills)
  - [Cursor Changelog 2.4](https://cursor.com/changelog/2-4)（发布标注 2026-01-22）
- 信息可信度：部分核对。文档页已打开；未读到内置技能的 SKILL.md 原文；未实测安装、同步或各内置技能的实际行为。
- 平台：Cursor 编辑器与 CLI（以官方文档为准）。Windows 快捷键已在文档出现。
- 技能门槛：会使用 Cursor Agent 聊天即可试用内置技能；编写自定义技能需会编辑 Markdown 和项目目录。
- 费用：产品订阅价格未知；本页不编造套餐价。内置技能不是一份单独售卖的开源包。
