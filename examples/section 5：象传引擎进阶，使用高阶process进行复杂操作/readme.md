# 象传引擎进阶，使用高阶process进行复杂操作

## 使用 process:Get 获取指定类型的数据

首先，在 apis/hero.json 的 paths 字段中加入如下代码：

```json
{
      "path": "/search",
      "method": "GET",
      "process": "models.hero.Get",
      "in": [
            ":params"
      ],
      "out": {
            "status": 200,
            "type": "application/json"
      }
}
```

然后进行请求，其中`:params`对应`get请求的参数`，如果请求成功，可以看到如下结果：

![img_Get](https://tva1.sinaimg.cn/large/008i3skNly1gurj31twx9j60u00vuwgx02.jpg)

## 使用 process:Insert 插入多条数据

首先，在 apis/hero.json 的 paths 字段中加入如下代码：

```json
{
      "path": "/insert",
      "method": "POST",
      "process": "models.hero.Insert",
      "in": [
            "$payload.columns",
            "$payload.data"
      ],
      "out": {
            "status": 200,
            "type": "application/json"
      }
}
```

然后进行请求，如果请求成功，可以看到如下结果：

![img_Insert](https://tva1.sinaimg.cn/large/008i3skNly1gurjq2z16xj60u017gq7002.jpg)

## 使用 process:UpdateWhere 插入多条数据

首先，在 apis/hero.json 的 paths 字段中加入如下代码：

```json
{
      "path": "/update_where",
      "method": "POST",
      "process": "models.hero.UpdateWhere",
      "in": [
            ":params",
            ":payload"
      ],
      "out": {
            "status": 200,
            "type": "application/json"
      }
}
```

然后进行请求，如果请求成功，可以看到如下结果：

![img_updateWhere](https://tva1.sinaimg.cn/large/008i3skNly1gurjzbxkfbj60u016edjw02.jpg)