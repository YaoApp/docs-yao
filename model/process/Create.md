# Create

创建单条记录, 返回新创建记录的主键

## `create` 创建单条记录, 返回新创建记录的 ID

### 处理器

`models.模型名称.Create`

### 参数表

| 参数    | 类型       | 说明     | 示例                                               |
| ------- | ---------- | -------- | -------------------------------------------------- |
| args[0] | Object Row | 数据记录 | `{"name": "用户创建","manu_id": 2,"type": "user"}` |

### 返回值

`Integer` 新创建的记录 ID

## 示例

### 数据模型

| 模型 | 模型定义                              |
| ---- | ------------------------------------- |
| user | [模型描述文件](../examples/user.json) |

### 处理器

```json
models.user.Create
```

### 参数表

```json
[
  {
    "name": "用户创建",
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
106
```

## 外部引用

### 在业务逻辑(`Flow`) 中调用:

```json
{
  "nodes": [
    {
      "name": "user",
      "process": "models.user.Create",
      "args": [
        {
          "name": "用户创建",
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
      "path": "/create",
      "method": "POST",
      "process": "models.user.Create",
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
POST /api/user/create
```

`REQUEST PAYLOAD`

```json
{
  "name": "用户创建",
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
