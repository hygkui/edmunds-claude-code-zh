# Edmund's Claude Code Setup (中文版)

我的个人 Claude Code 配置,用于高效 Web 开发。这个插件提供了 **14 个斜杠命令** 和 **11 个专业 AI 代理**,让你的开发工作流程如虎添翼。

## 快速安装

```bash
# 步骤 1: 添加 marketplace
/plugin marketplace add edmund-io/edmunds-claude-code

# 步骤 2: 安装插件
/plugin install edmunds-claude-code
```

## 内容概览

### 📋 开发命令 (7 个)

- `/new-task` - 分析代码性能问题
- `/code-explain` - 生成详细说明
- `/code-optimize` - 性能优化
- `/code-cleanup` - 重构和清理
- `/feature-plan` - 功能实现规划
- `/lint` - 代码检查和修复
- `/docs-generate` - 文档生成

### 🔌 API 命令 (3 个)

- `/api-new` - 创建新的 API 端点
- `/api-test` - 测试 API 端点
- `/api-protect` - 添加保护和验证

### 🎨 UI 命令 (2 个)

- `/component-new` - 创建 React 组件
- `/page-new` - 创建 Next.js 页面

### 💾 Supabase 命令 (2 个)

- `/types-gen` - 生成 TypeScript 类型
- `/edge-function-new` - 创建 Edge Functions

### 🤖 专业 AI 代理 (11 个)

**架构与规划**
- **tech-stack-researcher** - 技术选型推荐,包含权衡分析
- **system-architect** - 可扩展的系统架构设计
- **backend-architect** - 注重数据完整性和安全的后端系统
- **frontend-architect** - 高性能、可访问的 UI 架构
- **requirements-analyst** - 将想法转化为具体规范

**代码质量与性能**
- **refactoring-expert** - 系统性重构和代码整洁
- **performance-engineer** - 数据驱动的优化
- **security-engineer** - 漏洞识别和安全标准

**文档与研究**
- **technical-writer** - 清晰全面的文档
- **learning-guide** - 循序渐进的编程概念教学
- **deep-research-agent** - 自适应策略的全面研究

## 安装方法

### 从 GitHub 安装 (推荐)

```bash
# 添加 marketplace
/plugin marketplace add edmund-io/edmunds-claude-code

# 安装插件
/plugin install edmunds-claude-code
```

### 从本地克隆安装 (用于开发)

```bash
git clone https://github.com/edmund-io/edmunds-claude-code.git
cd edmunds-claude-code

# 添加为本地 marketplace
/plugin marketplace add /path/to/edmunds-claude-code

# 安装插件
/plugin install edmunds-claude-code
```

## 适用对象

- Next.js 开发者
- TypeScript 项目
- Supabase 用户
- React 开发者
- 全栈工程师

## 使用示例

### 规划功能

```bash
/feature-plan
# 然后描述你的功能想法
```

### 创建 API

```bash
/api-new
# Claude 将搭建一个完整的 API 路由,包含类型、验证和错误处理
```

### 研究技术选型

只需向 Claude 提问,例如:
- "我应该使用 WebSockets 还是 SSE?"
- "我应该如何构建这个数据库?"
- "X 的最佳库是什么?"

tech-stack-researcher 代理会自动激活,并提供详细、有研究依据的答案。

## 设计理念

这个配置强调:
- **类型安全**: 从不使用 `any` 类型
- **最佳实践**: 遵循现代 Next.js/React 模式
- **生产力**: 减少重复的脚手架工作
- **研究**: AI 驱动的技术决策,有据可循

## 系统要求

- Claude Code 2.0.13+
- 适用于任何项目(针对 Next.js + Supabase 优化)

## 自定义配置

安装后,你可以通过编辑 `.claude/commands/` 和 `.claude/agents/` 中的文件来自定义任何命令。

## 贡献

欢迎:
- Fork 并按需定制
- 提交问题或建议
- 分享你的改进

## 许可证

MIT - 在你的项目中自由使用

## 作者

由 Edmund 创建

---

**注意**: 这是我个人优化的配置。命令针对 Next.js + Supabase 工作流进行了优化,但也适用于任何现代 Web 技术栈。
