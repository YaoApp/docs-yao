# 自定义process对数据进行处理

上一节介绍过了象传引擎的基本用法，这一节介绍如何使用自定义process请求特定格式的数据，模型依然沿用之前设计好的hero。

首先，在apis/hero.json中加入如下代码：

![img_hero](https://tva1.sinaimg.cn/large/008i3skNly1gureqjok1ej60u01auwh802.jpg)

其中`process`字段对应的值为`flows.sort`，记住这个值。

然后在flows文件夹创建名为`sort.flow.json`的文件，文件内容如下：

```json
{
      "label": "排序",
      "version": "1.0.0",
      "description": "获取排序之后的数据",
      "nodes": [
            {
                  "name": "hero",
                  "process": "models.hero.get",
                  "args": [
                        {
                              "select": [
                                    "id",
                                    "name",
                                    "type",
                                    "price"
                              ],
                              "orders": [
                                    {
                                          "column": "price",
                                          "option": "desc"
                                    }
                              ]
                        }
                  ],
                  "outs": [
                        "{{$out}}"
                  ]
            }
      ],
      "output": {
            "data": {
                  "heros": "{{$res.hero.0}}"
            }
      }
}
```

需要这里需要重点关注的字段是`args`字段，该字段会编译成sql指令，去数据库取数据，取到的数据通过`outs`字段导出，在`output`中通过`$res`变量即可获取到。

这时再访问`http://local.iqka.com:5099/api/hero/sort`会得到如下结果：

![img_result](https://tva1.sinaimg.cn/large/008i3skNly1gurezbibeuj60u015g77802.jpg)

自定义process能够满足一些特定的业务需求，当预置的process无法满足要求时。下一节将会介绍如何使用预置的`process.Create`（model.hero.Create）往数据库添加新的英雄。
