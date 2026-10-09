# 语雀插件

一个面向支持本地 MCP 的 Codex 桌面环境的语雀知识库插件。它将语雀 MCP 工具、`yuque` 统一入口和八个专用技能打包在一起，可以搜索、阅读、总结、整理和维护个人语雀知识库。其他宿主需支持 stdio MCP 并配置凭据转发；云端环境需要单独配置运行依赖和 Token。

当前版本：**0.2.1**。

## 功能

- 使用自然语言搜索个人语雀知识库
- 阅读并总结文档或知识库
- 整理、润色和结构化笔记
- 记录碎片想法和制作阅读笔记
- 发现知识关联、检查过期内容和分析写作风格

## 安装

需要先安装 Node.js 18 或以上版本、npm，以及支持本地插件和 stdio MCP 的 Codex 桌面应用或 CLI。

添加 GitHub 插件市场并安装语雀插件：

```powershell
codex plugin marketplace add LaoYutang/codex-plugins
codex plugin add yuque@laoyutang-plugins
```

安装后请重启桌面应用，并在新任务中使用插件。

## 从旧版本更新

在本版本发布到 GitHub 市场后，刷新市场并重新安装：

```powershell
codex plugin marketplace upgrade laoyutang-plugins
codex plugin add yuque@laoyutang-plugins
```

完全退出并重新打开桌面应用，再新建聊天。市场升级会刷新索引和源码快照，已安装插件仍需重新安装。可以用 `codex plugin list --json` 检查安装版本。

开发时也可直接从当前源码所在的本地市场安装：

```powershell
codex plugin marketplace add .
codex plugin add yuque@laoyutang-plugins
```

上面的 `.` 必须是包含 `.agents/plugins/marketplace.json` 的仓库根目录。

## 配置语雀 Token

插件通过环境变量 `YUQUE_PERSONAL_TOKEN` 读取你的个人语雀 Token。不要把 Token 写进仓库或提交到 Git。

当前 PowerShell 会话临时设置：

```powershell
$env:YUQUE_PERSONAL_TOKEN = "你的语雀 Token"
```

为当前 Windows 用户持久设置：

```powershell
[Environment]::SetEnvironmentVariable(
  "YUQUE_PERSONAL_TOKEN",
  "你的语雀 Token",
  "User"
)
```

持久设置后请重新启动桌面应用。

Token 必须配置在实际运行 MCP 服务的环境中。桌面电脑的环境变量不会自动传到远程或云端任务。

### 可选：自定义语雀 API 地址

默认连接 `https://www.yuque.com/api/v2`。需要连接其他语雀站点时，在运行 MCP 的环境中设置完整 API 地址：

```powershell
$env:YUQUE_BASE_URL = "https://your-space.yuque.com/api/v2"
```

如需持久设置，可用上面的 `SetEnvironmentVariable` 方法设置 `YUQUE_BASE_URL`，然后重启桌面应用。插件的 Codex 兼容配置会转发这个变量；地址应包含 `/api/v2`，不能只填写站点域名。

当前固定的 npm 正式版 `1.0.0` 使用 `YUQUE_PERSONAL_TOKEN` 和可选的 `YUQUE_BASE_URL`。MCP 主分支新增的 `YUQUE_TOKEN`、`YUQUE_HOST` 尚未进入该正式版，配置本插件时请使用正式版支持的变量。

## 使用示例

在桌面应用支持 `@` 技能选择的输入框中输入 `@`，搜索 `yuque` 并选择 **yuque · 语雀**。如果客户端显示完整命名空间名称，例如 `yuque:yuque`，请选择该项。

- `@yuque 找找英维克空调的通讯协议`
- `@yuque 总结这篇语雀文档`
- `@yuque 帮我整理一下最近的想法`

这里的 `@yuque` 指新增的统一技能入口。Codex CLI 使用 `$yuque`，或选择客户端列出的完整技能名。也可以直接说“用语雀搜索……”，让模型按请求匹配技能。

| 专用技能 | 用途 |
| --- | --- |
| `smart-search` | 搜索知识库并回答问题 |
| `smart-summary` | 阅读、总结文档或知识库 |
| `note-refine` | 整理和润色笔记 |
| `daily-capture` | 记录想法和整理碎片 |
| `knowledge-connect` | 发现文档关联 |
| `reading-digest` | 制作阅读笔记 |
| `stale-detector` | 检查过期内容 |
| `style-extract` | 分析和应用写作风格 |

## 为什么以前只能选择八个技能？

0.1.1 只打包了上面八个技能，没有 `name: yuque` 的通用技能。插件清单中的 `name: yuque` 是包标识，`interface.displayName` 是插件展示名称；它们不会自动生成同名技能入口。因此，技能选择器中只有那八项与旧版包内容一致，并不能单凭这一现象判断 MCP 连接失败。

0.2.0 新增 `skills/yuque/SKILL.md` 和该技能的 `agents/openai.yaml`，提供统一入口、界面名称、默认提示和 MCP 依赖声明。它根据请求加载对应的专用工作流，原有八项仍可独立选择。

插件或连接应用能否作为独立的 `@` 项出现，也取决于产品界面和连接类型。本地 stdio MCP 不会因为填写展示名称就变成已注册的远程连接应用。本版本通过通用技能提供 `yuque` 入口；在支持的 Codex 任务界面中也可以从 **Sources → Use plugins** 选择已安装插件。参见 [OpenAI 插件使用说明](https://help.openai.com/en/articles/20001256-plugins-in-codexOpenAI)。

## 插件规范更新

按 2026-10-09 查阅的 [OpenAI 打包文档](https://developers.openai.com/plugins/build/plugins)，新包推荐使用 Agent Plugins 1.0：

- 根目录 `plugin.json` 声明标准 Schema、包名称和版本。
- `skills/` 自动发现技能；根目录 `mcp.json` 声明 MCP 服务和明确的传输类型。
- OpenAI 专有展示信息放在 `extensions.com.openai.interface`。
- 旧 `.codex-plugin/plugin.json` 仍受支持；本插件同时保留它和 `.mcp.json`，兼容旧客户端并声明 `YUQUE_PERSONAL_TOKEN` 和 `YUQUE_BASE_URL` 的环境变量转发。

便携 MCP 标准没有任意环境变量占位符或 `env_vars` 字段，所以 `mcp.json` 不写 Token，也不使用 `${YUQUE_PERSONAL_TOKEN}`。支持环境覆盖的 Codex 运行时从兼容配置中读取同名服务的 `env_vars`；其他宿主需自行设置凭据传递。Token 配置失败时应检查实际运行环境。参见 [Agent Plugins MCP 规范](https://agent-plugins.org/plugin-authors/mcp-servers)及 [Codex 环境覆盖实现](https://github.com/openai/codex/blob/main/codex-rs/core-plugins/src/agent_plugin_mcp_overlay.rs)。

## 排查入口与连接

- **仍然只有八个技能**：确认已安装版本为 `0.2.1`，重新安装后重启应用并新建聊天，搜索 `yuque` 或完整技能名称。
- **有 `yuque` 入口，但没有工具**：检查插件是否启用，运行环境中的 Node.js/npm 是否可用，以及 `yuque-mcp` 服务是否启动成功。
- **工具返回认证或权限错误**：在 MCP 所在环境中检查 `YUQUE_PERSONAL_TOKEN` 的配置和语雀访问权限，不要把 Token 发到聊天或写进插件文件。
- **自定义站点连接失败**：检查 MCP 所在环境中的 `YUQUE_BASE_URL` 是否为包含 `/api/v2` 的完整 API 地址，以及当前 Codex 是否支持兼容配置的环境变量转发。
- **在远程或云端任务中不可用**：在该执行环境单独安装依赖、连接 MCP 和配置 Token，再新建聊天。

## 上游来源与同步

八个专用技能来自 [yuque/yuque-ecosystem](https://github.com/yuque/yuque-ecosystem)，MCP 来自 [yuque/yuque-mcp-server](https://github.com/yuque/yuque-mcp-server)。`yuque` 统一入口由本插件维护。

0.2.1 已同步八个技能的最新兼容声明，并修正三个技能中列知识库的调用示例：通过 `yuque_get_user` 获取 `login` 后传给 `yuque_list_books`。MCP 保持官方 npm 正式版 `1.0.0`，并补充该版本已支持的自定义 API 地址转发。检查日期、提交和本地兼容调整见 [UPSTREAM.md](UPSTREAM.md)。

## 安全说明

- 仓库只声明环境变量名称，不包含你的语雀 Token。
- 每位使用者都应配置自己的 Token，并只授予必要权限。
- 插件通过固定版本的 `yuque-mcp@1.0.0` npm 包连接语雀。

## License

[MIT](../../LICENSE)
