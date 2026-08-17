# 语雀 Codex 插件

一个面向 ChatGPT 和 Codex 的语雀知识库插件。它将语雀 MCP 工具和一组可复用技能打包在一起，可以搜索、阅读、总结、整理和维护个人语雀知识库。

## 功能

- 使用自然语言搜索个人语雀知识库
- 阅读并总结文档或知识库
- 整理、润色和结构化笔记
- 记录碎片想法和制作阅读笔记
- 发现知识关联、检查过期内容和分析写作风格

## 安装

需要先安装 Node.js、npm，以及支持插件的 ChatGPT/Codex 桌面应用。

添加这个 GitHub 插件市场：

```powershell
codex plugin marketplace add LaoYutang/yuque-codex-plugin
```

重启桌面应用，在插件目录中选择 `LaoYutang Plugins`，然后安装“语雀”。

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

## 使用示例

- `@yuque 找找英维克空调的通讯协议`
- `@yuque 总结这篇语雀文档`
- `@yuque 帮我整理一下最近的想法`

## 目录结构

```text
.agents/plugins/marketplace.json   GitHub 插件市场清单
plugins/yuque/                     插件包
  .codex-plugin/plugin.json        插件清单
  .mcp.json                        语雀 MCP 配置
  assets/icon.png                  插件图标
  skills/                          语雀工作流技能
```

## 安全说明

- 仓库只声明环境变量名称，不包含你的语雀 Token。
- 每位使用者都应配置自己的 Token，并只授予必要权限。
- 插件通过固定版本的 `yuque-mcp@1.0.0` npm 包连接语雀。

## License

[MIT](LICENSE)
