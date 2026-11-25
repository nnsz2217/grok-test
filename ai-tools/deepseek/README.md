# DeepSeek 高级技巧

本目录整理 DeepSeek 网页/App 和官方 API 里更细、更可操作的用法，作为 [产品总览](../DeepSeek.md) 的补充，不替换总览里的入口说明、限制和「本轮访问情况（2026-11-25，Asia/Shanghai）」。

本批对照官方 API 文档、用户协议、官网和下载页整理，查询日期为 2026-11-25（Asia/Shanghai）。没有登录产品，也没有实际发出 API 请求，所以功能状态只用 Officially Documented、Community Reported 或 Unverified，不标 Verified，也不声称已经实测成功。

读者若主要在网页或官方 App 里学习，先看功能和模型选择两篇；只有需要按量调用或把模型接到自己的程序时，再看 API 用法和价格。API 工作流的自动化方案不在本目录范围。DeepSeek Harness 的上手实测不在本批展开。

## 当前内容

- [网页与 App 的对话功能](./chat-features.md)：思考模式、网页搜索、深度思考搜索、上传文件提问，以及这些能力和 API 的对应关系。
- [模型与思考强度怎么选](./model-selection.md)：什么时候用网页/App，什么时候用 API；`deepseek-flash` 与 `deepseek-v4-pro` 的差别；何时开关思考模式。
- [API 用法](./api-usage.md)：申请密钥、官方地址、在 Windows 上保存密钥、第一次调用的官方示例，以及常见错误码。本轮未实际发请求。
- [API 价格与省钱方法](./api-pricing-and-cost.md)：2026-11-25 官方单价、高峰/空闲时段（北京时间）、缓存命中，以及不要引用过时营销页价格。

## 元数据

- 更新时间：2026-11-25（Asia/Shanghai）
- 来源：本目录当前文件清单；各篇事实来源见文末。产品总览与访问记录见 [../DeepSeek.md](../DeepSeek.md)
- 信息可信度：部分核对。本页作为索引已与当前文件清单对齐。各篇对照官方文档的内容为 Officially Documented；本轮没有登录、没有发送 API 请求，不能当作上手验证
- 平台：以各篇已核对的官方说明为准，主要包括网页 chat.deepseek.com、官方 iOS / Android 客户端，以及 `https://api.deepseek.com`。未实测具体机型
- 技能门槛：使用网页/App 时，会注册或登录并说明任务即可。阅读 API 两篇需要会在 Windows 上设置环境变量，并理解“按 token 付费”
- 费用：网页/App 官方表述为「免费体验」（是否另有未公布限额：未知）。API 为 API 计费，具体单价见价格笔记，并带来源和查询日期
