# POST /delete

删除指定主键值的数据记录, 请求成功返回`null`；请求失败返回错误对象。 [查看异常规范](../../api/protocol/http.md#4-异常规范)。

默认绑定数据模型的 [Delete](../../model/process/Delete.md) 处理器。

## 1. 接口文档

| 请求 | 数值                                   |
| ---- | -------------------------------------- |
| 方法 | `POST`                                 |
| 路由 | `/api/xiang/table/表格名称/delete/:id` |

### 1.1 Request 请求

#### 路由参数

| 参数 | 说明           | 示例 |
| ---- | -------------- | ---- |
| id   | 数据记录主键值 | `1`  |

### 1.2 Response 响应

| 响应           | 数值               |
| -------------- | ------------------ |
| `Status Code`  | `200`              |
| `Content-Type` | `application/json` |
| `Body`         | `null`             |

## 2. 请求示例

### 2.1 Request

```bash
POST /api/table/user/delete/1
```

| 路由参数 | 数值 |
| -------- | ---- |
| id       | `1`  |

### 2.2 Response

```json
null
```
