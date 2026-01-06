---
description: 运行 linting 并修复代码质量问题
model: claude-sonnet-4-5
---

在代码库中运行 linting 并修复代码质量问题。

## 目标

$ARGUMENTS

## 独立开发者 Lint 策略

### 1. **运行 Linting 命令**

```bash
# ESLint（JavaScript/TypeScript）
npm run lint
npx eslint . --fix

# TypeScript 编译器
npx tsc --noEmit

# Prettier（格式化）
npx prettier --write .

# 全部一起
npm run lint && npx tsc --noEmit && npx prettier --write .
```

### 2. **常见 ESLint 问题**

**TypeScript 错误**
- 缺少类型注解
- 使用了 `any` 类型
- 未使用的变量
- 缺少返回类型

**React/Next.js 问题**
- 列表中缺少 keys
- 不安全的 useEffect 依赖
- JSX 中未转义的实体
- 图片上缺少 alt 文本

**代码质量**
- 未使用的导入
- Console.log 语句
- Debugger 语句
- TODO 注释

**最佳实践**
- 不使用 var，使用 const/let
- 优先使用 const 而不是 let
- 不使用嵌套三元运算符
- 一致的 return 语句

### 3. **自动修复你能修复的**

**安全的自动修复**
```bash
# 修复格式化
prettier --write .

# 修复 ESLint 可自动修复的规则
eslint --fix .

# 修复导入顺序
eslint --fix --rule 'import/order: error' .
```

**需要手动修复**
- 类型注解
- 逻辑错误
- 缺少错误处理
- 可访问性问题

### 4. **Lint 配置**

**ESLint 配置**（`.eslintrc.json`）
```json
{
  "extends": [
    "next/core-web-vitals",
    "plugin:@typescript-eslint/recommended"
  ],
  "rules": {
    "@typescript-eslint/no-explicit-any": "error",
    "@typescript-eslint/no-unused-vars": "error",
    "no-console": "warn"
  }
}
```

**Prettier 配置**（`.prettierrc`）
```json
{
  "semi": false,
  "singleQuote": true,
  "tabWidth": 2,
  "trailingComma": "es5"
}
```

### 5. **优先级修复**

**高优先级**（立即修复）
- 阻塞构建的类型错误
- 安全漏洞
- 运行时错误
- 可访问性问题

**中等优先级**（提交前修复）
- 缺少类型注解
- 未使用的变量
- 代码风格违规
- TODO 注释

**低优先级**（方便时修复）
- 格式不一致
- 注释改进
- 小的重构机会

### 6. **预提交钩子**（推荐）

**安装 Husky + lint-staged**
```bash
npm install -D husky lint-staged
npx husky init
```

**配置**（`.husky/pre-commit`）
```bash
npx lint-staged
```

**lint-staged 配置**（`package.json`）
```json
{
  "lint-staged": {
    "*.{js,jsx,ts,tsx}": [
      "eslint --fix",
      "prettier --write"
    ]
  }
}
```

### 7. **VSCode 集成**

**设置**（`.vscode/settings.json`）
```json
{
  "editor.formatOnSave": true,
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true
  },
  "typescript.tsdk": "node_modules/typescript/lib"
}
```

## 生成内容

1. **Lint 报告** - 发现的所有问题
2. **自动修复结果** - 自动修复的内容
3. **手动修复建议** - 需要手动干预的问题
4. **优先级列表** - 按严重程度排序
5. **配置建议** - 改进 lint 设置

## 常见修复

**移除未使用的导入**
```typescript
// 之前
import { A, B, C } from 'lib'

// 之后
import { A, C } from 'lib'  // B 未使用
```

**添加类型注解**
```typescript
// 之前
function process(data) {
  return data.map(x => x.value)
}

// 之后
function process(data: DataItem[]): number[] {
  return data.map(x => x.value)
}
```

**修复缺少的 Keys**
```typescript
// 之前
{items.map(item => <div>{item.name}</div>)}

// 之后
{items.map(item => <div key={item.id}>{item.name}</div>)}
```

专注于改进代码质量和防止错误的修复。在每次提交前运行 linting。
