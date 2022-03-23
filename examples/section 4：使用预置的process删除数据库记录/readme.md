# 使用预置的process删除数据库记录

## 使用 process:Delete 新增数据库记录

首先，在 apis/hero.json 的 paths 字段中加入如下代码：

```json
{
      "path": "/delete/:id",
      "method": "POST",
      "process": "models.hero.Delete",
      "in": [
            "$param.id"
      ],
      "out": {
            "status": 200,
            "type": "application/json"
      }
}
```

然后进行请求，其中`$param.id`对应`:id`，如果请求成功，可以看到如下结果：

![img_result](https://tva1.sinaimg.cn/large/008i3skNly1gurioxoxqij61450u00wm02.jpg)
