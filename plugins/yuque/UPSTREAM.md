# 上游同步记录

检查日期：2026-10-09。插件版本：0.2.1。

## 专用技能

- 来源：[yuque/yuque-ecosystem](https://github.com/yuque/yuque-ecosystem/tree/2959228ad3e8acf7503a56ace8e33a9f54afd0e1/skills)。
- 同步基准提交：`2959228ad3e8acf7503a56ace8e33a9f54afd0e1`。
- 范围：`daily-capture`、`knowledge-connect`、`note-refine`、`reading-digest`、`smart-search`、`smart-summary`、`stale-detector`、`style-extract` 的完整 `SKILL.md`。
- 上游本次差异：每个技能补充 `compatibility` 声明，要求连接语雀 MCP 并配置个人 Token。
- `daily-capture`、`note-refine`、`reading-digest`、`smart-search`、`smart-summary` 与基准提交逐字节一致。
- 本地兼容调整：`stale-detector` 上游示例向 `yuque_list_books` 传入 `user_id`，`knowledge-connect` 和 `style-extract` 的示例省略参数。npm 正式版 `1.0.0` 要求 `login`，因此这三个技能补充 `yuque_get_user` 获取登录名的步骤，并修正列表调用参数；其他内容沿用上游。
- `skills/yuque/` 是本插件维护的统一入口，不属于上游技能副本；入口也说明了正式版的 `login` 参数要求。

## MCP 正式版

- 来源：[yuque/yuque-mcp-server](https://github.com/yuque/yuque-mcp-server)。
- npm 包：[yuque-mcp](https://www.npmjs.com/package/yuque-mcp)，最新正式版仍为 `1.0.0`，发布于 2026-05-27。
- npm 包的 `gitHead`：[a8420a9dc86c970dfaeb0096e351b537d11fbb8c](https://github.com/yuque/yuque-mcp-server/commit/a8420a9dc86c970dfaeb0096e351b537d11fbb8c)。
- 插件固定使用 `npx -y yuque-mcp@1.0.0`，运行要求为 Node.js 18 或以上版本。
- 正式版 CLI 支持 `YUQUE_PERSONAL_TOKEN` 和可选的 `YUQUE_BASE_URL`。0.2.1 的 Codex 兼容配置转发这两个变量；API 地址必须完整包含 `/api/v2`。

## 已检查但尚未发布的 MCP 源码

检查时 MCP 主分支提交为 [757a408c29cb21ba493a22de2ac99126d2460f75](https://github.com/yuque/yuque-mcp-server/commit/757a408c29cb21ba493a22de2ac99126d2460f75)。相较 npm 正式版，其源码新增或调整了配置、分页、搜索返回结构和文档读写行为，包括 `YUQUE_TOKEN`、`YUQUE_HOST`、搜索分页及 `{ total, items }` 返回结构。

这些变更尚未进入 npm 正式版。本插件继续跟随官方发布版，不将主分支源码或新环境变量当作 `1.0.0` 的功能。后续 npm 发布新版本时，应重新检查工具参数、搜索结果结构和读写行为，再升级固定版本并验证技能兼容性。
