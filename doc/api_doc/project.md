# project 模块

## ① 项目管理接口（不完善）

## 1. GET 请求

### 描述

获取所有项目数据。

### 响应示例

- 成功响应：
  - 状态码：`200`
  - 响应体：
    ```json
    {
      "code": "200",
      "data": [
        {
          "project_id": 1,
          "project_name": "Project A",
          "project_address": "/media/project_document/projectA",
          "project_create_time": "2025-01-01T10:00:00Z",
          "project_update_time": "2025-01-01T10:00:00Z",
          "create_user_id": 1
        },
        {
          "project_id": 2,
          "project_name": "Project B",
          "project_address": "/media/project_document/projectB",
          "project_create_time": "2025-01-01T10:00:00Z",
          "project_update_time": "2025-01-01T10:00:00Z",
          "create_user_id": 1
        }
      ],
      "msg": "请求数据失败"
    }
    ```
- 失败响应：
  - 状态码：`200`
  - 响应体：
    ```json
    {
      "code": "200",
      "msg": "请求数据失败",
      "data": null
    }
    ```

## ② 项目文档修改接口

## 1. PUT 请求

### 描述

用于修改项目文档。

### 参数

| 参数名     | 类型 | 是否必填 | 描述                   |
| ---------- | ---- | -------- | ---------------------- |
| project_id | int  | 是       | 指定要修改的项目 ID    |
| content    | str  | 是       | 新的 Markdown 文档内容 |

### 响应示例

- 成功响应：
  - 状态码：`200`
  - 响应体：
    ```json
    {
      "code": "200",
      "status": true,
      "msg": "文档修改成功"
    }
    ```
- 失败响应：
  - 状态码：`200`
  - 响应体：
    ```json
    {
      "code": "200",
      "msg": "请求数据失败",
      "data": null
    }
    ```

## ③ 项目文档展示接口

## 1. GET 请求

### 描述

用于获取指定项目的 Markdown 文档内容。

### 参数

| 参数名     | 类型 | 是否必填 | 描述                  |
| ---------- | ---- | -------- | --------------------- |
| project_id | int  | 是       | 指定要查看的项目 ID。 |

### 响应示例

- 成功响应：
  - 状态码：`200`
  - 响应体：
    ```json
    {
      "code": "200",
      "data": "# Project A\n\nThis is the content of Project A's document.",
      "msg": "请求数据成功"
    }
    ```
- 失败响应：
  - 状态码：`200`
  - 响应体：
    ```json
    {
      "code": "200",
      "data": null,
      "msg": "请求数据失败"
    }
    ```

## ④ 项目列表接口

## 1. GET 请求

### 描述

用于获取所有项目的列表。

### 响应示例

- 成功响应：
  - 状态码：`200`
  - 响应体：
    ```json
    {
      "code": "200",
      "data": [
        {
          "project_id": 1,
          "project_name": "Project A",
          "project_address": "/media/project_document/projectA",
          "project_create_time": "2025-01-01T10:00:00Z",
          "project_update_time": "2025-01-01T10:00:00Z",
          "create_user_id": 1
        },
        {
          "project_id": 2,
          "project_name": "Project B",
          "project_address": "/media/project_document/projectB",
          "project_create_time": "2025-01-01T10:00:00Z",
          "project_update_time": "2025-01-01T10:00:00Z",
          "create_user_id": 1
        }
      ],
      "msg": "请求数据成功"
    }
    ```
- 失败响应：
  - 状态码：`200`
  - 响应体：
    ```json
    {
      "code": "200",
      "data": null,
      "msg": "请求数据失败"
    }
    ```
