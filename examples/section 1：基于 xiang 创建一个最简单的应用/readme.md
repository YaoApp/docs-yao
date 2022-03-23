# 基于 xiang 创建一个最简单的应用

在开始之前，你需要对 xiang-象传引擎 的各个功能模块有一个简单的认知：

- models 数据库模型的json描述文件
- apis 接口的json描述文件
- flows 业务数据流的json描述文件
- plugins grpc支持的业务插件

## 安装mysql数据库

确认你的电脑已安装docker，启动docker engine，执行以下命令：

```bash
docker pull mysql
```

待镜像拉取完成执行，执行以下命令生成mysql容器，并将容器内部的数据卷映射到宿主机上：

```bash
docker run --name mysql -v /Users/xiewendao/Data/mysql:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=123456 -p 3306:3306 -d mysql
```

`/Users/xiewendao/Data/mysql:/var/lib/mysql`即为，宿主机数据卷存放位置:容器内部数据卷存放位置。注意前者需要根据个人电脑自行设置，这一步的目的是让数据库数据持久化到宿主机的磁盘上，后续直接启动容器，不需要再重复创建相关数据库。

执行完以上命令之后如果容器运行状态正常，且宿主机数据卷存放位置有相关mysql数据，则表示mysql启动成功，如果存在命令行卡死的情况，删除容器并重启docker engine即可。

## 创建xiang数据库

连接mysql数据库，创建名称为`xiang`的数据库，字符集为utf8，创建成功之后设置环境变量：

```bash
export XIANG_DB_PRIMARY="root:123456@tcp(localhost:3306)/xiang?charset=utf8mb4&parseTime=True&loc=Local"
```

全部环境变量如图所示，其中`XIANG_ROOT`、`XIANG_DB_PRIMARY`、`XIANG_STOR_PATH`需要根据实际情况设置：

![img_env](https://tva1.sinaimg.cn/large/008i3skNly1guqdehafmnj61n20aa0vh02.jpg)

## 学习xiang的命令

环境变量设置好之后，执行相关命令（根据平台）让环境变量生效，执行`xiang -h`查看象传引擎支持哪些命令，如下图：

![img_help](https://tva1.sinaimg.cn/large/008i3skNly1guqdk9dttoj60r80d2gmo02.jpg)

其中经常使用到的是`xiang start`和`xiang migrate`，`xiang start`用来启动项目，`xiang migrate`用来将model的变更同步到数据库的表中。

## 设计一个英雄并编写代码生成相关业务逻辑

首先，设计一个简单的英雄模型，叫做hero，并设定几条初始数据：

models/hero.json

```json
{
      "name": "英雄",
      "table": {
            "name": "hero",
            "comment": "英雄信息表",
            "engine": "InnoDB"
      },
      "columns": [
            {
                  "name": "id",
                  "type": "ID"
            },
            {
                  "label": "名称",
                  "name": "name",
                  "type": "string",
                  "length": 200,
                  "comment": "名称",
                  "unique": true
            },
            {
                  "label": "类型",
                  "name": "type",
                  "type": "enum",
                  "option": [
                        "AP",
                        "AD",
                        "Tank"
                  ],
                  "comment": "英雄类型：法师, 物理, 坦克",
                  "default": "AP",
                  "index": true
            },
            {
                  "label": "价格",
                  "name": "price",
                  "type": "integer",
                  "default": 1000,
                  "comment": "英雄价格"
            }
      ],
      "relations": {},
      "option": {
            "timestamps": true,
            "soft_deletes": true
      },
      "values": [
            {
                  "name": "艾希",
                  "type": "AD",
                  "price":1350
            },
            {
                  "name": "蛮王",
                  "type": "AD",
                  "price":3500
            },
            {
                  "name": "赵信",
                  "type": "AD",
                  "price":1350
            },
            {
                  "name": "杰斯",
                  "type": "AD",
                  "price":6300
            },
            {
                  "name": "卡特",
                  "type": "AP",
                  "price":3750
            },
            {
                  "name": "巨魔之王",
                  "type": "Tank",
                  "price":4800
            }
      ]
}
```

然后，使用 `xiang` 内置的`process:get`编写一个简单的查询接口：

apis/hero.json

```json
{
      "name": "英雄-接口",
      "version": "1.0.0",
      "description": "英雄相关接口",
      "group": "hero",
      "guard": "-",
      "paths": [
            {
                  "path": "/:id",
                  "method": "GET",
                  "process": "models.hero.Find",
                  "in": [
                        "$param.id",
                        ":params"
                  ],
                  "out": {
                        "status": 200,
                        "type": "application/json"
                  }
            }
      ]
}
```

先不要纠结每个字段的具体含义，暂时理解上述json的字面意义即可。

执行 `xiang start`，你会看到生成了如下接口 `http://local.iqka.com:5099/api/hero/:id`，试着使用浏览器或者postman访问一下`http://local.iqka.com:5099/api/hero/2`，如果一切正常，会得到以下结果：

![img_result](https://tva1.sinaimg.cn/large/008i3skNly1guqe2uol9vj60tw0c4my602.jpg)

是不是很简单，下面一节将会介绍自定义process的用法。
