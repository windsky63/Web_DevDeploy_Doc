# user 模块

- 基础路由：/api/user
- 子路由 ①：/user_manage
- 子路由 ②：/login_register
- 子路由 ③：/change_info

## ① 用户管理接口

## 1. GET 请求

### 描述

用于获取用户列表数据，支持分页和搜索。

### 参数

| 参数名     | 类型 | 是否必填 | 描述                                                 |
| ---------- | ---- | -------- | ---------------------------------------------------- |
| page       | int  | 是       | 当前页码，从 1 开始                                  |
| search_key | str  | 否       | 搜索关键字类型，可选值：`用户ID`、`用户名`、`手机号` |
| search     | str  | 否       | 搜索关键字内容，与 `search_key` 配合使用             |

### 响应示例

- 成功响应：
  - 状态码：`200`
  - 响应体：
    ```json
    {
      "code": "200",
      "status": true,
      "msg": "请求数据成功",
      "data": [
        {
          "user_id": 1,
          "user_name": "example_user",
          "phone_number": "1234567890",
          "password": "123456",
          "email": "user@example.com",
          "user_avatar": "/media/user_avatar/1_avatar.webp",
          "user_create_time": "2025-01-01T10:00:00Z",
          "recent_login": "2025-01-01T10:00:00Z"
        }
      ],
      "max_page": 10
    }
    ```
- 失败响应：
  - 状态码：`200`
  - 响应体：
    ```json
    {
      "code": "200",
      "status": false,
      "msg": "缺少参数！",
      "data": null,
      "max_page": null
    }
    ```

## 2. POST 请求

### 描述

用于创建新用户。

### 请求体包含参数

| 参数名       | 类型 | 是否必填 | 描述         |
| ------------ | ---- | -------- | ------------ |
| user_name    | str  | 是       | 用户名       |
| password     | str  | 是       | 密码         |
| phone_number | str  | 是       | 手机号       |
| email        | str  | 是       | 邮箱地址     |
| user_avatar  | str  | 否       | 用户头像 URL |

### 响应示例

- 成功响应：
  - 状态码：`200`
  - 响应体:
    ```json
    {
      "code": "200",
      "status": true,
      "msg": "添加数据成功",
      "data": {
        "user_id": 1,
        "user_name": "example_user",
        "phone_number": "1234567890",
        "password": "123456",
        "email": "user@example.com",
        "user_avatar": "/media/user_avatar/1_avatar.webp",
        "user_create_time": "2025-01-01T10:00:00Z",
        "recent_login": "2025-01-01T10:00:00Z"
      }
    }
    ```
- 失败响应：
  - 状态码：`200`
  - 响应体：
    ```json
    {
      "code": "200",
      "status": false,
      "msg": "未知错误",
      "data": null
    }
    ```

## 3. PUT 请求

### 描述

用于修改指定用户的信息。

### 请求体包含参数

| 参数名   | 类型 | 是否必填 | 描述                                                          |
| -------- | ---- | -------- | ------------------------------------------------------------- |
| user_id  | int  | 是       | 要修改的用户 ID                                               |
| 其他字段 | 任意 | 否       | 要更新的用户字段及对应值（如 `user_name`、`phone_number` 等） |

### 响应示例

- 成功响应：
  - 状态码：`200`
  - 响应体:
    ```json
    {
      "code": "200",
      "status": true,
      "msg": "修改数据成功"
    }
    ```
- 失败响应：
  - 状态码：`200`
  - 响应体：
    ```json
    {
      "code": "200",
      "status": false,
      "msg": "未知错误"
    }
    ```

## 4. DELETE 请求

### 描述

用于删除指定用户。

### 参数

| 参数名  | 类型 | 是否必填 | 描述            |
| ------- | ---- | -------- | --------------- |
| user_id | int  | 是       | 要删除的用户 ID |

### 响应示例

- 成功响应：
  - 状态码：`200`
  - 响应体:
    ```json
    {
      "code": "200",
      "status": true,
      "msg": "删除数据成功"
    }
    ```
- 失败响应：
  - 状态码：`200`
  - 响应体：
    ```json
    {
      "code": "200",
      "status": false,
      "msg": "未知错误"
    }
    ```

### 注意事项

- Token 验证：所有请求均需在 `Authorization` 头中携带有效的 Token，否则返回 `用户未登录或无权限！`。
- 权限验证：只有具备 `access_id=1` 即 `用户管理` 权限的用户才能访问该 API。
- 分页：`GET` 请求默认每页返回 50 条数据，最大页码根据总数据量动态计算。

## ② 登录与注册接口

## 1. GET 请求

### 描述

通过手机号和密码登录，或者使用 Cookies 登录（如果 Cookies 存在且未过期）。

### 参数

| 参数名       | 类型 | 是否必填 | 描述                                                    |
| ------------ | ---- | -------- | ------------------------------------------------------- |
| phone_number | str  | 是       | 用户手机号                                              |
| password     | str  | 是       | 用户密码                                                |
| rem_flag     | int  | 否       | 是否记住登录状态（`true` 表示记住，默认不传表示不记住） |

### 响应示例

- 成功响应：
  - 状态码：`200`
  - 响应体：
    ```json
    {
      "code": "200",
      "status": true,
      "msg": "登录成功",
      "data": {
        "user_id": 1,
        "user_name": "example_user",
        "phone_number": "1234567890",
        "email": "user@example.com",
        "user_avatar": "/media/user_avatar/1_avatar.webp",
        "user_create_time": "2025-01-01T10:00:00Z",
        "recent_login": "2025-01-01T10:00:00Z",
        "token": "abcdef123456"
      }
    }
    ```
- 失败响应：
  - 状态码：`200`
  - 响应体：
    ```json
    {
      "code": "200",
      "status": false,
      "msg": "用户未注册"
    }
    ```

### Cookies 处理

- 如果 `rem_flag=true`：
  - 服务端会设置一个有效期为 7 天的 `cookies` Cookie，包含加密后的用户信息。

## 2. POST 请求

### 描述

通过手机号和密码注册新用户，并自动赋予普通角色。

### 请求体包含参数

| 参数名       | 类型 | 是否必填 | 描述           |
| ------------ | ---- | -------- | -------------- |
| phone_number | str  | 是       | 用户注册手机号 |
| password     | str  | 是       | 用户注册密码   |

### 响应示例

- 成功响应：
  - 状态码：`200`
  - 响应体：
    ```json
    {
      "code": "200",
      "status": true,
      "msg": "注册成功"
    }
    ```
- 失败响应：
  - 状态码：`200`
  - 响应体：
    ```json
    {
      "code": "200",
      "status": false,
      "msg": "用户已注册"
    }
    ```

## ③ 用户信息修改接口

## 1. PUT 请求

### 描述

用户可以通过该接口修改自己的信息，包括邮箱和用户名。

### 请求体包含参数

请求头
参数名 类型 是否必填 描述
Authorization str 是 用户的 Token，用于验证身份

| 参数名    | 类型 | 是否必填 | 描述             |
| --------- | ---- | -------- | ---------------- |
| user_id   | int  | 是       | 用户的唯一标识   |
| email     | str  | 是       | 用户的新邮箱地址 |
| user_name | str  | 是       | 用户的新用户名   |

### 响应示例

- 成功响应：
  - 状态码：`200`
  - 响应体：
    ```json
    {
      "code": "200",
      "status": true,
      "msg": "修改用户信息成功",
      "data": {
        "email": "new_email@example.com",
        "user_name": "new_username"
      }
    }
    ```
- 失败响应：
  - 状态码：`200`
  - 响应体：
    ```json
    {
      "code": "200",
      "status": false,
      "msg": "用户未登录或无权限！"
    }
    ```

### 注意事项

请求头中必须包含有效的 Authorization Token，用于验证用户身份。
如果 Token 无效或与当前登录用户不一致，将返回 用户未登录或无权限！ 的错误信息。
