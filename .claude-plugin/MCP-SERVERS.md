# 包含的 MCP 服务器

此插件包含 3 个预配置的 MCP 服务器，可增强 Claude Code 的功能。

## 包含的服务器

### 1. **Context7** (`@upstash/context7-mcp`)
**用途**：访问任何库的最新、特定版本的文档

**使用方法**：在需要当前库文档时，只需在提示词中提及"use context7"

**优势**：
- 始终保持最新的文档
- 特定版本的信息
- 支持数千个库
- 无需手动搜索

### 2. **Playwright** (`@playwright/mcp`)
**用途**：浏览器自动化和 Web 测试

**功能**：
- 导航网站
- 截取屏幕截图
- 与 Web 元素交互
- 生成测试代码
- 访问可访问性树

**使用场景**：
- E2E 测试
- Web 爬虫
- 浏览器自动化
- 视觉测试

### 3. **Supabase** (`@supabase/mcp-server-supabase`)
**用途**：Supabase 数据库操作

**功能**：
- 查询数据库
- 管理表
- 执行 SQL
- 处理身份验证
- 使用存储

**使用场景**：
- 数据库管理
- 架构探索
- 数据查询
- 管理操作

## 未包含的服务器（暂不可用）

以下服务器已被请求，但尚未有官方 MCP 实现：

- **chrome-devtools** - 未找到官方 MCP 服务器
- **stripe** - 未找到官方 MCP 服务器（截至 2025 年 10 月）
- **vercel** - 未找到官方 MCP 服务器

## 使用 MCP 服务器

安装此插件后：

1. **自动激活**：使用插件时 MCP 服务器会自动启动
2. **需要重启**：插件安装后需重启 Claude Code
3. **工具访问**：MCP 工具会出现在 Claude 的可用工具列表中

## 添加更多 MCP 服务器

你可以将自定义 MCP 服务器添加到本地的 `.claude/.mcp.json`：

```json
{
  "server-name": {
    "command": "npx",
    "args": ["-y", "package-name"],
    "env": {
      "API_KEY": "your-key"
    }
  }
}
```

## 故障排除

**MCP 服务器无法加载？**
1. 重启 Claude Code
2. 检查是否安装了 npm/npx
3. 验证网络连接（MCP 服务器在首次使用时会下载）

**性能问题？**
- MCP 服务器按需运行
- 首次使用可能较慢（包下载）
- 后续使用会很快

## 了解更多

- 官方 MCP 文档：https://modelcontextprotocol.io
- Claude Code MCP 指南：https://docs.claude.com/en/docs/claude-code/mcp
- MCP 服务器目录：https://mcpcat.io
