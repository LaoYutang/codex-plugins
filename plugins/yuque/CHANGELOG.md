# 更新记录

## 0.2.1 — 2026-10-09

- 同步官方 `yuque-ecosystem` 的八个专用技能，补全个人 Token 和 MCP 服务的兼容声明。
- 修正 `stale-detector`、`knowledge-connect` 和 `style-extract` 的知识库列表调用示例，先获取用户 `login`，再按 MCP 正式版参数调用。
- 保持 MCP 官方 npm 正式版 `yuque-mcp@1.0.0`，新增该版本已支持的 `YUQUE_BASE_URL` 环境变量转发。
- 补充 Node.js 18+、完整 API 地址配置和正式版环境变量说明。
- 添加上游来源与检查记录，区分 npm 已发布功能和 MCP 主分支尚未发布的源码更新。

## 0.2.0 — 2026-10-09

- 新增 `yuque` 通用技能入口，按请求选择原有八个语雀工作流。
- 添加统一入口的界面元数据、默认提示和 `yuque-mcp` 依赖声明。
- 添加 Agent Plugins 1.0 根清单 `plugin.json` 和 stdio `mcp.json`，保留 Codex 兼容配置和 Token 环境变量转发声明。
- 更新安装、升级和故障排查说明，区分技能入口、插件展示名称和 MCP 连接状态。

## 0.1.1

- 调整为一个市场索引和独立插件目录的仓库结构。
