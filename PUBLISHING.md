# 发布指南：Edmund 的 Claude Code 插件

将你的 Claude Code 插件发布到 GitHub 并供他人安装的完整分步说明。

## 前置条件

- [ ] GitHub 账户
- [ ] 本地已安装 Git
- [ ] 仓库已重命名为 `edmunds-claude-code` ✅
- [ ] 所有配置文件已更新 ✅

## 步骤 1：创建 GitHub 仓库

### 1.1 在 GitHub 上创建新仓库

1. 访问 https://github.com/new
2. 填写详情：
   - **仓库名称**：`edmunds-claude-code`
   - **描述**："Edmund's personal Claude Code setup with 14 productivity commands and 11 specialized AI agents for modern web development"
   - **可见性**：Public（公开，以便其他人可以安装）
   - **初始化**：❌ 不要添加 README、.gitignore 或 license（我们已经有了这些）
3. 点击"Create repository"

### 1.2 推送本地仓库

GitHub 仓库创建完成后，运行以下命令：

```bash
cd ~/Documents/GitHub/edmunds-claude-code

# 添加 GitHub 远程仓库
git remote add origin https://github.com/edmund-io/edmunds-claude-code.git

# 推送代码
git push -u origin main
```

如果遇到身份验证问题：
- 使用 Personal Access Token 代替密码
- 或设置 SSH 密钥（推荐）：https://docs.github.com/en/authentication/connecting-to-github-with-ssh

## 步骤 2：验证安装是否正常工作

测试插件是否可以安装：

```bash
# 从你的 GitHub 仓库安装
/plugin install edmund-io/edmunds-claude-code

# 验证命令可用
/code-explain
/feature-plan

# 验证 agent 可用（它们会根据上下文自动激活）
```

如需卸载并重新测试：
```bash
/plugin uninstall edmunds-claude-code
```

## 步骤 3：分享你的插件

你的 README 已经包含了你的 GitHub 用户名 `edmund-io`，所以用户可以直接复制粘贴命令！

### 方案 A：分享直接安装命令

与他人分享此命令：

```bash
/plugin install edmund-io/edmunds-claude-code
```

### 方案 B：提交到社区市场

#### Claude Code Plugins Marketplace
1. 访问 https://claudecodemarketplace.com/
2. 遵循他们的提交指南
3. 分享你的插件详情

#### CC Plugins Curated Marketplace
1. 访问 https://github.com/ccplugins/marketplace
2. Fork 该仓库
3. 将你的插件添加到他们的 `marketplace.json`
4. 创建 Pull Request，格式如下：

```json
{
  "name": "edmunds-claude-code",
  "source": "edmund-io/edmunds-claude-code",
  "description": "Personal Claude Code configuration with 14 productivity commands and 11 specialized AI agents for modern web development",
  "version": "1.0.0",
  "author": "Edmund",
  "tags": ["productivity", "nextjs", "supabase", "typescript", "react", "development"]
}
```

#### Claude Code Plugins Plus
1. 访问 https://github.com/jeremylongshore/claude-code-plugins-plus
2. 遵循他们的贡献指南
3. 提交你的插件详情

### 方案 C：在社交媒体上分享

示例帖子：

```
🚀 刚将我的 Claude Code 设置发布为插件！

14 个斜杠命令 + 11 个专用 AI agent，助力高效 Web 开发

安装方式：
/plugin install edmund-io/edmunds-claude-code

功能特性：
✅ API 脚手架 (/api-new)
✅ 代码优化 (/code-optimize)
✅ 功能规划 (/feature-plan)
✅ 技术研究 agent
✅ 架构 agent
✅ 安全与性能 agent

完美适用于 Next.js、React、TypeScript 和 Supabase 项目！

GitHub: https://github.com/edmund-io/edmunds-claude-code
```

## 步骤 5：维护你的插件

### 更新插件

当你对本地设置进行更改时：

```bash
cd ~/Documents/GitHub/edmunds-claude-code

# 对命令/agent 进行更改
# 然后提交并推送

git add .
git commit -m "Add new command: /new-command-name"

# 在 plugin.json 中更新版本
# 提升版本：1.0.0 -> 1.1.0

git add .claude-plugin/plugin.json
git commit -m "Bump version to 1.1.0"

git push
```

用户可以更新到最新版本：
```bash
/plugin update edmunds-claude-code
```

### 版本控制指南

- **1.0.x** - Bug 修复和小幅调整
- **1.x.0** - 添加新命令或 agent
- **x.0.0** - 重大重构或破坏性更改

## 故障排除

### 问题：插件无法安装

检查：
- 仓库在 GitHub 上是否为公开
- `.claude-plugin/plugin.json` 是否存在于仓库根目录
- JSON 文件是否具有有效语法（无尾随逗号、正确的引号）

### 问题：命令不显示

检查：
- `plugin.json` 中的命令文件路径是否与实际文件位置匹配
- 命令文件是否具有 `.md` 扩展名
- 命令文件是否不为空

### 问题：Agent 不激活

检查：
- `plugin.json` 中的 agent 文件路径是否与实际文件位置匹配
- Agent 文件是否具有正确的前言（frontmatter），包含 `name` 和 `description`
- Agent 根据上下文激活，而非通过命令

## 高级：创建发布版本

对于主要版本，创建 GitHub releases：

1. 访问你的仓库：https://github.com/edmund-io/edmunds-claude-code
2. 点击"Releases" → "Create a new release"
3. 标签版本：`v1.0.0`
4. 发布标题：`v1.0.0 - Initial Release`
5. 描述：功能/更改列表
6. 点击"Publish release"

用户可以安装特定版本：
```bash
/plugin install edmund-io/edmunds-claude-code@v1.0.0
```

## 成功指标

跟踪插件的成功：
- ⭐ GitHub stars
- 👁️ GitHub watchers
- 🍴 GitHub forks
- 💬 Issues 和讨论
- 📊 克隆/下载计数（GitHub Insights）

## 获取帮助

如果遇到问题：
- Claude Code 文档：https://docs.claude.com/en/docs/claude-code/plugin-marketplaces
- GitHub Issues：https://github.com/anthropics/claude-code/issues
- 社区：在 GitHub 上搜索 Claude Code 插件

---

**恭喜！** 发布后，你的插件将可供 Claude Code 社区使用和学习。快乐分享！ 🎉
