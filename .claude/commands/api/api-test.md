---
description: 使用自动测试生成测试 API 端点
model: claude-sonnet-4-5
---

为指定端点生成全面的 API 测试。

## 目标

$ARGUMENTS

## 独立开发者的测试策略

使用现代工具创建实用、可维护的测试：

### 1. **测试方法**
- 验证逻辑的单元测试
- 完整 API 流程的集成测试
- 边缘情况覆盖
- 错误场景测试

### 2. **工具**（根据项目选择）
- **Vitest** - 快速、现代（推荐用于新项目）
- **Jest** - 成熟、广泛使用
- **Supertest** - HTTP 断言
- **MSW** - API 模拟

### 3. **测试覆盖**

**正常路径**
- 有效输入返回预期结果
- 正确的状态码
- 正确的响应结构

**错误路径**
- 无效输入验证
- 身份验证失败
- 速率限制
- 服务器错误
- 缺少必填字段

**边缘情况**
- 空请求
- 格式错误的 JSON
- 大 payload
- 特殊字符
- SQL 注入尝试
- XSS 尝试

### 4. **测试结构**

```typescript
describe('API Endpoint', () => {
  describe('Success Cases', () => {
    it('should handle valid request', () => {})
    it('should return correct status code', () => {})
  })

  describe('Validation', () => {
    it('should reject invalid input', () => {})
    it('should validate required fields', () => {})
  })

  describe('Error Handling', () => {
    it('should handle server errors', () => {})
    it('should return proper error format', () => {})
  })
})
```

### 5. **生成内容**

1. **测试文件** - 包含所有场景的完整测试套件
2. **模拟数据** - 真实的测试 fixtures
3. **辅助函数** - 可重用的测试工具
4. **设置/清理** - 数据库/状态管理
5. **快速测试脚本** - 运行测试的 npm 脚本

## 关键测试原则

- 测试行为，而非实现
- 清晰、描述性的测试名称
- Arrange-Act-Assert 模式
- 独立的测试（无共享状态）
- 快速执行（单元测试 <5s）
- 真实的模拟数据
- 测试错误消息
- 不测试框架内部
- 不模拟你不拥有的内容
- 避免脆弱的测试

## 需要覆盖的其他场景

1. **身份验证/授权**
   - 有效 token
   - 过期 token
   - 缺失 token
   - 无效权限

2. **数据验证**
   - 类型不匹配
   - 超出范围的值
   - SQL/NoSQL 注入
   - XSS payload

3. **速率限制**
   - 在限制内
   - 超过限制
   - 重置行为

4. **性能**
   - 响应时间
   - 大数据集处理
   - 并发请求

生成我可以使用 `npm test` 立即运行的生产就绪测试。
