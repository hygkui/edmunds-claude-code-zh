---
description: 使用 TypeScript 和现代最佳实践创建新的 React 组件
model: claude-sonnet-4-5
---

按照 2025 年最佳实践生成新的 React 组件。

## 组件规格

$ARGUMENTS

## 现代 React + TypeScript 标准

### 1. **仅使用函数组件**
- 使用函数组件（不使用类组件）
- React 19 模式
- 适当使用 Server Components（Next.js）

### 2. **TypeScript 最佳实践**
- 严格类型检查（`strict: true`）
- Props 使用 Interface
- 正确使用 TypeScript 工具类型（ComponentProps、ReactNode 等）
- 禁止使用 `any` 类型
- 复杂组件使用显式返回类型

### 3. **组件模式**

**Client Components**（交互式，使用 hooks）
```typescript
'use client'
import { useState } from 'react'

interface Props {
  // 类型化的 props
}

export function Component({ }: Props) {
  // 实现
}
```

**Server Components**（Next.js App Router 默认）
```typescript
interface Props {
  // 类型化的 props
}

export async function Component({ }: Props) {
  // 可以直接获取数据
}
```

### 4. **状态管理**
- 本地状态使用 `useState`
- 复杂状态使用 `useReducer`
- 全局状态使用 Zustand
- 主题/认证使用 React Context

### 5. **性能优化**
- 使用 `React.lazy()` 进行懒加载
- 代码分割
- 昂贵计算使用 `useMemo()`
- 回调函数使用 `useCallback()`

### 6. **样式方案**（根据项目选择）
- **Tailwind CSS** - Utility-first（推荐）
- **CSS Modules** - 作用域样式
- **Styled Components** - CSS-in-JS

## 生成内容

1. **组件文件** - 带有 TypeScript 的主组件
2. **Props 接口** - 完整类型化的 props
3. **样式** - Tailwind 类或 CSS 模块
4. **使用示例** - 如何导入和使用
5. **Storybook Story**（可选）- 组件文档

## 代码质量标准

**结构**
- 基于功能的文件夹组织
- 相关文件同位
- Barrel exports（index.ts）
- 清晰的文件命名规范

**TypeScript**
- 通过 interface 显式声明 props 类型
- 适当使用泛型
- 工具类型（Pick、Omit、Partial）
- 使用可辨识联合处理变体

**Props**
- 必需 vs 可选 props
- 适当设置默认值
- 在函数签名中解构
- 谨慎使用 props 展开

**可访问性**
- 语义化 HTML
- 必要时使用 ARIA 标签
- 键盘导航
- 屏幕阅读器友好

**最佳实践**
- 单一职责原则
- 组合优于继承
- 将复杂逻辑提取到 hooks
- 保持组件小型（< 200 行）

## 可考虑的组件类型

**展示组件**
- 纯 UI 渲染
- 无业务逻辑
- 通过 props 接收数据
- 易于测试

**容器组件**
- 数据获取
- 业务逻辑
- 状态管理
- 将数据传递给展示组件

**复合组件**
- 协同工作的相关组件
- 共享上下文
- 灵活的 API
- 示例：`<Select><Select.Trigger/><Select.Content/></Select>`

## 可使用的 React 19 特性

- **use()** API 用于读取 promise/context
- **useActionState()** 用于表单状态
- **useFormStatus()** 用于表单待定状态
- **useOptimistic()** 用于乐观 UI 更新
- **Server Actions** 用于数据变更

按照 Next.js 15 和 React 19 模式生成生产就绪、可访问且高性能的 React 组件。
