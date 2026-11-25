# Windows 上的安装与沙箱

适用产品：OpenAI Codex 在 Windows 上的桌面应用、原生环境与 WSL2。Windows 用户需要先选对“代理在哪里运行”，否则会出现路径很慢、Git 检测不到或配置不共享的问题。以下为官方说明，状态为 Officially Documented。本轮没有在 Windows 上安装或运行，不能当作已经实测成功。

## 1. 先决定用 Windows 原生还是 WSL2，并按该环境放置项目

**用途：** 在 Windows 上稳定运行 Codex，并避开官方已经写明的常见坑。

**两条官方路径：**

1. **Windows 原生（适合主要在 Windows 文件夹里工作）：**
   - 安装 ChatGPT 桌面应用，在设置中把 agent environment 选为 **Windows native**，集成终端可选 PowerShell。代理在 Windows 沙箱中运行。
   - 官方写明该应用支持工作树、定时任务、Git、内置浏览器、文件预览、插件和技能。
   - 企业或需要命令行安装时，文档给出了 Microsoft Store 的 winget 示例：`winget install --id 9PLM9XGG6VKS -s msstore`。是否适用于你的帐户，以官方桌面应用说明和你的方案为准。
2. **WSL2（适合项目已经在 Linux 环境里、或需要 Linux 原生工具）：**
   - 需要 Windows 上已安装 WSL2。在提升权限的 PowerShell 或 Windows Terminal 中可用 `wsl --install`，再进入 WSL 后运行 `curl -fsSL https://chatgpt.com/codex/install.sh | sh` 和 `codex`。
   - 在 WSL 里开发时，官方建议把仓库放在 Linux 主目录（例如 `~/code/my-app`），不要放在 `/mnt/c/...`，否则可能更慢，并更容易遇到符号链接和权限问题。
   - 若使用 VS Code，应在 WSL 终端中进入项目后运行 `code .`，确认状态栏显示 `WSL: ...`，集成终端路径应为 `/home/...`。
   - **WSL1 已不受支持。** 官方写明 WSL1 支持到 Codex `0.114`；从 `0.115` 起 Linux 沙箱改为 `bubblewrap`，不再支持 WSL1。

**两处官方建议看起来相反，需要按场景理解：**

- [WSL](https://learn.chatgpt.com/docs/windows/wsl) 建议：在 WSL2 里工作时，仓库放在 Linux 主目录，避免 `/mnt/c`。
- [ChatGPT desktop app for Windows](https://learn.chatgpt.com/docs/windows/windows-app) 建议：若要用 **Windows 原生代理** 处理同时也可从 WSL 访问的项目，目前较稳妥的做法是把项目放在 Windows 磁盘，再从 WSL 通过 `/mnt/...` 访问；从 `\\wsl$` 打开的项目可能检测不到 Git。若希望代理本身在 WSL2 中运行，把设置里的 agent 改成 WSL 并重启应用。

也就是说：代理在 WSL 里时，代码放 Linux 主目录；代理在 Windows 原生时，代码放 Windows 磁盘。不要混用后再认为官方“自相矛盾”。

**其他官方已经写明的 Windows 注意事项：**

- 桌面应用与 Windows 原生 Codex 共用 `%USERPROFILE%\.codex`。在 WSL 里跑 CLI 时，默认用的是 Linux 主目录下的 `~/.codex`，**不会自动**与 Windows 应用共享配置、登录状态和会话。若要共享，需自行同步这两个目录，或在 WSL 中设置 `export CODEX_HOME=/mnt/c/Users/<windows-user>/.codex`。
- 若 PowerShell 提示无法运行脚本（例如 `npm.ps1 cannot be loaded because running scripts is disabled`），官方提到一种常见处理是把执行策略设为 `RemoteSigned`，并建议先阅读微软的执行策略说明再改。
- 若需要代理运行需要管理员权限的命令，应把 ChatGPT 桌面应用本身以管理员身份启动，代理会继承该权限。请只在确实需要时使用。
- 官方列出 Git、Node.js、Python、.NET SDK、GitHub CLI 等常用工具，并给出 winget 安装示例。不是每项都必须先装齐；没有 Git 时，应用的部分审查功能不可用。GitHub CLI 在 `gh auth login` 之后才能使用相关功能。

**适用场景：** 在 Windows 10/11 上写课程编程作业；已经安装了 WSL 或只想用桌面应用。

**限制：** 本轮未在 Windows 上安装，安装是否成功、沙箱具体提示以及执行策略修改的效果均为 Unverified。不要在不理解后果时更改系统执行策略或长期以管理员身份运行。桌面应用对方案的要求以 ChatGPT Windows 帮助页为准，两处官方说明曾有过不一致，见 [ChatGPT.md](../ChatGPT.md)。

**来源与可信度：** Officially Documented。[ChatGPT desktop app for Windows](https://learn.chatgpt.com/docs/windows/windows-app)、[WSL](https://learn.chatgpt.com/docs/windows/wsl)、[Codex CLI](https://learn.chatgpt.com/docs/codex/cli)。查询日期 2026-11-25。

## 元数据

- 更新时间：2026-11-25（Asia/Shanghai）
- 来源：上文各官方学习文档链接，以及 [../ChatGPT.md](../ChatGPT.md) 中关于 Windows 桌面应用适用方案的说明
- 信息可信度：部分核对。安装路径、WSL1 不再支持、配置目录不自动共享等为 Officially Documented。本轮未在 Windows 上安装或运行，属 Unverified。未核对手表价
- 平台：已核对官方文档中的 Windows 原生桌面应用、PowerShell 与 WSL2。未测 WSL1（官方已写明不再支持）。未实测具体 Windows 版本
- 技能门槛：会安装桌面应用或在终端粘贴一条官方安装命令，并分清 Windows 路径和 WSL 路径。修改执行策略前需要阅读微软说明。不是必须先精通 Linux
- 费用：免费 / 付费。能否安装桌面应用可能与 ChatGPT 方案有关；未核对手表价，故不写入金额
