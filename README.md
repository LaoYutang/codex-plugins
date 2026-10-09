# LaoYutang Codex Plugins

这是一个可扩展的 ChatGPT / Codex 插件市场仓库。每个插件独立存放在 `plugins/<plugin-name>/`，统一由 `.agents/plugins/marketplace.json` 提供安装索引。

## 安装市场

```powershell
codex plugin marketplace add LaoYutang/codex-plugins
```

查看可用插件：

```powershell
codex plugin list
```

## 可用插件

| 插件 | 说明 | 版本 |
| --- | --- | --- |
| [语雀](plugins/yuque/) | 通过 `yuque` 统一入口搜索、阅读、总结和整理个人语雀知识库 | 0.2.0 |

安装语雀插件：

```powershell
codex plugin add yuque@laoyutang-plugins
```

安装后重启桌面应用并新建聊天。在支持 `@` 技能选择的输入框中搜索 `yuque`，选择 `yuque · 语雀`；Codex CLI 使用 `$yuque`（以客户端显示的完整技能名称为准）。该入口会根据请求选择合适的语雀工作流，原有八个专用技能也可继续使用。

## 更新市场

```powershell
codex plugin marketplace upgrade laoyutang-plugins
```

市场更新后，如需升级某个已安装插件，请重新安装该插件，并在新任务中使用：

```powershell
codex plugin add yuque@laoyutang-plugins
```

## 仓库结构

```text
.
├── .agents/plugins/marketplace.json
├── plugins/
│   └── yuque/
│       ├── plugin.json
│       ├── mcp.json
│       ├── .codex-plugin/plugin.json
│       ├── .mcp.json
│       ├── assets/
│       ├── skills/
│       └── README.md
├── CONTRIBUTING.md
└── README.md
```

新增插件时，在 `plugins/<plugin-name>/` 创建独立插件包，并向市场清单的 `plugins[]` 追加一项。具体步骤见 [CONTRIBUTING.md](CONTRIBUTING.md)。

新格式使用 Agent Plugins 1.0 的根清单 `plugin.json` 和 `mcp.json`，同时保留 Codex 兼容配置。规范变化及 `@yuque` 入口的说明见[语雀插件 README](plugins/yuque/README.md)。

## License

[MIT](LICENSE)
