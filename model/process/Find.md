# Find

按主键查询单条记录，返回数据记录

## `find` 查询单条记录

### 处理器

`models.模型名称.Find`

### 参数表

| 参数    | 类型              | 说明                      | 示例                                                 |
| ------- | ----------------- | ------------------------- | ---------------------------------------------------- |
| args[0] | Integer \| String | 模型主键                  | `1`                                                  |
| args[1] | Object QueryParam | 查询条件, 仅 `withs` 有效 | `{"withs":{"manu":{}, "mother":{}, "addresses":{}}}` |

### 返回值

`Object Row` 数据记录

返回主键数值等于 `args[0]` 的数据记录（Key-Value 结构 Object), JSON 类型字段自动解析, AES 字段自动解密。 关联模型作为一个独立字段，字段名称为关联关系名称； hasOne 关联为数据记录 Object , hasMany 关联为数据记录数组 Array\<Object\>。

## 示例

### 数据模型

| 模型              | 模型定义                                 |
| ----------------- | ---------------------------------------- |
| user `主`         | [模型描述文件](../examples/user.json)    |
| manu `hasOne`     | [模型描述文件](../examples/manu.json)    |
| address `hasMany` | [模型描述文件](../examples/address.json) |

### 处理器

```json
models.user.Find
```

### 参数表

```json
[
  1,
  {
    "withs": { "manu": {}, "mother": {}, "addresses": {} }
  }
]
```

### 返回值

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

## 外部引用

### 在业务逻辑(`Flow`) 中调用:

```json
{
  "nodes": [
    {
      "name": "user",
      "process": "models.user.Find",
      "args": [
        1,
        {
          "withs": { "manu": {}, "mother": {}, "addresses": {} }
        }
      ],
      "outs": ["{{$out}}"]
    }
  ]
}
```

### 在服务接口(`API`) 中调用:

```json
{
  "paths": [
    {
      "path": "/find/:id",
      "method": "GET",
      "process": "models.user.Find",
      "in": ["$param.id", ":params"],
      "out": {
        "status": 200,
        "type": "application/json"
      }
    }
  ]
}
```

```bash
GET /api/user/find/1?withs=manu,mother,addresses
```
