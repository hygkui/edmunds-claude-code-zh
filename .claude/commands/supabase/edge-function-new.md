---
description: 使用 Deno 创建新的 Supabase Edge Function
model: claude-sonnet-4-5
---

创建新的 Supabase Edge Function。

## 函数规格

$ARGUMENTS

## Supabase Edge Functions 概述

Edge Functions 运行在 Deno Deploy 上（而非 Node.js）：
- 支持 TypeScript/JavaScript
- 在全球边缘运行
- 访问 Supabase 客户端
- HTTP 触发器
- 快速冷启动

## 创建 Edge Function

### 1. **初始化函数**

```bash
npx supabase functions new function-name
```

### 2. **函数结构**

```typescript
// supabase/functions/function-name/index.ts
import { serve } from 'https://deno.land/std@0.168.0/http/server.ts'
import { createClient } from 'https://esm.sh/@supabase/supabase-js@2'

serve(async (req: Request) => {
  try {
    // 1. 解析请求
    const { data } = await req.json()

    // 2. 创建 Supabase 客户端
    const supabaseClient = createClient(
      Deno.env.get('SUPABASE_URL') ?? '',
      Deno.env.get('SUPABASE_ANON_KEY') ?? '',
      {
        global: {
          headers: {
            Authorization: req.headers.get('Authorization')!
          }
        }
      }
    )

    // 3. 验证用户（如果需要）
    const {
      data: { user },
      error: authError
    } = await supabaseClient.auth.getUser()

    if (authError || !user) {
      return new Response(
        JSON.stringify({ error: 'Unauthorized' }),
        { status: 401, headers: { 'Content-Type': 'application/json' } }
      )
    }

    // 4. 业务逻辑
    const result = await processData(data, user)

    // 5. 返回响应
    return new Response(
      JSON.stringify({ data: result }),
      {
        status: 200,
        headers: {
          'Content-Type': 'application/json',
          'Access-Control-Allow-Origin': '*'
        }
      }
    )
  } catch (error) {
    return new Response(
      JSON.stringify({ error: error.message }),
      {
        status: 500,
        headers: { 'Content-Type': 'application/json' }
      }
    )
  }
})
```

### 3. **常见用例**

**Webhook 处理器**
```typescript
serve(async (req) => {
  const signature = req.headers.get('stripe-signature')
  // 验证 webhook 签名
  // 处理事件
  return new Response('OK', { status: 200 })
})
```

**定时函数**（使用 pg_cron）
```typescript
serve(async () => {
  // 运行日常清理、发送邮件等
  const supabase = createClient(url, serviceKey)
  await supabase.from('old_records').delete().lt('created_at', oldDate)
  return new Response('Done', { status: 200 })
})
```

**API 代理/转换**
```typescript
serve(async (req) => {
  const apiKey = Deno.env.get('THIRD_PARTY_API_KEY')
  const response = await fetch('https://api.example.com/data', {
    headers: { 'Authorization': `Bearer ${apiKey}` }
  })
  const data = await response.json()
  // 转换并返回
  return new Response(JSON.stringify(data), { status: 200 })
})
```

### 4. **本地测试**

```bash
# 本地启动 Supabase
npx supabase start

# 本地运行函数
npx supabase functions serve function-name

# 使用 curl 测试
curl -X POST http://localhost:54321/functions/v1/function-name \
  -H "Authorization: Bearer YOUR_ANON_KEY" \
  -H "Content-Type: application/json" \
  -d '{"key":"value"}'
```

### 5. **部署函数**

```bash
# 部署到 Supabase
npx supabase functions deploy function-name

# 设置密钥
npx supabase secrets set API_KEY=your-secret-key

# 查看日志
npx supabase functions logs function-name
```

### 6. **从前端调用**

```typescript
// 使用 Supabase 客户端
const { data, error } = await supabase.functions.invoke('function-name', {
  body: { key: 'value' }
})

// 直接 fetch
const response = await fetch(
  `${SUPABASE_URL}/functions/v1/function-name`,
  {
    method: 'POST',
    headers: {
      'Authorization': `Bearer ${SUPABASE_ANON_KEY}`,
      'Content-Type': 'application/json'
    },
    body: JSON.stringify({ key: 'value' })
  }
)
```

### 7. **最佳实践**

**安全性**
- ✓ 验证用户身份
- ✓ 使用 RLS 策略
- ✓ 验证所有输入
- ✓ 谨慎使用 service role key
- ✓ 正确设置 CORS 头

**性能**
- ✓ 保持函数小而专注
- ✓ 对大响应使用流式传输
- ✓ 尽可能使用缓存
- ✓ 处理超时（最多 150s）

**错误处理**
- ✓ 使用正确的 HTTP 状态码
- ✓ 保持一致的错误格式
- ✓ 记录错误以便调试
- ✓ 不要暴露敏感信息

**代码组织**
- ✓ 每个文件一个函数
- ✓ 将工具函数提取到共享文件夹
- ✓ 使用 TypeScript 以确保类型安全
- ✓ 从与 Deno 兼容的 URL 导入

### 8. **环境变量**

```bash
# 本地设置
echo "API_KEY=secret" > supabase/functions/.env

# 在生产环境中设置
npx supabase secrets set API_KEY=secret

# 在函数中访问
const apiKey = Deno.env.get('API_KEY')
```

### 9. **常见模式**

**CORS 处理**
```typescript
serve(async (req) => {
  if (req.method === 'OPTIONS') {
    return new Response('ok', {
      headers: {
        'Access-Control-Allow-Origin': '*',
        'Access-Control-Allow-Methods': 'POST',
        'Access-Control-Allow-Headers': 'authorization, content-type'
      }
    })
  }
  // 处理请求
})
```

**数据库访问**
```typescript
// 使用 RLS 读取（使用用户的 token）
const { data } = await supabaseClient
  .from('posts')
  .select('*')

// 管理员访问（绕过 RLS）
const supabaseAdmin = createClient(url, serviceRoleKey)
const { data } = await supabaseAdmin
  .from('posts')
  .select('*')
```

生成具有适当错误处理、身份验证和类型安全的生产级 Edge Functions。
