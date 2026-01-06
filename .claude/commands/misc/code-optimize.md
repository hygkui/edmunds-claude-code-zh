---
description: 分析和优化代码的性能、内存和效率
model: claude-sonnet-4-5
---

优化以下代码以提高性能和效率。

## 待优化代码

$ARGUMENTS

## 独立开发者优化策略

### 1. **首先进行性能分析**
- 识别实际瓶颈
- 不要过早优化
- 优化前后都要测量
- 专注于高影响区域

### 2. **性能优化领域**

**React/Next.js**
- 记忆化（React.memo、useMemo、useCallback）
- 代码分割和懒加载
- 图片优化（next/image）
- 字体优化（next/font）
- 移除不必要的重新渲染
- 长列表虚拟滚动

**数据库查询**
- 为频繁查询的字段添加索引
- 批量查询（减少 N+1 问题）
- 使用 select 限制字段
- 实现分页
- 缓存频繁查询
- 对复杂连接使用数据库视图

**API 调用**
- 实现缓存（SWR、React Query）
- 防抖/节流请求
- 尽可能并行请求
- 请求去重
- 乐观更新

**打包大小**
- Tree-shaking 未使用的代码
- 大型库的动态导入
- 替换重型依赖
- 按路由代码分割
- 懒加载首屏以下内容

**内存**
- 修复内存泄漏（清理 useEffect）
- 避免不必要的对象创建
- 对不变的值使用 const
- 清除 intervals/timeouts
- 移除事件监听器

### 3. **优化清单**

**JavaScript/TypeScript**
- 使用 const/let 而不是 var
- 尽可能避免嵌套循环
- 使用 Map/Set 进行查找
- 最小化 DOM 操作
- 对昂贵操作进行防抖/节流

**React**
- 记忆化频繁渲染的组件
- 将静态值移到组件外
- 在列表中正确使用 keys
- 避免渲染中的内联函数
- 懒加载路由和组件

**Next.js**
- 尽可能使用服务端组件
- 对动态内容实现 ISR
- 使用 next/image 优化图片
- 预取关键路由
- 使用 Suspense 进行流式传输

**数据库**
- 在外键上添加索引
- 使用准备好的语句
- 批量插入/更新
- 实现连接池
- 缓存昂贵的查询

**网络**
- 压缩响应（gzip/brotli）
- 对静态资源使用 CDN
- 实现 HTTP/2
- 设置适当的缓存头
- 最小化负载大小

### 4. **测量工具**

**前端**
- Chrome DevTools 性能标签
- Lighthouse CI
- React DevTools Profiler
- Bundle Analyzer（next/bundle-analyzer）

**后端**
- Node.js profiler
- 数据库查询分析器
- APM 工具（DataDog、New Relic）
- 负载测试（k6、Artillery）

### 5. **常见优化**

**替换低效的数组方法**
```typescript
// 之前: 多次迭代
const result = arr
  .filter(x => x > 0)
  .map(x => x * 2)
  .reduce((sum, x) => sum + x, 0)

// 之后: 单次迭代
const result = arr.reduce((sum, x) => {
  return x > 0 ? sum + (x * 2) : sum
}, 0)
```

**记忆化昂贵计算**
```typescript
const expensiveValue = useMemo(() => {
  return complexCalculation(props.data)
}, [props.data])
```

**长列表虚拟滚动**
```typescript
import { useVirtual } from 'react-virtual'
// 只渲染可见项
```

## 输出格式

1. **分析** - 识别性能瓶颈
2. **优化后的代码** - 改进版本
3. **解释** - 改变的内容和原因
4. **基准测试** - 预期的性能改进
5. **权衡** - 增加的任何复杂度
6. **后续步骤** - 进一步优化机会

专注于提供实际用户价值的实用、可测量的优化。不要为了微优化牺牲可读性。
