# 使用预置的 process 进行新增和修改

上一节介绍过了如何自定义 process 对数据进行处理，但事实上象传引擎提供了大量预置的 process，你只需了解了这些 process 的用法，对于一般的中小型应用而言，即可满足 80%的业务需求。

## 使用 process:Create 新增数据库记录

首先，在 apis/hero.json 的 paths 字段中加入如下代码：

```json
{
	"path": "/create",
	"method": "POST",
	"process": "models.hero.Create",
	"in": [":payload"],
	"out": {
		"status": 200,
		"type": "application/json"
	}
}
```

其中`:payload`对应的 POST 请求传输的**json**数据，然后进行请求，如果请求成功，会得到对应的记录 ID：

![img_result](https://tva1.sinaimg.cn/large/008i3skNly1gurffjhclpj60wq0u040802.jpg)

## 使用 process:Update 更新数据库记录

首先，在 apis/hero.json 的 paths 字段中加入如下代码：

```json
{
	"path": "/update/:id",
	"method": "POST",
	"process": "models.hero.Update",
	"in": ["$params.id", ":payload"],
	"out": {
		"status": 200,
		"type": "application/json"
	}
}
```

其中`:payload`对应的 POST 请求传输的**json**数据，然后进行请求：

![img_result](https://tva1.sinaimg.cn/large/008i3skNly1gurfq9ibuij60u010cq6102.jpg)

可以看到，无极剑圣的type由AD变成了AP，下一节将介绍如何删除数据库记录。
