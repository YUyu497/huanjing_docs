# UID功能说明

## 概述

UID（User ID）是一个纯数字的用户唯一标识符，用于进一步区分用户。与现有的字符串ID不同，UID是纯数字组合，便于用户间识别和记忆。

## 功能特点

- **8位数字格式**：UID由8位纯数字组成，如：10000001, 10000002, 10000003...
- **唯一性**：每个用户拥有唯一的UID，不会重复
- **自动生成**：注册时自动分配，用户无法修改
- **递增分配**：从10000000开始，按注册顺序递增分配
- **黑名单机制**：避免分配特殊数字组合（如重复数字、连续数字等）
- **公开显示**：UID可以公开显示，用于用户间识别

## 数据库结构

### users表新增字段

```sql
-- 添加uid字段（8位数）
ALTER TABLE `users` ADD COLUMN `uid` int(11) NOT NULL COMMENT '用户唯一数字ID（8位数）' AFTER `id`;
ALTER TABLE `users` ADD UNIQUE KEY `unique_uid` (`uid`);
ALTER TABLE `users` ADD KEY `idx_uid` (`uid`);

-- 创建uid黑名单表
CREATE TABLE `uid_blacklist` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `uid` int(11) NOT NULL COMMENT '被禁止的UID',
  `reason` varchar(255) DEFAULT NULL COMMENT '禁止原因',
  `created_at` timestamp NULL DEFAULT CURRENT_TIMESTAMP,
  PRIMARY KEY (`id`),
  UNIQUE KEY `unique_blacklist_uid` (`uid`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci COMMENT='UID黑名单表';
```

## API接口

### 1. 根据UID获取用户信息

**接口地址：** `GET /api/auth/user/:uid`

**请求参数：**

- `uid` (路径参数): 用户UID，必须是8位纯数字

**响应示例：**

```json
{
  "user": {
    "uid": 10000001,
    "username": "testuser",
    "nickname": "测试用户",
    "avatar": "avatar_url",
    "bio": "个人简介",
    "signature": "个人签名",
    "created_at": "2025-01-27T10:00:00.000Z"
  }
}
```

**错误响应：**

```json
{
  "error": "用户不存在",
  "message": "未找到该UID对应的用户"
}
```

### 2. 用户注册/登录响应

所有用户相关的API响应现在都包含uid字段：

```json
{
  "user": {
    "id": "user_string_id",
    "uid": 10000001,
    "username": "testuser",
    "email": "test@example.com",
    "role": 4,
    // ... 其他字段
  },
  "token": "jwt_token"
}
```

### 3. UID黑名单管理API（管理员专用）

#### 3.1 获取黑名单列表

**接口地址：** `GET /api/admin/uid-blacklist`

**请求参数：**

- `page` (查询参数): 页码，默认1
- `limit` (查询参数): 每页数量，默认50

**响应示例：**

```json
{
  "success": true,
  "data": {
    "blacklist": [
      {
        "id": 1,
        "uid": 11111111,
        "reason": "重复数字组合",
        "created_at": "2025-01-27T10:00:00.000Z"
      }
    ],
    "pagination": {
      "page": 1,
      "limit": 50,
      "total": 1,
      "pages": 1
    }
  }
}
```

#### 3.2 添加UID到黑名单

**接口地址：** `POST /api/admin/uid-blacklist`

**请求体：**

```json
{
  "uid": 12345678,
  "reason": "连续数字组合"
}
```

#### 3.3 从黑名单移除UID

**接口地址：** `DELETE /api/admin/uid-blacklist/:uid`

#### 3.4 检查UID是否在黑名单

**接口地址：** `GET /api/admin/uid-blacklist/check/:uid`

#### 3.5 批量添加UID到黑名单

**接口地址：** `POST /api/admin/uid-blacklist/batch`

**请求体：**

```json
{
  "uids": [11111111, 22222222, 33333333],
  "reason": "批量添加"
}
```

## 前端功能

### 1. 用户资料页面

在用户个人资料页面显示UID：

- 位置：基本信息部分，用户名上方
- 显示格式：`用户ID: 10000001`
- 说明：您的唯一数字ID，用于其他用户识别您

### 2. 用户仪表板

在用户仪表板头部显示UID：

- 位置：用户详细信息中
- 显示格式：`UID: 10000001`

### 3. 用户查找功能

新增用户查找功能：

- 位置：用户控制台 → 用户查找标签页
- 功能：通过输入UID查找其他用户信息
- 支持：显示用户基本信息、头像、个人简介等公开信息

## 使用方法

### 1. 数据库迁移

首先执行数据库迁移脚本：

```bash
# 在MySQL中执行
mysql -u username -p database_name < backend/scripts/add-uid-field.sql
```

### 2. 为现有用户生成UID

迁移脚本会自动为现有用户生成UID，从100001开始递增。

### 3. 测试功能

运行测试脚本验证功能：

```bash
cd backend
node scripts/test-uid-functionality.js
```

## 黑名单机制

### 黑名单规则

系统会自动避免分配以下类型的UID：

1. **重复数字组合**：如 11111111, 22222222, 88888888 等
2. **连续数字组合**：如 12345678, 87654321 等
3. **特殊数字组合**：如 12345679, 98765432 等
4. **系统保留UID**：如 10000000（起始UID）, 99999999（最大UID）等

### 黑名单管理

- **自动添加**：系统预置了常见的黑名单UID
- **手动管理**：管理员可以通过API添加或移除黑名单UID
- **实时检查**：生成UID时会实时检查黑名单，确保不会分配被禁止的UID

## 技术实现

### 后端实现

1. **User模型更新**
   - 添加uid字段到构造函数
   - 实现`generateUid()`方法生成唯一8位UID，避开黑名单
   - 实现`findByUid()`方法根据UID查找用户
   - 实现黑名单相关方法：`isUidBlacklisted()`, `addToBlacklist()`, `removeFromBlacklist()`
   - 更新`create()`方法在创建用户时自动生成UID

2. **认证系统更新**
   - JWT Token中包含uid字段
   - 所有用户相关API响应包含uid

3. **新增API接口**
   - `GET /api/auth/user/:uid` - 根据UID获取用户公开信息
   - `GET /api/admin/uid-blacklist` - 获取UID黑名单列表（管理员）
   - `POST /api/admin/uid-blacklist` - 添加UID到黑名单（管理员）
   - `DELETE /api/admin/uid-blacklist/:uid` - 从黑名单移除UID（管理员）
   - `GET /api/admin/uid-blacklist/check/:uid` - 检查UID是否在黑名单（管理员）
   - `POST /api/admin/uid-blacklist/batch` - 批量添加UID到黑名单（管理员）

### 前端实现

1. **用户资料组件**
   - 显示用户UID
   - 不可编辑的UID字段

2. **用户仪表板**
   - 在头部显示UID信息

3. **用户查找组件**
   - 输入8位UID查找用户
   - 显示用户公开信息
   - 错误处理和验证
   - 支持8位数字格式验证

## 安全考虑

1. **公开信息限制**：根据UID获取用户信息时，只返回公开信息，不包含敏感数据如邮箱、密码等
2. **输入验证**：严格验证UID格式，只允许8位纯数字
3. **权限控制**：用户查找功能不需要登录，但返回的信息有限

## 注意事项

1. **UID不可修改**：一旦分配，UID不可更改
2. **递增分配**：UID按注册顺序递增，便于管理
3. **黑名单保护**：系统会自动避开黑名单中的特殊数字组合
4. **并发安全**：生成UID时考虑了并发情况，确保唯一性
5. **现有用户**：迁移时会为现有用户自动分配UID

## 未来扩展

1. **UID范围管理**：可以为不同用户类型分配不同的UID范围
2. **UID预留**：可以为特殊用户预留特定的UID
3. **UID回收**：删除用户时可以考虑UID回收机制
4. **UID统计**：添加UID使用统计功能

## 故障排除

### 常见问题

1. **UID字段不存在**
   - 解决：执行数据库迁移脚本

2. **UID重复**
   - 解决：检查数据库约束，确保unique_uid索引存在

3. **前端显示问题**
   - 解决：检查用户数据是否包含uid字段

4. **API调用失败**
   - 解决：检查后端服务是否正常运行，API路由是否正确

### 调试命令

```bash
# 检查数据库表结构
DESCRIBE users;

# 检查UID索引
SHOW INDEX FROM users WHERE Key_name = 'unique_uid';

# 查看用户UID分布
SELECT uid, username, created_at FROM users ORDER BY uid LIMIT 10;
```
