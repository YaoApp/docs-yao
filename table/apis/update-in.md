# POST /update/in

批量更新一组指定主键值数据记录, 请求成功返回更新行数；请求失败返回错误对象。 [查看异常规范](../../api/protocol/http.md#4-异常规范)。

默认绑定数据模型的 [UpdateWhere](../../model/process/UpdateWhere.md) 处理器，并将请求参数 `ids` 与 where.主键.in 绑定。

## 1. 接口文档

| 请求 | 数值                                  |
| ---- | ------------------------------------- |
| 方法 | `POST`                                |
| 路由 | `/api/xiang/table/表格名称/update/in` |

### 1.1 Request 请求

#### URL Query String

| 请求参数 | 说明                                  | 示例      |
| -------- | ------------------------------------- | --------- |
| ids      | 要删除的数据记录主键值，用 `,` 分割。 | `1,2,3,4` |
| primary  | 主键名称，默认为 `id`                 | `id`      |

#### 请求 Header

| 请求 Header  | 数值               |
| ------------ | ------------------ |
| Content-Type | `application/json` |

#### 请求 Body

`[key:String]Any` 结构的 JSON 格式字符串

### 1.2 Response 响应

| 响应           | 数值               |
| -------------- | ------------------ |
| `Status Code`  | `200`              |
| `Content-Type` | `application/json` |
| `Body`         | `Integer`          |

## 2. 请求示例

### 2.1 Request

```bash
POST /api/table/user/update/where?ids=1,2,3,4
```

#### Header

| 请求 Header  | 数值               |
| ------------ | ------------------ |
| Content-Type | `application/json` |

#### URL Query String

| 参数 | 数值      |
| ---- | --------- |
| ids  | `1,2,3,4` |

#### Body

```json
{
  "balance": 200
}
```

### 2.2 Response

```json
4
```
