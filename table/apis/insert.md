# POST /insert

插入多条数据记录，请求成功返回插入行数；请求失败返回错误对象。 [查看异常规范](../../api/protocol/http.md#4-异常规范)。

默认绑定数据模型的 [Insert](../../model/process/Insert.md) 处理器。

## 1. 接口文档

| 请求 | 数值                               |
| ---- | ---------------------------------- |
| 方法 | `POST`                             |
| 路由 | `/api/xiang/table/表格名称/insert` |

### 1.1 Request 请求

#### 请求 Header

| 请求 Header  | 数值               |
| ------------ | ------------------ |
| Content-Type | `application/json` |

#### 请求 Body

JSON 格式字符串

```json
{
  "columns": ["user_id", "province"],
  "values": [
    [4, "北京市"],
    [4, "天津市"]
  ]
}
```

| 字段      | 类型                  | 说明             | 示例                             |
| --------- | --------------------- | ---------------- | -------------------------------- |
| `columns` | Array\<String\>       | 字段列表         | `["user_id", "province"]`        |
| `values`  | Array\<Array\<Any\>\> | 数据记录数值集合 | `[[4, "北京市"], [4, "天津市"]]` |

### 1.2 Response 响应

| 响应           | 数值               |
| -------------- | ------------------ |
| `Status Code`  | `200`              |
| `Content-Type` | `application/json` |
| `Body`         | `Integer`          |

## 2. 请求示例

### 2.1 Request

```bash
POST /api/table/user/save
```

**请求 Header**

| Header       | 数值               |
| ------------ | ------------------ |
| Content-Type | `application/json` |

**请求 Body**

```json
[
  ["user_id", "province", "city", "location"],
  [
    [4, "北京市", "丰台区", "银海星月9号楼9单元9层1024室"],
    [4, "天津市", "塘沽区", "益海星云7号楼3单元1003室"]
  ]
]
```

### 2.2 Response

```json
2
```
