# GET /find

按主键值查询单条数据, 请求成功返回对应主键的数据记录；请求失败返回错误对象。 [查看异常规范](../../api/protocol/http.md#4-异常规范)。

默认绑定数据模型的 [Find](../../model/process/Find.md) 处理器。

## 1. 接口文档

| 请求 | 数值                                 |
| ---- | ------------------------------------ |
| 方法 | `GET`                                |
| 路由 | `/api/xiang/table/表格名称/find/:id` |

### 1.1 Request 请求

#### 请求参数

| 路由参数 | 说明           | 示例 |
| -------- | -------------- | ---- |
| id       | 数据记录主键值 | `1`  |

### 1.2 Response 响应

| 响应           | 数值               |
| -------------- | ------------------ |
| `Status Code`  | `200`              |
| `Content-Type` | `application/json` |
| `Body`         | `Object Row`       |

#### `Object Row` 数据结构

`[key:String]Any`

## 2. 请求示例

### 2.1 Request

```bash
GET /api/table/user/find/1
```

| 路由参数 | 数值 |
| -------- | ---- |
| id       | `1`  |

### 2.2 Response

```json
{
  "addresses": [
    {
      "city": "丰台区",
      "created_at": "2021-09-15T08:34:19+08:00",
      "deleted_at": null,
      "id": 2,
      "location": "北京国家数字出版基地A103",
      "province": "北京市",
      "status": "enabled",
      "updated_at": null,
      "user_id": 1
    }
  ],
  "balance": 0,
  "created_at": "2021-09-15T08:34:06+08:00",
  "deleted_at": null,
  "extra": {
    "sex": "男"
  },
  "id": 1,
  "idcard": "230624198301170015",
  "key": "FB3fxCeQ",
  "manu": {
    "contact_mobile": null,
    "contact_name": null,
    "created_at": "2021-09-15T08:34:14+08:00",
    "deleted_at": null,
    "desc": null,
    "id": 1,
    "link": null,
    "logo": null,
    "name": "北京云道天成科技有限公司",
    "rank": 9999999,
    "short_name": "云道天成",
    "status": "enabled",
    "summary": null,
    "type": "服务商",
    "updated_at": null
  },
  "mobile": "13900001111",
  "mother": {
    "extra": {
      "sex": "女"
    },
    "friends": {
      "friend_id": 2,
      "status": "enabled",
      "type": "monther"
    },
    "id": 2,
    "name": "员工",
    "secret": "wBeYjL7FjbcvpAdBrxtDFfjydsoPKhRN",
    "status": "enabled",
    "type": "staff"
  },
  "name": "管理员",
  "password": "$2a$04$nDBXydTJ93gmZo5UVj./PeGJGweSfEbXyEvMZjJ2Pf3THIpvAkhhO",
  "resume": null,
  "secret": "XMTdNRVigbgUiAPdiJCfaWgWcz2PaQXw",
  "status": "enabled",
  "type": "admin",
  "updated_at": "2021-09-15T08:34:24+08:00"
}
```
