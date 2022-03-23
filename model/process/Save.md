# Save

保存单条记录。如数据记录中包含主键字段则更新，不包含主键字段则创建记录；返回创建或更新的记录 ID。

## `save` 保存单条记录, 不存在创建记录, 存在更新记录, 返回记录 ID

### 处理器

`models.模型名称.Save`

### 参数表

| 参数    | 类型       | 说明     | 示例                                               |
| ------- | ---------- | -------- | -------------------------------------------------- |
| args[0] | Object Row | 数据记录 | `{"name": "用户创建","manu_id": 2,"type": "user"}` |

### 返回值

`Integer` 创建或更新的记录 ID

## 示例

### 数据模型

| 模型 | 模型定义                              |
| ---- | ------------------------------------- |
| user | [模型描述文件](../examples/user.json) |

### 处理器

```json
models.user.Save
```

### 参数表

```json
[
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
]
```

### 返回值

```json
101
```

## 外部引用

### 在业务逻辑(`Flow`) 中调用:

```json
{
  "nodes": [
    {
      "name": "user",
      "process": "models.user.Save",
      "args": [
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
      "path": "/save",
      "method": "POST",
      "process": "models.user.Save",
      "in": [":payload"],
      "out": {
        "status": 200,
        "type": "application/json"
      }
    }
  ]
}
```

```bash
POST /api/user/save
```

`REQUEST PAYLOAD`

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
