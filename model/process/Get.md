# Get

按条件查询数据记录, 返回符合条件的结果集

## `Get` 按条件查询, 不分页

### 处理器

`models.模型名称.Get`

### 参数表

| 参数    | 类型              | 说明     | 示例                                                                 |
| ------- | ----------------- | -------- | -------------------------------------------------------------------- |
| args[0] | Object QueryParam | 查询条件 | `{"wheres":[{"column":"name", "value":"张三"}],"withs":{"manu":{}}}` |

### 返回值

`Array<Object Row>` 数据记录集合

返回符合条件的的数据记录（Key-Value 结构 Object)集合, JSON 类型字段自动解析, AES 字段自动解密。 关联模型作为一个独立字段，字段名称为关联关系名称； hasOne 关联为数据记录 Object , hasMany 关联为数据记录数组 Array\<Object\>。

## 示例

### 数据模型

| 模型              | 模型定义                                 |
| ----------------- | ---------------------------------------- |
| user `主`         | [模型描述文件](../examples/user.json)    |
| manu `hasOne`     | [模型描述文件](../examples/manu.json)    |
| address `hasMany` | [模型描述文件](../examples/address.json) |

### 处理器

```json
models.user.Get
```

### 参数表

```json
[
  {
    "select": ["id", "name", "mobile", "status"],
    "withs": { "manu": {}, "mother": {}, "addresses": {} },
    "wheres": [{ "column": "status", "value": "enabled" }],
    "orders": [{ "column": "id", "option": "desc" }],
    "limit": 2
  }
]
```

### 返回值

```json
[
  {
    "addresses": [
      {
        "city": "威海市",
        "created_at": "2021-09-15T08:34:20+08:00",
        "deleted_at": null,
        "id": 4,
        "location": "威海市6号楼6单元6层1056室",
        "province": "山东省",
        "status": "enabled",
        "updated_at": null,
        "user_id": 3
      }
    ],
    "id": 3,
    "manu": {
      "contact_mobile": null,
      "contact_name": null,
      "created_at": "2021-09-15T08:34:14+08:00",
      "deleted_at": null,
      "desc": null,
      "id": 2,
      "link": null,
      "logo": null,
      "name": "象传高新（北京）数字科技有限公司",
      "rank": 9999999,
      "short_name": "象传高新",
      "status": "enabled",
      "summary": null,
      "type": "服务商",
      "updated_at": null
    },
    "mobile": "13900003333",
    "mother": {
      "extra": null,
      "friends": {
        "friend_id": null,
        "status": null,
        "type": null
      },
      "id": null,
      "name": null,
      "secret": null,
      "status": null,
      "type": null
    },
    "name": "用户"
  },
  {
    "addresses": [
      {
        "city": "海淀区",
        "created_at": "2021-09-15T08:34:20+08:00",
        "deleted_at": null,
        "id": 3,
        "location": "华严北里7号楼7单元7层2048室",
        "province": "北京市",
        "status": "enabled",
        "updated_at": null,
        "user_id": 2
      }
    ],
    "id": 2,
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
    "mobile": "13900002222",
    "mother": {
      "extra": null,
      "friends": {
        "friend_id": null,
        "status": null,
        "type": null
      },
      "id": null,
      "name": null,
      "secret": null,
      "status": null,
      "type": null
    },
    "name": "员工"
  }
]
```

## 外部引用

### 在业务逻辑(`Flow`) 中调用:

```json
{
  "nodes": [
    {
      "name": "users",
      "process": "models.user.Get",
      "args": [
        {
          "select": ["id", "name", "mobile", "status"],
          "withs": { "manu": {}, "mother": {}, "addresses": {} },
          "wheres": [{ "column": "status", "value": "enabled" }],
          "orders": [{ "column": "id", "option": "desc" }],
          "limit": 2
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
      "path": "/search",
      "method": "GET",
      "process": "models.user.Get",
      "in": [":params"],
      "out": {
        "status": 200,
        "type": "application/json"
      }
    }
  ]
}
```

```bash
GET /api/user/search?withs=manu,mother,addresses&where.status.eq=enabled&order=id.desc&select=id,name,mobile,status&limit=2
```
