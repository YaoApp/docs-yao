# GET /search

按条件查询数据记录, 请求成功返回符合查询条件带有分页信息的数据对象；请求失败返回错误对象。 [查看异常规范](../../api/protocol/http.md#4-异常规范)。

默认绑定数据模型的 [Paginate](../../model/process/Paginate.md) 处理器。

## 1. 接口文档

| 请求 | 数值                               |
| ---- | ---------------------------------- |
| 方法 | `GET`                              |
| 路由 | `/api/xiang/table/表格名称/search` |

### 1.1 Request 请求

#### 请求参数

| URL Query String                          | 说明                      | 示例                                                        |
| ----------------------------------------- | ------------------------- | ----------------------------------------------------------- |
| 查询方法.字段名称.匹配关系                | 字段匹配关系查询          | `where.status.eq=enabled`, `orwhere.status.eq=disabled`     |
| 查询方法.关联模型名称.字段名称.匹配关系   | 关联模型字段匹配关系查询  | `where.mother.friends.status.eq=enabled`,                   |
| group.分组名称.查询方法.字段名称.匹配关系 | 字段匹配关系分组查询      | `group.types.where.type.eq=1&group.types.orwhere.type.eq=2` |
| order                                     | 排序条件, 多个用 `,` 分割 | `order=id.desc,name`                                        |
| page                                      | 当前页码                  | `1`                                                         |
| pagesize                                  | 每页显示记录数量          | `15`                                                        |

支持的查询方法、匹配关系参考 [QueryParam 数据结构](../../model#31-数据结构)

[URL Query String 与 QueryParam 对照表](../../api/protocol/http.md#url-query-string-与-queryparam-对照表)

### 1.2 Response 响应

| 响应           | 数值               |
| -------------- | ------------------ |
| `Status Code`  | `200`              |
| `Content-Type` | `application/json` |
| `Body`         | `Object Paginate`  |

#### `Object Paginate` 带有分页信息的数据对象

| 字段     | 类型                | 说明                          |
| -------- | ------------------- | ----------------------------- |
| data     | Array\<Object Row\> | 数据记录集合                  |
| next     | Integer             | 下一页，如没有下一页返回 `-1` |
| prev     | Integer             | 上一页，如没有上一页返回 `-1` |
| page     | Integer             | 当前页码                      |
| pagesize | Integer             | 每页记录数量                  |
| pagecnt  | Integer             | 总页数                        |
| total    | Integer             | 总记录数                      |

## 2. 请求示例

### 2.1 Request

```bash
GET /api/table/user/search?where.status.eq=enabled&pagesize=2&page=1
```

| 请求参数        | 数值      |
| --------------- | --------- |
| where.status.eq | `enabled` |
| pagesize        | `2`       |
| page            | `1`       |

### 2.2 Response

```json
{
  "data": [
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
      "extra": {
        "sex": "男"
      },
      "id": 1,
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
      "name": "管理员"
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
      "extra": {
        "sex": "女"
      },
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
  ],
  "next": 2,
  "page": 1,
  "pagecnt": 2,
  "pagesize": 2,
  "prev": -1,
  "total": 3
}
```
