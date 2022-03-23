# Delete

标记删除指定主键的单条数据记录. 如模型定义时未开启 `soft_deletes` 则真删除数据记录。

## `delete` 删除单条记录(标记删除)

### 处理器

`models.模型名称.Delete`

### 参数表

| 参数    | 类型       | 说明     | 示例 |
| ------- | ---------- | -------- | ---- |
| args[0] | Object Row | 模型主键 | `1`  |

### 返回值

`null` 无返回值

## 示例

### 数据模型

| 模型 | 模型定义                              |
| ---- | ------------------------------------- |
| user | [模型描述文件](../examples/user.json) |

### 处理器

```json
models.user.Delete
```

### 参数表

```json
[1]
```

### 返回值

```json
null
```

## 外部引用

### 在业务逻辑(`Flow`) 中调用:

```json
{
  "nodes": [
    {
      "name": "user",
      "process": "models.user.Delete",
      "args": [1],
      "outs": []
    }
  ]
}
```

### 在服务接口(`API`) 中调用:

```json
{
  "paths": [
    {
      "path": "/delete/:id",
      "method": "POST",
      "process": "models.user.Delete",
      "in": ["$params.id"],
      "out": {
        "status": 200
      }
    }
  ]
}
```

```bash
POST /api/user/delete/1
```
