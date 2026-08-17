# 添加插件

这个仓库按“一份市场清单、多个独立插件包”的方式组织。新增插件时，请保持插件之间互不依赖，避免把某个插件的专属文件放在仓库根目录。

## 步骤

1. 在 `plugins/<plugin-name>/` 下创建插件目录。
2. 添加必需的 `.codex-plugin/plugin.json`。
3. 按需添加 `.mcp.json`、`skills/`、`assets/` 和插件自己的 `README.md`。
4. 在 `.agents/plugins/marketplace.json` 的 `plugins[]` 中追加插件条目，`source` 指向 `./plugins/<plugin-name>`。
5. 校验插件清单和 JSON 文件，并确认版本号已正确递增。
6. 检查提交内容，确保没有 Token、密码、私钥或其他凭据。

## 最小目录结构

```text
plugins/<plugin-name>/
├── .codex-plugin/plugin.json
├── README.md
└── ...
```

插件名称应使用小写字母、数字和连字符，并与市场清单中的 `name` 保持一致。
