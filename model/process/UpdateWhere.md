# UpdateWhere

按条件更新数据记录, 返回更新行数

## `updateWhere` 按条件更新记录, 返回更新行数

### 处理器

`models.模型名称.UpdateWhere`

### 参数表

| 参数    | 类型              | 说明     | 示例                                             |
| ------- | ----------------- | -------- | ------------------------------------------------ |
| args[0] | Object QueryParam | 查询条件 | `{"wheres":[{"column":"name", "value":"张三"}]}` |
| args[1] | Object Row        | 数据记录 | `{"balance": 200}`                               |

### 返回值

`Integer` 更新行数

## 示例

### 数据模型

| 模型 | 模型定义                              |
| ---- | ------------------------------------- |
| user | [模型描述文件](../examples/user.json) |

### 处理器

```json
models.user.UpdateWhere
```

### 参数表

```json
[
  {
    "wheres": [{ "column": "status", "value": "enabled" }]
  },
  {
    "balance": 200
  }
]
```

### 返回值

```json
4
```

## 外部引用

### 在业务逻辑(`Flow`) 中调用:

```json
{
  "nodes": [
    {
      "name": "users",
      "process": "models.user.UpdateWhere",
      "args": [
        {
          "wheres": [{ "column": "status", "value": "enabled" }]
        },
        {
          "balance": 200
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
      "path": "/updatewhere",
      "method": "POST",
      "process": "models.user.UpdateWhere",
      "in": [":params", ":payload"],
      "out": {
        "status": 200,
        "type": "application/json"
      }
    }
  ]
}
```

```bash
POST /api/user/updatewhere?where.status.eq=enabled
```

`REQUEST PAYLOAD`

```json
{
  "balance": 200
}
```
