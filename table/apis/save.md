# POST /save

保存单条记录。如数据记录中包含主键字段则更新，不包含主键字段则创建记录；返回创建或更新的记录主键值；请求失败返回错误对象。 [查看异常规范](../../api/protocol/http.md#4-异常规范)。

默认绑定数据模型的 [Save](../../model/process/Save.md) 处理器。

## 1. 接口文档

| 请求 | 数值                             |
| ---- | -------------------------------- |
| 方法 | `POST`                           |
| 路由 | `/api/xiang/table/表格名称/save` |

### 1.1 Request 请求

#### 请求 Header

| 请求 Header  | 数值               |
| ------------ | ------------------ |
| Content-Type | `application/json` |

#### 请求 Body

`[key:String]Any` 结构的 JSON 格式字符串

### 1.2 Response 响应

| 响应           | 数值                |
| -------------- | ------------------- |
| `Status Code`  | `200`               |
| `Content-Type` | `application/json`  |
| `Body`         | `Integer \| String` |

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
{
  "id": 101,
  "name": "用户保存",
  "manu_id": 2,
  "type": "user",
  "idcard": "23082619820207006X",
  "mobile": "13900004444",
  "password": "qV@uT1DI",
  "key": "XZ12MiPp",
  "secret": "wBeYjL7FjbcvpAdBrxtDFfjydsoPKhRN",
  "status": "enabled",
  "extra": { "sex": "女" }
}
```

### 2.2 Response

```json
1024
```
