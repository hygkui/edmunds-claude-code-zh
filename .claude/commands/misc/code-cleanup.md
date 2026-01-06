---
description: 重构和清理代码，遵循最佳实践
model: claude-sonnet-4-5
---

清理和重构以下代码以提高可读性、可维护性，并遵循最佳实践。

## 待清理代码

$ARGUMENTS

## 独立开发者清理清单

### 1. **需要修复的代码异味**

**命名**
- 描述性的变量/函数名称
- 一致的命名约定（camelCase、PascalCase）
- 避免使用缩写，除非显而易见
- 布尔值名称以 is/has/can 开头

**函数**
- 每个函数单一职责
- 保持函数简短（<50 行）
- 减少参数数量（最多 3-4 个）
- 提取复杂逻辑
- 尽可能避免副作用

**DRY（不要重复自己）**
- 提取重复代码到工具函数
- 创建可重用组件
- 使用 TypeScript 泛型实现类型复用
- 集中管理常量/配置

**复杂度**
- 减少嵌套的 if 语句
- 用函数替换复杂条件
- 使用早期返回
- 简化布尔逻辑

**TypeScript**
- 移除 `any` 类型
- 添加适当的类型注解
- 使用接口定义对象结构
- 利用工具类型（Pick、Omit、Partial）

### 2. **应用的现代模式**

**JavaScript/TypeScript**
```typescript
// 使用可选链
const value = obj?.prop?.nested

// 使用空值合并
const result = value ?? defaultValue

// 使用解构
const { name, email } = user

// 使用模板字符串
const message = `Hello, ${name}!`

// 使用数组方法
const filtered = arr.filter(x => x.active)
```

**React**
```typescript
// 提取自定义 hooks
const useUserData = () => {
  // 逻辑代码
}

// 使用适当的 TypeScript 类型
interface Props {
  user: User
  onUpdate: (user: User) => void
}

// 通过组合避免 prop drilling
<Provider value={data}>
  <Component />
</Provider>
```

### 3. **重构技术**

**提取函数**
```typescript
// 之前
const process = () => {
  // 50 行代码
}

// 之后
const validate = () => { /* ... */ }
const transform = () => { /* ... */ }
const save = () => { /* ... */ }

const process = () => {
  validate()
  const data = transform()
  save(data)
}
```

**用多态替换条件**
```typescript
// 之前
if (type === 'A') return processA()
if (type === 'B') return processB()

// 之后
const processors = {
  A: processA,
  B: processB
}
return processors[type]()
```

**引入参数对象**
```typescript
// 之前
function create(name, email, age, address)

// 之后
interface UserData {
  name: string
  email: string
  age: number
  address: string
}
function create(userData: UserData)
```

### 4. **常见清理任务**

**移除死代码**
- 未使用的导入
- 不可达的代码
- 被注释的代码
- 未使用的变量

**改进错误处理**
```typescript
// 之前
try { doSomething() } catch (e) { console.log(e) }

// 之后
try {
  doSomething()
} catch (error) {
  if (error instanceof ValidationError) {
    // 处理验证错误
  } else {
    logger.error('意外错误', { error })
    throw error
  }
}
```

**一致的格式化**
- 正确的缩进
- 一致的引号
- 行长度（<100 字符）
- 组织良好的导入

**更好的注释**
- 移除显而易见的注释
- 添加"为什么"，而不是"是什么"
- 记录复杂逻辑
- 更新过时的注释

### 5. **Next.js/React 特定优化**

**服务端 vs 客户端组件**
```typescript
// 将状态移至客户端组件
'use client'
function Interactive() {
  const [state, setState] = useState()
}

// 将数据获取保留在服务端组件
async function Page() {
  const data = await fetchData()
}
```

**正确的数据获取**
```typescript
// 客户端使用 SWR/React Query
const { data } = useSWR('/api/user')

// 服务端组件直接使用 fetch
const data = await fetch('/api/user').then(r => r.json())
```

## 输出格式

1. **发现的问题** - 代码异味和问题列表
2. **清理后的代码** - 重构后的版本
3. **说明** - 改变的内容和原因
4. **前后对比** - 有帮助时并排展示
5. **进一步改进** - 可选的增强建议

专注于使代码更易维护的实用改进，避免过度工程化。在整洁代码和实用性之间保持平衡。
