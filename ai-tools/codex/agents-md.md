# 用 AGENTS.md 写可复用约定

适用产品：OpenAI Codex。把“这个作业怎么运行、测试、哪些文件不要动”写成文件，让以后的每次任务自动带上，而不必把同一段话贴进每一次提示。以下为官方说明，状态为 Officially Documented。本轮没有运行 Codex，不能当作已经实测成功。

## 1. 用短而具体的 AGENTS.md，并按目录分层

**用途：** 减少重复说明，也减少它用错测试命令或改到不该改的文件。

**操作方法：**

1. 在 CLI 里，可先运行 `/init` 生成一份起始 `AGENTS.md`，然后改成符合这个项目的真实命令和约定。官方提醒：自动生成只是起点，应改成你们实际使用的构建、测试和提交方式。
2. Codex 在每次运行开始时（TUI 里通常是每个会话开始时）按下面的顺序收集说明：
   1. 全局：默认读取 `~/.codex/AGENTS.override.md`（若存在），否则读取 `~/.codex/AGENTS.md`。这一层只用第一份非空文件。
   2. 项目：从项目根目录（通常是 Git 根目录）走到当前工作目录。每一层先看 `AGENTS.override.md`，再看 `AGENTS.md`，再看你在配置里列出的备用文件名。每一层最多纳入一份。
   3. 合并时从根到当前目录拼接，靠后的文件覆盖前面的说明。
3. 空文件会被跳过。全部说明合计达到 `project_doc_max_bytes`（默认 32 KiB）后不再追加。需要时可提高该上限，或把说明拆到更靠近工作目录的文件中。
4. 官方建议一份好的 `AGENTS.md` 写清：仓库结构、如何运行、构建 / 测试 / 检查命令、约定和 PR 期望、不要做的事、以及怎样算完成。先写短而准确的内容，发现它重复犯同一类错误时再追加，不要一上来写很长的空泛规则。
5. 可用 `~/.codex/AGENTS.override.md` 做临时全局覆盖，而不删除原来的全局文件。
6. 若仓库已经使用别的文件名（例如 `TEAM_GUIDE.md`），可在 `~/.codex/config.toml` 里设置 `project_doc_fallback_filenames`。官方示例还把 `project_doc_max_bytes` 提高到 65536。

**可复制的全局约定示例（官方示例的中文改写，需按你的项目修改命令）：**

```markdown
# ~/.codex/AGENTS.md

## 工作约定

- 修改 JavaScript 文件后，要运行项目里已有的测试命令。
- 安装依赖时，优先使用项目已经在用的包管理器，不要擅自更换。
- 新增生产环境依赖前先征求确认。
```

**可复制的课程项目示例：**

```markdown
# AGENTS.md

## 这个作业项目怎么运行

- 用 `npm test` 运行测试，不要发明其他测试命令。
- 只修改 `src/` 和 `src/` 下已有测试文件。不要改老师提供的 `fixtures/`。
- 提交前不要重写无关文件的格式。
- 完成标准：相关测试通过，并且 README 里的示例命令仍能运行。
- 不要在回复或代码里写入密钥、密码或个人帐户信息。
```

官方还给出在子目录使用 `AGENTS.override.md` 以覆盖通用测试命令的例子，例如某个子项目应运行 `make test-payments` 而不是 `npm test`。

**适用场景：** 课程项目有固定的启动和测试方式；你希望它默认用简体中文解释、并且先给出计划再改文件。

**限制：**

- 说明看起来过期时，在目标目录重新启动 Codex。它会在每次运行（以及每个 TUI 会话开始时）重建说明链，没有需要手动清理的缓存。
- 官方核对方法包括：`codex --ask-for-approval never "Summarize the current instructions."` 以及带 `--cd` 查看子目录加载了哪些文件。这些命令会改变审批行为（`never` 表示不再询问），只应在你理解含义的可信目录中用于检查说明，不要当成日常默认。
- 若设置了 `CODEX_HOME`，它会读取另一个主目录。Windows 与 WSL 的主目录可能不是同一处，见 Windows 笔记。
- 本轮未生成或加载 AGENTS.md，属 Unverified。

**来源与可信度：** Officially Documented。[Custom instructions with AGENTS.md](https://learn.chatgpt.com/docs/agent-configuration/agents-md)、[Best practices](https://learn.chatgpt.com/guides/best-practices)、[Codex CLI](https://learn.chatgpt.com/docs/codex/cli)。查询日期 2026-11-25。

## 元数据

- 更新时间：2026-11-25（Asia/Shanghai）
- 来源：上文各官方学习文档链接
- 信息可信度：部分核对。发现顺序、覆盖规则、建议写入的内容和 `/init` 为 Officially Documented。本轮未运行 `/init` 或核对命令，属 Unverified。未核对手表价
- 平台：CLI、IDE 和桌面应用共用说明发现机制。Windows 上注意 `~/.codex` 与 `%USERPROFILE%\.codex` 是否为同一位置。未实测
- 技能门槛：会在项目根目录新建或编辑一个 Markdown 文件。使用全局文件需要知道用户主目录。不需要先会写程序，但要能写清真实的测试命令
- 费用：不适用（这是本地说明文件）。运行 Codex 本身仍按你的方案或 API 计费，未核对手表价
