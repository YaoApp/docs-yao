# POST /delete/where

按条件批量删除数据, 请求成功返回删除行数；请求失败返回错误对象。 [查看异常规范](../../api/protocol/http.md#4-异常规范)。

默认绑定数据模型的 [DeleteWhere](../../model/process/DeleteWhere.md) 处理器。

## 1. 接口文档

| 请求 | 数值                                     |
| ---- | ---------------------------------------- |
| 方法 | `POST`                                   |
| 路由 | `/api/xiang/table/表格名称/delete/where` |

### 1.1 Request 请求

#### URL Query String

| 请求参数                                  | 说明                      | 示例                                                        |
| ----------------------------------------- | ------------------------- | ----------------------------------------------------------- |
| 查询方法.字段名称.匹配关系                | 字段匹配关系查询          | `where.status.eq=enabled`, `orwhere.status.eq=disabled`     |
| 查询方法.关联模型名称.字段名称.匹配关系   | 关联模型字段匹配关系查询  | `where.mother.friends.status.eq=enabled`,                   |
| group.分组名称.查询方法.字段名称.匹配关系 | 字段匹配关系分组查询      | `group.types.where.type.eq=1&group.types.orwhere.type.eq=2` |
| order                                     | 排序条件, 多个用 `,` 分割 | `order=id.desc,name`                                        |
| limit                                     | 限定最大行数              | `100`                                                       |

支持的查询方法、匹配关系参考 [QueryParam 数据结构](../../model#31-数据结构)

[URL Query String 与 QueryParam 对照表](../../api/protocol/http.md#url-query-string-与-queryparam-对照表)

### 1.2 Response 响应

| 响应           | 数值               |
| -------------- | ------------------ |
| `Status Code`  | `200`              |
| `Content-Type` | `application/json` |
| `Body`         | `Integer`          |

## 2. 请求示例

### 2.1 Request

```bash
POST /api/table/user/delete/where?where.status.eq=enabled&limit=100
```

| 请求参数        | 数值      |
| --------------- | --------- |
| where.status.eq | `enabled` |
| limit           | `100`     |

### 2.2 Response

```json
100
```
