---
description: 为 API 端点添加身份验证、授权和安全性
model: claude-sonnet-4-5
---

为指定的 API 路由添加全面的安全性、身份验证和授权。

## 目标 API 路由

$ARGUMENTS

## 要实现的安全层

### 1. **身份验证**（你是谁？）
- 验证用户身份
- Token 验证（JWT、session、API keys）
- 处理过期/无效的 token

### 2. **授权**（你可以做什么？）
- 基于角色的访问控制（RBAC）
- 资源级别的权限
- 检查用户所有权

### 3. **输入验证**
- 清理所有输入
- SQL/NoSQL 注入防护
- XSS 防护
- 使用 Zod 进行类型验证

### 4. **速率限制**
- 防止滥用
- 每用户/IP 限制
- 滑动窗口算法

### 5. **CORS**（如需要）
- 将允许的来源加入白名单
- 正确的请求头
- 凭证处理

## 实现方法

### 对于 Supabase 项目：
```typescript
// 使用 Supabase Auth + RLS
- getUser() 从服务端客户端
- RLS 策略用于数据访问
- Service role key 用于管理员操作
```

### 对于 NextAuth.js 项目：
```typescript
// 使用 NextAuth sessions
- getServerSession() 在路由处理器中
- 使用 middleware 保护
- 角色检查逻辑
```

### 对于自定义 Auth：
```typescript
// JWT 验证
- 验证 token
- 解码并验证声明
- 检查过期时间
```

## 安全检查清单

**身份验证**
- 验证身份验证 token
- 处理缺失/无效的 token（401）
- 检查 token 过期时间
- 安全的 token 存储建议

**授权**
- 检查用户角色/权限（403）
- 验证资源所有权
- 实施最小权限原则
- 记录授权失败

**输入验证**
- 使用 Zod 验证所有输入
- 清理 SQL/NoSQL 输入
- 转义特殊字符
- 限制 payload 大小

**速率限制**
- 每用户限制
- 每 IP 限制
- 清晰的错误消息（429）
- Retry-After 请求头

**CORS**
- 将特定来源加入白名单
- 处理预检请求
- 保护凭证
- 适当的请求头

**错误处理**
- 不暴露堆栈跟踪
- 通用错误消息
- 在服务端记录详细错误
- 一致的错误格式

**日志和监控**
- 记录身份验证尝试
- 记录授权失败
- 跟踪可疑活动
- 监控速率限制命中

## 生成内容

1. **受保护的路由处理器** - API 路由的安全版本
2. **中间件/工具** - 可重用的 auth 助手
3. **类型定义** - User、permissions、roles
4. **错误响应** - 标准化的 auth 错误
5. **使用示例** - 客户端集成

## 独立开发者的常见模式

**模式 1: 简单 Token Auth**
```typescript
// 用于内部工具、管理面板
const token = request.headers.get('authorization')
if (token !== process.env.ADMIN_TOKEN) {
  return new Response('Unauthorized', { status: 401 })
}
```

**模式 2: 基于用户的 Auth**
```typescript
// 用于面向用户的应用
const user = await getCurrentUser(request)
if (!user) {
  return new Response('Unauthorized', { status: 401 })
}
```

**模式 3: 基于角色的 Auth**
```typescript
// 用于具有不同用户类型的应用
const user = await getCurrentUser(request)
if (!user || !hasRole(user, 'admin')) {
  return new Response('Forbidden', { status: 403 })
}
```

生成遵循最小权限原则的生产就绪安全代码。
