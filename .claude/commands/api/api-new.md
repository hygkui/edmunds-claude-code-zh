---
description: 创建新的 Next.js API 路由，包含验证、错误处理和 TypeScript
model: claude-sonnet-4-5
---

为独立开发者创建遵循现代最佳实践的 Next.js API 路由。

## 需求

API 端点: $ARGUMENTS

## 实现指南

### 1. **Next.js 15 App Router**（推荐）
在 `app/api/` 目录中使用 Route Handlers 和 TypeScript

### 2. **验证**
- 使用 Zod 进行运行时类型验证
- 提前验证输入（在数据库/API 调用之前）
- 返回清晰的验证错误消息

### 3. **错误处理**
- 使用 try/catch 进行全局错误处理
- 一致的错误响应格式
- 适当的 HTTP 状态码
- 永不暴露敏感的错误详情

### 4. **TypeScript**
- 对请求/响应进行严格类型定义
- 共享类型定义
- 不使用 `any` 类型

### 5. **安全性**
- 输入清理
- 如需要则配置 CORS
- 考虑速率限制
- 身份验证/授权检查

### 6. **响应格式**
```typescript
// 成功
{ data: T, success: true }

// 错误
{ error: string, details?: unknown, success: false }
```

## 代码结构

创建完整的 API 路由，包含：

1. **路由处理文件** - `app/api/[route]/route.ts`
2. **验证模式** - 用于请求/响应的 Zod 模式
3. **类型定义** - 共享的 TypeScript 类型
4. **错误处理器** - 集中式错误处理
5. **使用示例** - 客户端 fetch 示例

## 遵循的最佳实践

- 在昂贵操作之前进行早期验证
- 使用适当的 HTTP 状态码（200, 201, 400, 401, 404, 500）
- 一致的错误响应格式
- TypeScript 严格模式
- 路由中的逻辑最小化（使用 services/utils）
- 环境变量验证
- 请求/响应日志记录以便调试
- 响应中不包含敏感数据
- 未经验证不得进行数据库查询
- 不得包含内联业务逻辑（提取到 services）

生成我可以立即在 Next.js 项目中使用的生产就绪代码。
