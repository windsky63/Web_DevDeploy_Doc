# data_mining 模块

- 基础路由：/api/data_mining
- 子路由 ①：/gen_data
- 子路由 ②：/get_data_list
- 子路由 ③：/get_data
- 子路由 ④：/data_view

## ① 生成数据集接口

## 1. GET 请求

### 描述

生成数据集。

### 参数

| 参数名      | 类型  | 是否必填 | 描述                                           |
| ----------- | ----- | -------- | ---------------------------------------------- |
| key         | str   | 是       | 数据类型（如 `home_price` 或 `customer`）      |
| random_seed | int   | 是       | 随机种子，用于生成数据。                       |
| size        | int   | 是       | 生成数据的样本数量。                           |
| noise_std   | float | 是       | 噪声标准差和均值（仅对 `home_price` 类型有效） |
| noise_mean  | float | 是       | 噪声标准差和均值（仅对 `home_price` 类型有效） |
| noise_level | float | 是       | 噪声级别（仅对 `customer` 类型有效）           |

### 响应示例

- 成功响应：
  - 状态码：`200`
  - 响应体：
    ```json
    {
      "code": "200",
      "status": true,
      "msg": "生成成功",
      "data": {
        "name": "数据集名称",
        "data": [], // 生成的数据集数据
        "meta": {}, // 生成的数据集的一些指标例如平均值等
        "csv_name": "生成数据集的csv文件名",
        "type": "gen"
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

## ② 数据集列表接口

## 1. GET 请求

### 描述

获取服务端存在的公开的数据集列表。

### 参数

| 参数名 | 类型 | 是否必填 | 描述                           |
| ------ | ---- | -------- | ------------------------------ |
| page   | int  | 是       | 分页参数，用于指定要获取的页码 |

### 响应示例

- 成功响应：
  - 状态码：`200`
  - 响应体：
    ```json
    {
      "code": "200",
      "status": true,
      "msg": "生成成功",
      "data": [
        {
          "dataset_id": 1,
          "dataset_name": "数据集名称",
          "dataset_info": "数据集简介",
          "dataset_size": "12.34MB",
          "download_num": 0,
          "dataset_address": "/media/datasets/1.csv",
          "dataset_cover_address": "/media/datasets_cover/1_cover.webp",
          "upload_time": "2025-01-01T10:00:00Z",
          "dataset_type": 1,
          "upload_user": 66
        }
      ],
      "max_page": 1,
      "datasets_num": 0
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
      "data": null,
      "max_page": 0,
      "datasets_num": 0
    }
    ```

## ③ 云端数据集接口

## 1. GET 请求

### 描述

使用云端存储的数据集。

### 参数

| 参数名     | 类型 | 是否必填 | 描述                |
| ---------- | ---- | -------- | ------------------- |
| dataset_id | int  | 是       | 要使用的数据集的 ID |

### 响应示例

- 成功响应：
  - 状态码：`200`
  - 响应体：
    ```json
    {
      "code": "200",
      "status": true,
      "msg": "云端数据集链接成功",
      "data": {
        "name": "数据集名称",
        "data": {
          "dataset_id": 1,
          "dataset_name": "数据集名称",
          "dataset": [], // 数据集数据
          "dataset_type": "cloud"
        }
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

## ④ 数据集可视化图表接口(不完善)

## 1. GET 请求

### 描述

生成 `pyecharts` 图表。

### 参数

| 参数名       | 类型 | 是否必填               | 描述                                             |
| ------------ | ---- | ---------------------- | ------------------------------------------------ |
| chart_type   | int  | 是                     | 图表类型（如 `bar`、`pie`、`line`、`wordcloud`） |
| dataset_id   | int  | 与 csv_name 任选其一   | 数据来源：数据集 ID                              |
| csv_name     | int  | 与 dataset_id 任选其一 | 数据来源：CSV 文件名                             |
| dataset_type | int  | 是                     | 数据类型（`cloud` 、`gen`、`upload`）            |
| feature_name | int  | 是                     | 特征名称（用于指定图表的数据列）                 |
| top_n        | int  | 否                     | 词云图中显示前 N 个词                            |

### 响应示例

- 成功响应：
  - 状态码：`200`
  - 响应体：
    ```json
    {
      "code": "200",
      "status": true,
      "msg": "生成图表成功",
      "data": "..." //以字符串形式存储的html图表
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
