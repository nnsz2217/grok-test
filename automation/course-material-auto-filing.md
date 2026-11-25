# 用 Power Automate 桌面版自动归档课程资料

当 PDF、PowerPoint 或 Word 文件出现在「下载」文件夹（或你指定的投放文件夹）里时，按文件名中的课程关键词，把它们移到对应的课程文件夹。本篇面向在 Windows 上、不想写代码的大学生，用官方已文档化的操作搭一条可反复运行的流程。

## 正文

### 能解决什么问题

下载课件、论文或作业附件后，文件常堆在「下载」里，要靠手工改名、拖拽归类。本流程把「按扩展名找出课程相关文件 → 按文件名里的课程关键词判断去向 → 移动到事先建好的课程文件夹」做成一条桌面流。官方入门文档也把「组织或备份文件和文件夹」列为可用 Microsoft 帐户完成的典型桌面自动化场景。

它能做的是：按你事先约定的文件名规则归类。它不能做的是：读懂课件内容后再决定属于哪门课，也不会在文件刚落入文件夹的同一秒自动启动（原因见「触发条件」）。

### 需要哪些工具

- 一台符合官方系统要求的 Windows 10 或 Windows 11 电脑（家庭版、专业版或企业版均可创建并在本地有人参与运行桌面流）。不支持 ARM 处理器设备。
- Power Automate 桌面版（Power Automate for desktop）。Windows 11 可能已预装该应用；若没有，可从 Microsoft Store 安装（无需管理员权限），或使用 MSI 安装程序（需要管理员权限）。不要同时安装 Store 版和 MSI 版。
- 一个用于登录的 Microsoft 帐户（个人帐户即可）。使用 Microsoft 帐户创建的桌面流会自动保存在你的 OneDrive。工作或学校帐户另需默认环境中的 Dataverse 数据库，本篇以个人 Microsoft 帐户为主。
- 不需要 API Key。官方安装与创建桌面流步骤均未要求申请开发者密钥。

### 触发条件

请把触发理解成「什么时候开始跑这一次归档」，而不是「文件一出现就立刻有人值守地接管」。

官方帐户功能对照写明：个人 Microsoft 帐户和工作/学校帐户都**没有**「与云端流（触发/计划流）的连接性」；要从云端触发或用云端计划来启动桌面流，需要组织高级帐户。Windows 10/11 家庭版可以创建桌面流并在本地有人参与运行，但不能从云端触发桌面流。

因此，本流程采用下面两种官方已记载、且个人帐户能用的启动方式（任选，可同时保留）：

1. **手动运行（建议先用这个完成验证）**：在 Power Automate 控制台中运行该流；或在控制台中右键单击流名称，选择「创建桌面快捷方式」，之后用快捷方式启动。
2. **按时间间隔自动运行**：用 Windows 任务计划程序，通过官方记载的运行 URL 定期启动同一条流。这是「到点检查一次文件夹」，不是「监视到新文件立即触发」。

不要把「等待文件」当作本流程的主触发：该操作需要填写**某一个文件的完整路径**，并等到该文件被创建或删除；它不能按官方参数写成「下载文件夹里出现任意新课件就继续」。另外，通过 URL 或快捷方式启动时，默认会弹出确认对话框；一次只能有一个流以本地有人参与模式运行；若该流已在运行，再次调用运行 URL 不会让它再跑一遍。

### 安装和配置

1. 确认系统。打开 Windows 设置查看版本是否为 Windows 10 或 Windows 11（家庭版、专业版或企业版）。若是 ARM 设备，官方写明不支持，不要继续按本篇安装。电脑需要有效的 Internet 连接，并安装受支持的浏览器（Microsoft Edge 80 或更高版本、Google Chrome 或 Mozilla Firefox）。
2. 确认或安装 Power Automate 桌面版。
   - 在 Windows 11 上，可先在「开始」菜单搜索 Power Automate，看是否已经预装。
   - 若未安装且没有管理员权限：按官方安装文档，打开 Microsoft Store 中的 Power Automate 桌面版页面，选择 Download（或「查看 Store」后在 Store 应用里安装）。Store 安装不需要管理员权限，并会自动更新。本次检索打开的 Store 列表页为：[Power Automate（Microsoft Store）](https://apps.microsoft.com/detail/9NFTCH6J7FHV)；若页面与文档不一致，以 [安装文档](https://learn.microsoft.com/zh-cn/power-automate/desktop-flows/install) 中的 Store 入口为准。
   - 若由学校或管理员用 MSI 安装：需要本机管理员权限，安装包文件名为 `Setup.Microsoft.PowerAutomate.exe`。同一台电脑不要同时保留 MSI 版和 Store 版。
3. 启动应用并用**个人 Microsoft 帐户**登录。官方写明：利用 Microsoft 帐户使用 Power Automate 无需额外费用。
4. 建议先在设置中确认已安装的是哪一种：开始菜单 > 设置 > 应用，搜索 Power Automate。若列表中是「Power Automate for desktop」（或「Power Automate 桌面版」），为 MSI 版；若是不带 “for desktop” 的「Power Automate」，为 Microsoft Store 版。后面配置任务计划程序时要用对应路径。

### 完整工作流程

先约定规则，再搭流。规则不清楚，自动化只能把文件挪错地方。

**约定（动手前先做完）**

- **投放文件夹**：可以是「下载」，也可以是你单独建的投放文件夹。在文件资源管理器中点开地址栏，复制完整路径，后面要原样填进流里。不要假设所有电脑都是同一个路径。
- **课程资料根目录**：例如在「文档」下建立 `课程资料`，其下再为每门课建一个文件夹（如 `高等数学`、`大学英语`），另外建一个 `待分类`。官方「获取特殊文件夹」可选「个人」（说明中对应「我的文档」一类位置）或「桌面」，但**官方特殊文件夹列表里没有「下载」**，所以投放文件夹必须手填完整路径。
- **文件名规则**：文件名里要能看出课程，例如 `高数-第3讲.pdf`、`英语-essay.docx`。本流用「如果」操作的 Contains（包含）运算符，检查 `%当前文件.Name%`（文件名，含扩展名）里是否出现你指定的关键词。Contains 是否区分大小写，官方条件文档未写明，**待核实**；关键词请按你实际保存文件时常用的写法填写。
- **只处理这些扩展名**：`.pdf`、`.pptx`、`.ppt`、`.docx`、`.doc`。用官方「获取文件夹中的文件」的文件筛选器，每次按一种通配符筛选（官方单类示例为 `*.txt`）。不要把下载文件夹里的安装包、图片一并搬走。

**在设计器里搭流（全部使用预生成操作，不用写代码）**

官方创建流的入口是：启动 Power Automate，在控制台选择「新建流」，输入名称（例如「课程资料归档」），选择「创建」，进入流设计器，从操作窗格拖入操作。

建议按下面顺序添加。界面显示语言跟随 Windows 显示语言；下文同时给出官方中文文档中的操作名。

1. （可选）添加「获取特殊文件夹」，将特殊文件夹名称设为「个人」，保存后得到 `%SpecialFolderPath%`。若课程资料根目录就建在「文档」下，后续路径可写成 `%SpecialFolderPath%\课程资料`。若你更想完全手填根目录，可跳过本步。
2. 用「如果文件夹存在」检查根目录、各课程文件夹和 `待分类` 是否存在；在「不存在」分支里用「创建文件夹」建出缺失的文件夹。移动文件前目标文件夹必须存在，否则「移动文件」会报「目标文件夹不存在」。
3. 添加「获取文件夹中的文件」：
   - Folder（文件夹）：投放文件夹的完整路径；
   - 文件筛选器：`*.pdf`；
   - Include subfolders（包含子文件夹）：保持默认的关闭（False），避免把子文件夹里的文件一并取出。
   - 该操作会产出文件列表变量，默认名通常为 `%Files%`。
4. 添加「对于每个」（For each），要迭代的值设为 `%Files%`。把循环里表示当前项的变量命名为 `当前文件`（或你能看懂的名字）。之后用官方文件属性写法访问：
   - `%当前文件.Name%`：含扩展名的文件名，用来匹配课程关键词；
   - `%当前文件.FullName%`：完整路径，可作为「移动文件」的来源。
5. 在循环内添加「如果」：
   - 第一个操作数：`%当前文件.Name%`
   - 运算符：Contains
   - 第二个操作数：你的课程关键词，例如 `高数`
   - 在此分支中添加「移动文件」：要移动的文件填 `%当前文件%`（或 `%当前文件.FullName%`），目标文件夹填该课程文件夹路径。「If file exists」（如果文件存在）官方可选「不执行任何操作」或「覆盖」，默认是「不执行任何操作」。建议先保持默认，避免覆盖已归档的同名课件。
6. 在同一个「如果」块中，用「否则如果」为其他课程重复「包含关键词 → 移动到对应文件夹」。最后用「否则」把未匹配到任何关键词的 PDF 移到 `待分类`。
7. 再添加四组同样结构的「获取文件夹中的文件」+「对于每个」+「如果 / 否则如果 / 否则」，文件筛选器分别设为 `*.pptx`、`*.ppt`、`*.docx`、`*.doc`。这样不必依赖「多个筛选器用分号连接」的写法——官方多筛选器示例写成了 `.txt;.exe`（没有星号），与单类示例 `*.txt` 不完全一致，**本篇不采用该写法，以免把未核清的筛选语法写进可运行步骤**。
8. 选择「运行」做第一次测试（见「怎样算做完」）。确认无误后，关闭设计器并保存。之后可从控制台再次运行，或右键流名称选择「创建桌面快捷方式」。

**第一次建议用「复制文件」试跑**：该操作的参数与「移动文件」类似，但不会把原件从投放文件夹拿走。试跑成功后再把相应步骤改回「移动文件」。

**可选：用任务计划程序定期运行**

仅在手动运行已经达到「怎样算做完」之后再配置。官方步骤是：

1. 打开 Windows 的任务计划程序，创建新任务，在「创建任务」对话框的「操作」选项卡中添加新操作。
2. 「Program/script」（程序或脚本）填写：
   - MSI 安装：`C:\Program Files (x86)\Power Automate Desktop\dotnet\PAD.Console.Host.exe`
   - Microsoft Store 安装：`C:\WINDOWS\system32\WindowsPowerShell\v1.0\powershell.exe`
3. 「添加参数」填写（把 `课程资料归档` 换成你的实际流名称）：
   - MSI 安装：`ms-powerautomate:/console/flow/run?workflowName=课程资料归档`
   - Microsoft Store 安装：`-Command "Start-Process \"ms-powerautomate:/console/flow/run?workflowName=课程资料归档\""`
4. 在触发器里设定你能接受的间隔（例如每天放学后一次）。具体间隔选项以任务计划程序本机界面为准；官方文档记载了如何添加启动动作，但没有为「课程归档」规定必须用哪一个时间表。
5. 保持默认的外部调用确认对话框，除非你已经理解官方警告：禁用「在外部调用流时显示确认对话框」可能在不知情时运行他人共享的可疑流。个人 Microsoft 帐户本身也不能与他人共享桌面流，但仍不要关闭该确认，除非你明确接受风险。

运行任务计划程序中的任务时，本机需要已安装 Power Automate 桌面版，并且你已登录。

### 是否需要 API Key

不需要。安装、登录、添加文件/文件夹操作、从控制台或运行 URL 启动，官方步骤都不要求 API Key。

### 使用成本

- 官方入门文档写明：「利用 Microsoft 帐户使用 Power Automate 无需额外费用。」核对日期：2026-11-25（Asia/Shanghai）。
- 个人 Microsoft 帐户可用拖放设计器、预生成操作，并在本地有人参与运行；桌面流存储在 OneDrive 个人帐户。不能把桌面流接到云端流上做触发或计划，不能共享协作，也不能使用官方对照表中仅向组织高级帐户开放的无人参与 RPA、高级连接器等能力。
- 本篇不列出具体价格或套餐金额：官方许可文档中的付费计划会变化，本次不为高级许可填写数字。
- Microsoft Store 列表页标题含 “Free download and install”，指的是应用可免费下载安装；不要把它理解成对所有 Power Automate 云端或高级功能的报价。

### 技术门槛

不需要编程。需要会：在文件资源管理器中复制文件夹完整路径、按名称保存课件、在设计器里拖入操作并填写路径和关键词、从控制台运行一次做测试。任务计划程序是可选的进阶配置，官方有逐步说明，但字段比「新建流」略多。

### 适用场景

- 经常从课程平台、邮箱或浏览器下载 PDF / PPT / Word，希望定期把它们归进各课程文件夹。
- 可以做到「保存时文件名带课程关键词」，或愿意为将要归档的文件补上关键词。
- 使用个人 Windows 电脑和个人 Microsoft 帐户，只在本机运行。

不适用：需要文件一保存就立刻自动处理且电脑不必登录、不能接受确认对话框；需要按文件内容（而不是文件名）分类；需要从云端或他人电脑远程启动这条桌面流。

### 潜在限制和安全风险

- **不是实时监视**。个人帐户不能用云端「当文件创建时」去启动桌面流；定时运行只按你设定的间隔检查。
- **只认文件名里的关键词和指定扩展名**。关键词写错、文件名毫无课程信息、或扩展名不在筛选列表里，文件就不会进对的课程文件夹。匹配失败的指定扩展名文件应进入 `待分类`，便于你补救。
- **「移动文件」会把文件从投放文件夹拿走**。目标已有同名文件时，默认「不执行任何操作」意味着源文件可能还留在投放文件夹；若改成「覆盖」，目标里的旧文件会被替换。这两种结果都可能造成资料看似「丢了」，测试阶段请先用「复制文件」，并先用副本而不是唯一原件。
- **权限**：访问受保护的文件或文件夹需要以管理员权限运行 Power Automate。本流应只指向你自己的「下载」和「文档」之类用户文件夹，不要对系统目录操作，也不必为普通课程资料提升权限。
- **运行环境**：需要已登录、本机有人参与；需要 Internet 连接。本地有人参与模式一次只能跑一条流。
- **存储与隐私**：个人帐户下的桌面流会存到 OneDrive。不要在流里硬编码他人文件路径，也不要自动化移动你尚未确认来源的附件（下载文件夹里可能有安装程序或不该归档的个人文件）。
- **外部启动确认**：不要为了省一步点击而关闭官方默认的确认对话框，除非你理解其中的安全警告。
- 本篇步骤已对照官方文档，但**没有在 Windows 上实际执行过这条流**。菜单用词若与本机略有出入，以本机界面和所引文档为准。

### 怎样算做完

以下每一项都要做到，才算这条工作流可用，而不是只安装了软件：

1. Power Automate 桌面版已安装（或 Windows 11 上已能打开预装应用），你已用个人 Microsoft 帐户登录。
2. 投放文件夹路径已从资源管理器复制并写进流里；`课程资料` 根目录、至少两个课程文件夹，以及 `待分类` 文件夹已经存在（由你事先建好，或由流里的「创建文件夹」建好）。
3. 控制台里能看到已保存的桌面流（例如「课程资料归档」），其中包含：按 `*.pdf` / `*.pptx` / `*.ppt` / `*.docx` / `*.doc` 分别获取文件、「对于每个」循环、按文件名 Contains 判断课程、以及「移动文件」（或测试阶段的「复制文件」）。
4. **用副本做通测**：把三个测试文件放进投放文件夹，例如 `高数-测试.pdf`、`英语-测试.docx`，以及一个不含任何课程关键词的 `未命名测试.pptx`。从控制台运行该流。运行结束后，前两个文件出现在对应课程文件夹中，第三个出现在 `待分类`；投放文件夹中这三份测试文件在使用「移动文件」时应已离开（若使用「复制文件」试跑，则源文件仍在，目标中有副本）。目标文件夹事先若已有同名文件且选项为「不执行任何操作」，则不应误报为成功。
5. 你能不打开设计器、从控制台或桌面快捷方式再成功运行一次。若启用了任务计划程序，还需要：按官方程序路径与运行 URL 配好任务，到点（或手动运行该任务）后流会启动；若未关闭确认对话框，应能看到确认提示。未配置定时任务时，第 4、5 步已构成「可反复使用」的完成标准。

## 元数据

- 更新时间：2026-11-25（Asia/Shanghai）
- 来源：
  - [先决条件和限制](https://learn.microsoft.com/zh-cn/power-automate/desktop-flows/requirements)（[英文](https://learn.microsoft.com/en-us/power-automate/desktop-flows/requirements)）
  - [安装 Power Automate](https://learn.microsoft.com/zh-cn/power-automate/desktop-flows/install)（[英文](https://learn.microsoft.com/en-us/power-automate/desktop-flows/install)）
  - [开始在 Windows 11 中使用 Power Automate](https://learn.microsoft.com/zh-cn/power-automate/desktop-flows/getting-started-windows-11)（[英文](https://learn.microsoft.com/en-us/power-automate/desktop-flows/getting-started-windows-11)）
  - [使用 Microsoft 帐户开始](https://learn.microsoft.com/zh-cn/power-automate/desktop-flows/getting-started-msa)（[英文](https://learn.microsoft.com/en-us/power-automate/desktop-flows/getting-started-msa)）
  - [文件夹操作引用](https://learn.microsoft.com/zh-cn/power-automate/desktop-flows/actions-reference/folder)（[英文](https://learn.microsoft.com/en-us/power-automate/desktop-flows/actions-reference/folder)）
  - [文件操作引用](https://learn.microsoft.com/zh-cn/power-automate/desktop-flows/actions-reference/file)（[英文](https://learn.microsoft.com/en-us/power-automate/desktop-flows/actions-reference/file)）
  - [循环操作引用](https://learn.microsoft.com/zh-cn/power-automate/desktop-flows/actions-reference/loops)（[英文](https://learn.microsoft.com/en-us/power-automate/desktop-flows/actions-reference/loops)）
  - [使用条件](https://learn.microsoft.com/zh-cn/power-automate/desktop-flows/use-conditionals)（[英文](https://learn.microsoft.com/en-us/power-automate/desktop-flows/use-conditionals)）
  - [条件操作引用](https://learn.microsoft.com/en-us/power-automate/desktop-flows/actions-reference/conditionals)（含 If / Else if 的 Contains 运算符）
  - [变量数据类型属性](https://learn.microsoft.com/en-us/power-automate/desktop-flows/datatype-properties)
  - [通过 URL 或桌面快捷方式运行桌面流](https://learn.microsoft.com/zh-cn/power-automate/desktop-flows/run-desktop-flows-url-shortcuts)（[英文](https://learn.microsoft.com/en-us/power-automate/desktop-flows/run-desktop-flows-url-shortcuts)）
  - [Power Automate（Microsoft Store 列表页，本次打开）](https://apps.microsoft.com/detail/9NFTCH6J7FHV)
- 信息可信度：部分核对。已对照上述官方文档核过系统要求、个人 Microsoft 帐户可在本地创建并有人参与运行、无需额外费用、不能用云端流触发或计划、Store/MSI 安装差异、文件与文件夹操作（含获取文件夹中的文件、创建文件夹、移动/复制文件、等待文件的参数限制）、For each / 如果与 Contains、文件属性、快捷方式与任务计划程序启动方式。未在 Windows 上实际安装或运行本流；Contains 是否区分大小写、多扩展名筛选器的准确写法、本机中文按钮与文档用词是否完全一致，均未实机核对。
- 平台：Windows 10 / Windows 11（家庭版、专业版、企业版）上的 Power Automate 桌面版；个人 Microsoft 帐户本地运行。未核对其它操作系统。
- 技能门槛：会在资源管理器中复制文件夹路径，能按官方步骤在设计器里拖入操作并填写路径和关键词；不要求编程。任务计划程序为可选项。
- 费用：免费（个人 Microsoft 帐户本地创建并运行桌面流：官方写明无需额外费用，核对日期 2026-11-25。云端触发、共享、无人参与等不在此列）
