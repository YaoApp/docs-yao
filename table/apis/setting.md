# GET /setting

读取数据表格配置信息, 请求成功返回配置信息对象；请求失败返回错误对象。 [查看异常规范](../../api/protocol/http.md#4-异常规范)。

## 1. 接口文档

| 请求 | 数值                                |
| ---- | ----------------------------------- |
| 方法 | `GET`                               |
| 路由 | `/api/xiang/table/表格名称/setting` |

### 1.1 Request 请求

#### 请求参数

| URL Query String | 说明                                            | 示例                |
| ---------------- | ----------------------------------------------- | ------------------- |
| select           | 配置项名称，多个用 `,` 分割, 默认返回全部配置项 | `list`, `list,edit` |

### 1.2 Response 响应

| 响应           | 数值               |
| -------------- | ------------------ |
| `Status Code`  | `200`              |
| `Content-Type` | `application/json` |
| `Body`         | `Object Setting`   |

#### `Object Setting` 数据结构

| 字段       | 类型                         | 说明                                                                                                                                                                             |
| ---------- | ---------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| name       | String                       | 数据表格名称 [查看完整说明](#21-基础信息)                                                                                                                                        |
| title      | String                       | 打开数据表格页面时，浏览器栏呈现的页面标题                                                                                                                                       |
| decription | String                       | 数据表格介绍, 可用于开发平台中呈现                                                                                                                                               |
| columns    | \[key:String\]:Object Column | 字段呈现方式设置。 如设置绑定数据模型，自动根据字段类型信息设置关联组件，可通过设置同 `key` 的配置信息，覆盖自动生成的关联组件信息。 [查看完整说明](../#24-字段呈现方式-columns) |
| filters    | \[key:String\]:Object Filter | 查询过滤器设置。 如设置绑定数据模型，自动根据索引和字段信息设置关联组件，可通过设置同 `key` 的配置信息，覆盖自动生成的关联组件信息。 [查看完整说明](../#25-查询过滤器-fliters)   |
| list       | Object Page                  | 列表页设置。 [查看完整说明](../#26-列表页-list)                                                                                                                                  |
| edit       | Object Page                  | 编辑页设置。 [查看完整说明](../#27-编辑页-edit)                                                                                                                                  |
| view       | Object Page                  | 查看页设置。 [查看完整说明](../#28-查看页-view)                                                                                                                                  |
| insert     | Object Page                  | 批量录入页设置。 [查看完整说明](../#29-批量录入页-insert)                                                                                                                        |

## 2. 请求示例

### 2.1 Request

```bash
GET /api/table/service/setting
```

### 2.2 Response

```json
{
  "name": "云服务库",
  "decription": "可信云云服务库",
  "columns": {
    "服务名称": {
      "label": "服务名称",
      "view": {
        "type": "label",
        "props": {
          "value": ":name"
        }
      },
      "edit": {
        "type": "input",
        "props": {
          "value": ":name"
        }
      }
    },
    "所属厂商": {
      "label": "所属厂商",
      "view": {
        "name": "label",
        "props": {
          "value": ":manu.short_name"
        }
      },
      "edit": {
        "type": "select",
        "props": {
          "value": ":manu.id",
          "searchable": true,
          "remote": {
            "api": "/api/manu/get",
            "query": {
              "select": ["id", "name"],
              "keyword": "where_name_like"
            }
          }
        }
      }
    },
    "服务类型": {
      "label": "服务类型",
      "view": {
        "name": "label",
        "props": {
          "value": ":kind.name"
        }
      },
      "edit": {
        "type": "select",
        "props": {
          "value": ":kind.id",
          "tree": true,
          "searchable": true,
          "remote": {
            "api": "/api/kind/tree",
            "query": {
              "select": ["id", "name"],
              "keyword": "where_name_like"
            }
          }
        }
      }
    },
    "服务领域": {
      "label": "服务领域",
      "view": {
        "name": "tags",
        "props": {
          "value": ":fields"
        }
      },
      "edit": {
        "type": "select",
        "props": {
          "value": ":fields",
          "searchable": true,
          "inputable": true,
          "multiple": true,
          "options": [
            { "label": "视频会议", "value": "视频会议" },
            { "label": "即时通信", "value": "即时通信" },
            { "label": "客服管理", "value": "客服管理" },
            { "label": "财务管理", "value": "财务管理" },
            { "label": "客户关系管理", "value": "客户关系管理" },
            { "label": "营销管理", "value": "营销管理" },
            { "label": "办公自动化", "value": "办公自动化" },
            { "label": "ERP", "value": "ERP" },
            { "label": "人力", "value": "人力" },
            { "label": "采购", "value": "采购" },
            { "label": "供应链", "value": "供应链" },
            { "label": "企业网盘", "value": "企业网盘" },
            { "label": "邮件服务", "value": "邮件服务" },
            { "label": "电子合同", "value": "电子合同" },
            { "label": "安全工具", "value": "安全工具" },
            { "label": "舆情分析", "value": "舆情分析" },
            { "label": "行业应用", "value": "行业应用" },
            { "label": "其他", "value": "其他" }
          ]
        }
      }
    },
    "计费方式": {
      "label": "计费方式",
      "view": {
        "name": "tags",
        "props": {
          "value": ":fields"
        }
      },
      "edit": {
        "type": "select",
        "props": {
          "value": ":price_options",
          "multiple": true,
          "options": [
            { "label": "按年订阅", "value": "按年订阅" },
            { "label": "按月订阅", "value": "按月订阅" },
            { "label": "按量计费", "value": "按量计费" },
            { "label": "私有化部署", "value": "私有化部署" },
            { "label": "其他", "value": "其他" }
          ]
        }
      }
    },
    "行业覆盖": {
      "label": "行业覆盖",
      "view": {
        "name": "tags",
        "props": {
          "value": ":industries"
        }
      },
      "edit": {
        "type": "select",
        "props": {
          "value": ":industries",
          "inputable": true,
          "multiple": true,
          "options": [
            { "label": "房地产", "value": "房地产" },
            { "label": "旅游", "value": "旅游" },
            { "label": "教育", "value": "教育" },
            { "label": "互联网", "value": "互联网" },
            { "label": "其他", "value": "其他" }
          ]
        }
      }
    },
    "状态": {
      "label": "状态",
      "view": {
        "name": "tags",
        "props": {
          "value": ":status",
          "options": [
            { "label": "开启", "value": "enabled", "color": "primary" },
            { "label": "关闭", "value": "disabled", "color": "danger" }
          ]
        }
      },
      "edit": {
        "type": "select",
        "props": {
          "value": ":status",
          "options": [
            { "label": "开启", "value": "enabled" },
            { "label": "关闭", "value": "disabled" }
          ]
        }
      }
    },
    "创建时间": {
      "label": "创建时间",
      "view": {
        "name": "label",
        "props": {
          "value": ":created_at",
          "datetime-format": "YYYY年MM月DD日 @hh:mm:ss"
        }
      }
    },
    "更新时间": {
      "label": "更新时间",
      "view": {
        "name": "label",
        "props": {
          "value": ":update_at",
          "datetime-format": "YYYY年MM月DD日 @hh:mm:ss"
        }
      }
    },
    "查询排序": {
      "label": "查询排序",
      "view": {
        "type": "label",
        "props": {
          "value": ":rank"
        }
      },
      "edit": {
        "type": "input",
        "props": {
          "value": ":rank",
          "type": "number"
        }
      }
    }
  },
  "filters": {
    "关键词": {
      "label": "关键词",
      "bind": "where.name.like",
      "input": {
        "type": "input",
        "props": {
          "placeholder": "请输入关键词"
        }
      }
    },
    "所属厂商": {
      "label": "厂商",
      "bind": "where.manu_id.in",
      "input": {
        "type": "select",
        "props": {
          "searchable": true,
          "multiple": true,
          "placeholder": "请选择所属厂商",
          "remote": {
            "api": "/api/manu/get",
            "query": {
              "select": ["id", "name"],
              "keyword": "where.name.like"
            }
          }
        }
      }
    },
    "服务类型": {
      "label": "类型",
      "bind": "where.kind_id.in",
      "input": {
        "type": "select",
        "props": {
          "tree": true,
          "searchable": true,
          "multiple": true,
          "placeholder": "请选择所属类型",
          "remote": {
            "api": "/api/kind/tree",
            "query": {
              "select": ["id", "name"],
              "keyword": "where.name.like"
            }
          }
        }
      }
    }
  },
  "list": {
    "primary": "id",
    "layout": {
      "columns": [
        { "name": "服务名称", "width": 6 },
        { "name": "所属厂商", "width": 6 },
        { "name": "服务类型", "width": 4 },
        { "name": "状态", "width": 4 },
        { "name": "服务领域", "width": 4 },
        { "name": "计费方式", "width": 4 },
        { "name": "创建时间", "width": 6 },
        { "name": "更新时间", "width": 6 }
      ],
      "filters": [
        { "name": "关键词", "width": 6 },
        { "name": "所属厂商", "width": 6 },
        { "name": "服务类型", "width": 4 }
      ]
    },
    "actions": {
      "create": {
        "type": "button",
        "props": {
          "label": "新建服务",
          "icon": "fas fa-plus"
        }
      },
      "view": {},
      "edit": {},
      "import": {},
      "update": {},
      "delete": {},
      "insert": {},
      "updateWhere": {},
      "deleteWhere": {},
      "updateSelect": {},
      "deleteSelect": {},
      "pagination": ["pages", "prev", "next"],
      "setting": {}
    }
  },
  "edit": {
    "primary": "id",
    "layout": {
      "fieldset": [
        {
          "title": "基础信息",
          "description": "",
          "columns": [
            { "name": "服务名称", "width": 6 },
            { "name": "所属厂商", "width": 6 },
            { "name": "服务类型", "width": 6 },
            { "name": "状态", "width": 6 },
            { "name": "rank", "width": 6 }
          ]
        },
        {
          "title": "数据标签",
          "description": "",
          "columns": ["服务领域", "计费方式", "行业覆盖"]
        }
      ]
    },
    "actions": {
      "cancel": {},
      "save": {
        "type": "button",
        "props": {
          "label": "保存"
        }
      },
      "delete": {}
    }
  },
  "insert": {},
  "view": {}
}
```
