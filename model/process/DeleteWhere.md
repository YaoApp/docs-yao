# DeleteWhere

按条件标记删除数据, 返回删除行数。如模型定义时未开启 `soft_deletes` 则真删除数据记录。

## `deleteWhere` 按条件标记删除数据, 返回删除行数

### 处理器

`models.模型名称.DeleteWhere`

### 参数表

| 参数    | 类型              | 说明     | 示例                                             |
| ------- | ----------------- | -------- | ------------------------------------------------ |
| args[0] | Object QueryParam | 查询条件 | `{"wheres":[{"column":"name", "value":"张三"}]}` |

### 返回值

`Integer` 删除行数

## 示例

### 数据模型

| 模型 | 模型定义                              |
| ---- | ------------------------------------- |
| user | [模型描述文件](../examples/user.json) |

### 处理器

```json
models.user.DeleteWhere
```

### 参数表

```json
[
  {
    "wheres": [{ "column": "status", "value": "enabled" }]
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
      "process": "models.user.DeleteWhere",
      "args": [
        {
          "wheres": [{ "column": "status", "value": "enabled" }]
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
      "path": "/deletewhere",
      "method": "POST",
      "process": "models.user.DeleteWhere",
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
POST /api/user/deletewhere?where.status.eq=enabled
```
