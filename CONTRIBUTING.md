# 添加插件

这个仓库按“一份市场清单、多个独立插件包”的方式组织。新增插件时，请保持插件之间互不依赖，避免把某个插件的专属文件放在仓库根目录。

## 步骤

1. 在 `plugins/<plugin-name>/` 下创建插件目录。
2. 添加 Agent Plugins 1.0 根清单 `plugin.json`，声明对应的 `$schema`；将 OpenAI 界面元数据放在 `extensions.com.openai.interface`。
3. 按需添加根目录 `mcp.json`、`skills/`、`assets/` 和插件自己的 `README.md`。每个 MCP 服务必须声明传输类型，例如 `"type": "stdio"`。为较旧的 Codex 客户端保留 `.codex-plugin/plugin.json` 和 `.mcp.json` 时，两套配置的名称、版本、界面元数据和 MCP 启动命令应保持一致。
4. 在 `.agents/plugins/marketplace.json` 的 `plugins[]` 中追加插件条目，`source` 指向 `./plugins/<plugin-name>`。
5. 使用对应的 JSON Schema 校验根清单及 MCP 配置，检查所有技能的 YAML 前置元数据和相对路径，并确认版本号已正确递增。
6. 检查提交内容，确保没有 Token、密码、私钥或其他凭据。

## 最小目录结构

```text
plugins/<plugin-name>/
├── plugin.json
├── README.md
└── ...
```

插件名称应使用小写字母、数字和连字符，并与市场清单中的 `name` 保持一致。

插件清单的 `name` 和 `interface.displayName` 不会自动创建同名技能。如需一个通用入口，在 `skills/<plugin-name>/SKILL.md` 中声明对应的技能名称，再将请求路由到专用技能。技能选择器的显示名称和默认提示应放在该技能的 `agents/openai.yaml` 中，使用 `display_name` 等 snake_case 字段。

便携 `mcp.json` 不支持 Codex 的 `env_vars` 或超时字段，也不支持 `${YUQUE_PERSONAL_TOKEN}` 这类任意环境变量占位符。认证由宿主管理；本仓库通过兼容 `.mcp.json` 声明需要转发的环境变量名称，并保留 `.codex-plugin/plugin.json` 对它的引用。支持该环境覆盖的 Codex 运行时会把同名服务的 `env_vars` 应用到便携配置；其他宿主需要自行配置凭据转发。

参考 [OpenAI 插件打包文档](https://developers.openai.com/plugins/build/plugins)、[技能文档](https://developers.openai.com/plugins/build/skills)和 [Agent Plugins MCP 规范](https://agent-plugins.org/plugin-authors/mcp-servers)。
