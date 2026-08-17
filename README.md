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
| [语雀](plugins/yuque/) | 搜索、阅读、总结和整理个人语雀知识库 | 0.1.1 |

安装语雀插件：

```powershell
codex plugin add yuque@laoyutang-plugins
```

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
│       ├── .codex-plugin/plugin.json
│       ├── .mcp.json
│       ├── assets/
│       ├── skills/
│       └── README.md
├── CONTRIBUTING.md
└── README.md
```

新增插件时，在 `plugins/<plugin-name>/` 创建独立插件包，并向市场清单的 `plugins[]` 追加一项。具体步骤见 [CONTRIBUTING.md](CONTRIBUTING.md)。

## License

[MIT](LICENSE)
