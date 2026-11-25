# AI Skill Engineering / Agent 工具开发简报

检索截止 2026-11-25（Asia/Shanghai）。过去半年里，社区已经不太纠结 Skills 和 MCP 谁更优，而是把 Skill 当成可定义、可分发、可训练、可验收的软件产物。下面 5 项按规范、方法论、训练、安装工具、工程教程排列；星标都在 2026-11-25（Asia/Shanghai）用 GitHub API 复核过。本轮 Reddit 无法打开，所以没有引用 upvote。窗口内也几乎没有新的高分 HN 帖，年初那几篇高赞讨论只作背景。

## 1. [Agent Skills 开放规范](https://github.com/agentskills/agentskills)

- 仓库：[github.com/agentskills/agentskills](https://github.com/agentskills/agentskills)，规范文档：[agentskills.io/specification](https://agentskills.io/specification)
- 热度：27,609 stars，2,075 forks；最近一次推送是 2026-11-05 03:47（Asia/Shanghai）
- 架构：技能就是一个至少含 `SKILL.md` 的目录。必填只有 `name` 和 `description`。路由不是单独的路由器，而是 **progressive disclosure（渐进披露）**：启动时只把各技能的 name + description 放进上下文（大约 100 tokens），匹配后再加载正文，脚本和参考资料执行时再读。技能选择由模型根据 description 判断。

这是目前大多数技能仓库和教程的共同底座。

## 2. [obra/superpowers](https://github.com/obra/superpowers)

- 仓库：[github.com/obra/superpowers](https://github.com/obra/superpowers)
- 热度：325,919 stars，28,920 forks；最近一次推送是 2026-11-25 07:59（Asia/Shanghai）。这是本次星标最高的相关仓库。
- 架构：每个能力仍是标准技能目录。引导技能 `using-superpowers` 要求在任何回复或行动前先检查并调用相关技能，过程类技能优先于实现类，用户指令优先于技能。`writing-skills` 把写技能本身做成 TDD：先拿无技能基线，再写 `SKILL.md`，再验收智能体是否遵从。没有独立路由器。

它把规范里的“description 触发 + 渐进加载”落实成可安装的强制工作流。

## 3. [Microsoft SkillOpt](https://github.com/microsoft/SkillOpt)

- 仓库：[github.com/microsoft/SkillOpt](https://github.com/microsoft/SkillOpt)；论文：[arXiv:2605.23904](https://arxiv.org/abs/2605.23904)；[MSR 博文](https://www.microsoft.com/en-us/research/blog/skillopt-agent-skills-as-trainable-parameters/)（2026-06-30）
- 热度：19,209 stars，1,835 forks；论文 v2 修订于 2026-05-25，仓库在检索当日仍有更新
- 架构：把技能文档当成可训练参数。目标模型权重冻结，优化器根据执行轨迹对技能做有预算的增删改，只有在验证集上严格提升才接受，最终导出可部署的 `best_skill.md`。推理期不再调用优化器，工具调用仍由原智能体的工具 / MCP / CLI 完成。SkillOpt 优化的是“怎么把已有工具用对”的程序文本。

这是最直接对应「AI Skill Engineering」的一项：写技能从一次性提示词，变成带验证门的训练过程。文中的基准提升数字来自项目 README / 博文，本文没有复现实验。

## 4. [vercel-labs/skills](https://github.com/vercel-labs/skills)

- 仓库：[github.com/vercel-labs/skills](https://github.com/vercel-labs/skills)；目录站点：[skills.sh](https://skills.sh)
- 热度：40,790 stars，3,606 forks；v1.9.0 发布于 2026-11-16
- 架构：不发明新格式，而是给符合规范的 `SKILL.md` 做包管理：从 GitHub 安装、更新、删除，并用 `skills-lock.json` 按内容哈希和 commit SHA 锁定。CLI 本身不做推理期路由，装好后仍由各智能体按 name/description 渐进加载。

它补齐的是技能如何分发和锁定，而不是又做一个技能合集。

## 5. [How we ship Google Agent Skills like products](https://cloud.google.com/blog/topics/developers-practitioners/behind-the-scenes-two-months-later-how-we-ship-google-agent-skills-like-products)

- 文章：Google Cloud Blog，Remigiusz Samborski，2026-10-28
- 配套仓库：[github.com/google/skills](https://github.com/google/skills)，24,629 stars，2,049 forks；检索当日仍有推送
- 架构：格式仍是 `SKILL.md`。工程重点在发布门禁：PR 先做结构、lint 和语义化版本检查，再跑评估套件和 AI review，最后由领域专家批准。评估把“技能是否被选中”和“选中后是否遵从指令”分开看。

这是窗口内少有的、日期可核验的官方深度教程，把技能工程落到版本、CI 和评审。

---

如果只想再读两篇对照文章，一篇是 Formal 的 [MCP vs Skills](https://www.formal.ai/blog/mcp-vs-skills/)（2026-11-18 更新）：缺步骤用 skill，缺系统访问用 MCP，多数工作流两者搭配。另一篇是 TuringPost 的 [What Is Skill Engineering for AI Agents?](https://www.turingpost.com/p/from-prompt-engineering-to-skill-engineering)（2026-06-10），直接定义了这个说法。两篇都没有核实到社区点赞数。工具层背景可以看 2026-07-28 的 [MCP Tools 规范](https://modelcontextprotocol.org/specification/2026-07-28/server/tools)：用 JSON Schema 定义工具，经 `tools/list` 发现、`tools/call` 调用。
