---
description: 从 Supabase 数据库 schema 生成 TypeScript 类型
model: claude-sonnet-4-5
---

从 Supabase 数据库 schema 生成 TypeScript 类型。

## 命令

运行以下命令来生成类型：

```bash
npx supabase gen types typescript --project-id YOUR_PROJECT_ID > lib/database.types.ts
```

或者使用本地 Supabase：

```bash
npx supabase gen types typescript --local > lib/database.types.ts
```

## 自动生成设置

### 1. **添加到 package.json**

```json
{
  "scripts": {
    "gen-types": "npx supabase gen types typescript --project-id $SUPABASE_PROJECT_ID > lib/database.types.ts",
    "gen-types:local": "npx supabase gen types typescript --local > lib/database.types.ts"
  }
}
```

### 2. **在代码中使用**

```typescript
import type { Database } from '@/lib/database.types'

// 获取表类型
type User = Database['public']['Tables']['users']['Row']
type UserInsert = Database['public']['Tables']['users']['Insert']
type UserUpdate = Database['public']['Tables']['users']['Update']

// 与 Supabase 客户端一起使用
const supabase = createClient<Database>(url, key)

// 类型安全的查询
const { data } = await supabase
  .from('users')
  .select('*')
  .single()  // data 被类型化为 User

// 类型安全的插入
const { data } = await supabase
  .from('users')
  .insert({
    email: 'user@example.com',
    name: 'John Doe'
  })  // TypeScript 会验证数据结构
```

### 3. **创建工具类型**

```typescript
// lib/database.helpers.ts
import type { Database } from './database.types'

// 提取表类型
export type Tables<T extends keyof Database['public']['Tables']> =
  Database['public']['Tables'][T]['Row']

export type Enums<T extends keyof Database['public']['Enums']> =
  Database['public']['Enums'][T]

// 使用示例
import type { Tables } from '@/lib/database.helpers'
type User = Tables<'users'>
type Post = Tables<'posts'>
```

### 4. **何时重新生成**

在以下情况后运行 `npm run gen-types`：
- 创建新表
- 添加/删除列
- 更改列类型
- 修改 RLS 策略
- 添加枚举

### 5. **最佳实践**

- ✓ 将生成的类型提交到 git
- ✓ 在 schema 更改后运行
- ✓ 在所有 Supabase 查询中使用
- ✓ 为常见模式创建辅助类型
- ✓ 将类型文件保存在 `lib/` 或 `types/` 目录
- ✗ 不要手动编辑生成的文件
- ✗ 不要使用 `any` 代替生成的类型

### 6. **与 Pre-commit Hook 集成**

```bash
# .husky/pre-commit
#!/bin/sh
npm run gen-types
git add lib/database.types.ts
```

## 故障排除

**问题**：找不到 `supabase` 命令
```bash
npm install -g supabase
```

**问题**：缺少项目 ID
```bash
# 在 Supabase dashboard 中查找你的项目 ID
# 或在 .env 中设置
SUPABASE_PROJECT_ID=your-project-id
```

**问题**：类型未更新
```bash
# 清除缓存并重新生成
rm lib/database.types.ts
npm run gen-types
```

生成并使用 TypeScript 类型，在编译时而非运行时发现数据库相关的错误。
