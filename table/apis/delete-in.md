# POST /delete/in

批量删除一组指定主键值数据记录, 请求成功返回删除行数；请求失败返回错误对象。 [查看异常规范](../../api/protocol/http.md#4-异常规范)。

默认绑定数据模型的 [DeleteWhere](../../model/process/DeleteWhere.md) 处理器, 并将请求参数 `ids` 与 where.主键.in 绑定。

## 1. 接口文档

| 请求 | 数值                                  |
| ---- | ------------------------------------- |
| 方法 | `POST`                                |
| 路由 | `/api/xiang/table/表格名称/delete/in` |

### 1.1 Request 请求

#### URL Query String

| 请求参数 | 说明                                  | 示例      |
| -------- | ------------------------------------- | --------- |
| ids      | 要删除的数据记录主键值，用 `,` 分割。 | `1,2,3,4` |
| primary  | 主键名称，默认为 `id`                 | `id`      |

### 1.2 Response 响应

| 响应           | 数值               |
| -------------- | ------------------ |
| `Status Code`  | `200`              |
| `Content-Type` | `application/json` |
| `Body`         | `Integer`          |

## 2. 请求示例

### 2.1 Request

```bash
POST /api/table/user/delete/in?ids=1,2,3,4
```

| 请求参数 | 数值      |
| -------- | --------- |
| ids      | `1,2,3,4` |

### 2.2 Response

```json
4
```
