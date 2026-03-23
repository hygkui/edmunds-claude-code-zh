# Repository Guidelines

## 项目结构与模块组织
这个仓库是 Claude Code 插件配置，不是可直接运行的应用。根目录放用户文档：`README.md`、`QUICK-START.md`、`PUBLISHING.md`。`.claude-plugin/` 保存插件元数据，其中 `plugin.json` 定义命令、agents 和 MCP servers，`marketplace.json` 定义市场信息。斜杠命令放在 `.claude/commands/`，按领域拆分到 `api/`、`misc/`、`supabase/`、`ui/`。Agent 定义放在 `.claude/agents/`。`.claude/settings.local.json` 是本地配置，不要提交。

## 构建、测试与开发命令
仓库没有传统的构建流程，提交前以清单校验和手工验证为主：

```bash
python -m json.tool .claude-plugin/plugin.json
python -m json.tool .claude-plugin/marketplace.json
git diff --check
```

功能验证建议本地安装插件后执行受影响命令：

```bash
/plugin marketplace add /path/to/edmunds-claude-code
/plugin install edmunds-claude-code
/code-explain
```

如果移动或重命名命令、agent 文件，必须在同一提交里同步更新 `plugin.json`。

## 编码风格与命名约定
仓库主要使用 Markdown 和 JSON。JSON 统一 2 空格缩进。提示词内容保持简洁、面向任务，风格与现有中文本地化文件一致。文件名、命令名、agent 名使用 kebab-case，例如 `code-cleanup.md`、`technical-writer.md`。命令描述使用明确的动宾短语；Markdown 通常保留一个清晰的一级标题，只有确实需要时再加 frontmatter。

## 测试指南
仓库未包含自动化测试，因此每次修改都要做手工验证。至少执行一次 JSON 解析校验，并安装插件后检查一个受影响的命令或 agent 路径。若只改文档，请重点检查标题层级、代码块和安装命令是否可读且一致。

## 提交与 Pull Request 规范
现有提交信息以简短英文祈使句为主，例如 `Add Chinese localization (中文版)`、`Fix marketplace.json schema validation errors`。继续使用 `Add ...`、`Fix ...`、`Update ...`、`Move ...` 这类格式。PR 需说明用户可见改动、列出修改过的命令或 agent 路径，并附上执行过的验证步骤。只有当文档配图或市场展示素材变更时才需要截图。发布用户可见版本时，记得同步更新 `.claude-plugin/plugin.json` 中的版本号。

## 安全与配置提示
不要在设置文件、提示词或文档中提交密钥、令牌或个人机器路径。保持 `.claude/settings.local.json` 为忽略状态；可共享的默认配置放在 `.claude/settings.template.json`。
