# upload 模块

- 基础路由：/api/upload
- 子路由 ①：/user_avatar
- 子路由 ②：/dataset

## ① 用户头像上传接口

## 1. POST 请求

### 描述

上传用户头像，将头像以 Base64 编码格式存储到服务器，并更新用户头像路径到数据库。

### 请求体包含参数

| 参数名     | 类型   | 是否必填 | 描述                     |
| ---------- | ------ | -------- | ------------------------ |
| user_id    | int    | 是       | 用户 ID                  |
| img_base64 | string | 是       | 头像的 Base64 编码字符串 |

### 响应示例

- 成功响应：
  - 状态码：`200`
  - 响应体:
    ```json
    {
      "code": "200",
      "status": true,
      "msg": "头像上传成功"
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

## ② 数据集上传接口

## 1. POST 请求

### 描述

上传一个数据集文件和封面图片，并将相关信息存储到数据库。

### 请求体包含参数

| 参数名     | 类型 | 是否必填 | 描述                                            |
| ---------- | ---- | -------- | ----------------------------------------------- |
| name       | str  | 是       | 数据集名称                                      |
| info       | str  | 否       | 数据集描述，最大长度为 200 字符。               |
| open       | str  | 是       | 数据集是否公开 (true/false)                     |
| file       | file | 是       | 数据集文件 (CSV 格式)，文件大小不能超过 100MB。 |
| cover_file | str  | 否       | 数据集封面图片，文件大小不能超过 2MB。          |

### 响应示例

- 成功响应：

  - 状态码：`200`
  - 响应体：

    ```json
    {
      "code": "200",
      "status": true,
      "msg": "数据集上传成功",
      "data": {
        "dataset_id": 1,
        "dataset_name": "Example Dataset",
        "dataset_info": "This is an example dataset",
        "dataset_size": "12.34MB",
        "download_num": 0,
        "dataset_address": "/media/datasets/1.csv",
        "dataset_cover_address": "/media/datasets_cover/1_cover.webp",
        "upload_time": "2025-01-01T12:00:00Z",
        "dataset_type": 1,
        "upload_user_id": 1
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
      "msg": "未知错误！数据集上传失败",
      "data": null
    }
    ```

## 注意事项

以上接口 均需要 HTTP_AUTHORIZATION 请求头，用于验证用户身份和权限。

- 头像文件以 user_id_avatar.webp 格式存储到 media/user_avatar/ 目录。
- 数据集文件以 dataset_id.csv 格式存储到 media/datasets/ 目录。
- 数据集封面图片以 dataset_id_cover.webp 格式存储到 media/datasets_cover/ 目录。
