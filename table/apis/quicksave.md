# POST /quicksave

保存多条记录。如数据记录中包含主键字段则更新，不包含主键字段则创建记录；返回创建或更新的记录主键值；请求失败返回错误对象。 [查看异常规范](../../api/protocol/http.md#4-异常规范)。

默认绑定数据模型的 [EachSaveAfterDelete](../../model/process/EachSaveAfterDelete.md) 处理器。

## 1. 接口文档

| 请求 | 数值                                  |
| ---- | ------------------------------------- |
| 方法 | `POST`                                |
| 路由 | `/api/xiang/table/表格名称/quicksave` |

### 1.1 Request 请求

#### 请求 Header

| 请求 Header  | 数值               |
| ------------ | ------------------ |
| Content-Type | `application/json` |

#### 请求 Body

```json
{
  "delete": [1, 5],
  "data": [{ "name": "张三" }, { "id": 2, "name": "李四" }],
  "query": { "type": "用户", "sort": "$index" }
}
```

### 1.2 Response 响应

| 响应           | 数值               |
| -------------- | ------------------ |
| `Status Code`  | `200`              |
| `Content-Type` | `application/json` |
| `Body`         | `Array<Integer>`   |

## 2. 请求示例

### 2.1 Request

```bash
POST /api/table/user/quicksave
```

**请求 Header**

| Header       | 数值               |
| ------------ | ------------------ |
| Content-Type | `application/json` |

**请求 Body**

```json
{
  "delete": [1, 5],
  "data": [{ "name": "张三" }, { "id": 2, "name": "李四" }],
  "query": { "type": "用户", "sort": "$index" }
}
```

### 2.2 Response

```json
[1, 2]
```
