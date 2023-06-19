# API文档

> v1.0.0

Base URLs:

* <a href=" http://127.0.0.1:32800">本地环境:  http://127.0.0.1:32800</a>

# 用户相关

## POST 列表

POST /mb_api/pushmsg/hulk/v1/user/list/{appid}

> Body 请求参数

```json
{
  "tids": [],
  "versions": [],
  "alias": [],
  "offset": 0,
  "models": [],
  "uids": [
    "auid55245",
    "iii",
    "auid00000007"
  ],
  "locations": [],
  "platforms": [],
  "phones": [],
  "imeis": [],
  "size": 100
}
```

### 请求参数

|名称|位置|类型|必选|说明|
|---|---|---|---|---|
|appid|path|string| 是 |none|
|body|body|object| 否 |none|
|» alias|body|[string]| 否 |none|
|» locations|body|[string]| 否 |none|
|» platforms|body|[string]| 否 |none|
|» models|body|[string]| 否 |none|
|» versions|body|[string]| 否 |none|
|» size|body|integer| 否 |none|
|» offset|body|integer| 否 |none|
|» uids|body|[string]| 否 |uid列表|
|» tids|body|[string]| 否 |none|
|» phones|body|[string]| 否 |none|
|» imeis|body|[string]| 否 |none|

> 返回示例

> 200 Response

```json
{}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|Inline|

### 返回数据结构

## GET 详情

GET /mb_api/pushmsg/hulk/v1/user/info/{appid}/{bundle}

### 请求参数

|名称|位置|类型|必选|说明|
|---|---|---|---|---|
|appid|path|string| 是 |none|
|bundle|path|string| 是 |none|

> 返回示例

> 200 Response

```json
{}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|Inline|

### 返回数据结构

## GET 平台与版本号列表

GET /mb_api/pushmsg/hulk/v1/user/sysvers

### 请求参数

|名称|位置|类型|必选|说明|
|---|---|---|---|---|
|bundle|query|string| 否 |none|

> 返回示例

> 成功

```json
{
  "android": [
    "11",
    "10",
    "12"
  ],
  "ios": [
    "15.4",
    "15.5",
    "13.4.1",
    "14.8.1",
    "15.2"
  ]
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» android|[string]|true|none||none|
|» ios|[string]|true|none||none|

## POST 总数

POST /mb_api/pushmsg/hulk/v1/user/count/{appid}

> Body 请求参数

```json
{
  "id": "{% mock 'uuid' %}",
  "where": {
    "alias": [],
    "imeis": [],
    "phones": [],
    "uids": [
      "auid55245",
      "iuid82780"
    ],
    "tids": [],
    "locations": [],
    "platform": [
      "android:8.1.0",
      "android:12",
      "android:10",
      "android:11",
      "ios:16.0",
      "ios:15.6.1",
      "ios:15.5",
      "ios:15.6",
      "ios:15.0.2"
    ],
    "created_at": [],
    "updated_at": []
  }
}
```

### 请求参数

|名称|位置|类型|必选|说明|
|---|---|---|---|---|
|appid|path|string| 是 |none|
|Content-Type|header|string| 否 |none|
|body|body|object| 否 |none|
|» id|body|string| 是 |none|
|» where|body|object| 是 |none|
|»» alias|body|[string]| 是 |none|
|»» imeis|body|[string]| 是 |none|
|»» phones|body|[string]| 是 |none|
|»» uids|body|[string]| 是 |none|
|»» tids|body|[string]| 是 |none|
|»» locations|body|[string]| 是 |none|
|»» platform|body|[string]| 是 |none|
|»» created_at|body|[string]| 是 |none|
|»» updated_at|body|[string]| 是 |none|

> 返回示例

> 成功

```json
{
  "code": 0,
  "message": "",
  "extend": null,
  "data": {
    "count": 20010,
    "req_id": "b4d2c096-5e6e-11ed-aecc-00163e017386"
  }
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» code|integer|true|none||none|
|» message|string|true|none||none|
|» extend|null|true|none||none|
|» data|object|true|none||none|
|»» count|integer|true|none||总数|
|»» req_id|string|true|none||req id|

## POST 保存群组条件

POST /mb_api/pushmsg/hulk/v1/user/group/{appid}

> Body 请求参数

```json
{
  "id": "{% mock 'uuid' %}",
  "where": {
    "alias": [],
    "imeis": [],
    "phones": [],
    "uids": [
      "auid55245",
      "iuid82780"
    ],
    "tids": [],
    "locations": [],
    "platform": [
      "android:8.1.0",
      "android:12",
      "android:10",
      "android:11",
      "ios:16.0",
      "ios:15.6.1",
      "ios:15.5",
      "ios:15.6",
      "ios:15.0.2"
    ],
    "created_at": [],
    "updated_at": []
  }
}
```

### 请求参数

|名称|位置|类型|必选|说明|
|---|---|---|---|---|
|appid|path|string| 是 |none|
|Content-Type|header|string| 否 |none|
|body|body|object| 否 |none|
|» id|body|string| 否 |群组ID|
|» where|body|object| 是 |群组条件|
|»» alias|body|[string]| 否 |none|
|»» imeis|body|[string]| 否 |none|
|»» phones|body|[string]| 否 |none|
|»» uids|body|[string]| 否 |none|
|»» tids|body|[string]| 否 |none|
|»» locations|body|[string]| 否 |none|
|»» platform|body|[string]| 否 |none|
|»» created_at|body|[string]| 否 |none|
|»» updated_at|body|[string]| 否 |none|
|»» register_day|body|integer| 否 |N天内注册|
|»» activate_day|body|integer| 否 |N天内活跃|

> 返回示例

> 成功

```json
{
  "code": 0,
  "message": "",
  "extend": null,
  "data": {
    "count": 20010,
    "req_id": "b4d2c096-5e6e-11ed-aecc-00163e017386"
  }
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» code|integer|true|none||none|
|» message|string|true|none||none|
|» extend|null|true|none||none|
|» data|object|true|none||none|
|»» count|integer|true|none||总数|
|»» req_id|string|true|none||req id|

## POST 更新用户第三方信息

POST /mb_api/pushmsg/hulk/v1/user/third_partys/{appid}

> Body 请求参数

```json
{
  "users": [
    {
      "uid": "18125160155",
      "channel": "wechat",
      "token": "u.sfwduayon@lxteofsmo.bv"
    },
    {
      "uid": "18604578848",
      "channel": "wechat",
      "token": "h.rkntku@nhuzuysf.mt"
    },
    {
      "uid": "19821572026",
      "channel": "email",
      "token": "w.ihtjj@crf.am"
    },
    {
      "uid": "19821572026",
      "channel": "wechat",
      "token": "w.ihtjj@wechat.am"
    }
  ]
}
```

### 请求参数

|名称|位置|类型|必选|说明|
|---|---|---|---|---|
|appid|path|string| 是 |none|
|body|body|object| 否 |none|
|» users|body|[object]| 是 |none|
|»» uid|body|string| 是 |none|
|»» channel|body|string| 是 |none|
|»» token|body|string| 是 |none|

> 返回示例

> 成功

```json
{
  "code": 0,
  "message": "ok",
  "extend": null,
  "data": {
    "count": 4
  }
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|Inline|

### 返回数据结构

## GET 获取用户第三方信息列表

GET /mb_api/pushmsg/hulk/v1/user/third_party/{appid}

> Body 请求参数

```json
{}
```

### 请求参数

|名称|位置|类型|必选|说明|
|---|---|---|---|---|
|appid|path|string| 是 |none|
|uid|query|string| 否 |none|
|channel|query|string| 否 |none|
|offset|query|integer| 否 |none|
|size|query|string| 否 |none|
|body|body|object| 否 |none|

> 返回示例

> 成功

```json
{
  "code": 0,
  "message": "ok",
  "extend": null,
  "data": {
    "Count": 1,
    "Users": [
      {
        "UID": "19821572026",
        "AppID": "hulk4015d",
        "CreatedAt": "0001-01-01 00:00:00 +0000 UTC",
        "UpdatedAt": "0001-01-01 00:00:00 +0000 UTC",
        "ThirdParty": [
          {
            "UID": "19821572026",
            "AppID": "hulk4015d",
            "Channel": "wechat",
            "Token": "w.ihtjj@wechat.am"
          },
          {
            "UID": "19821572026",
            "AppID": "hulk4015d",
            "Channel": "email",
            "Token": "w.ihtjj@crf.am"
          }
        ]
      }
    ]
  }
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|Inline|

### 返回数据结构

## DELETE 删除用户第三方信息

DELETE /mb_api/pushmsg/hulk/v1/user/third_party/{appid}

> Body 请求参数

```json
{
  "uid": "19821572026,18604578848",
  "channel": "email,wechat"
}
```

### 请求参数

|名称|位置|类型|必选|说明|
|---|---|---|---|---|
|appid|path|string| 是 |none|
|body|body|object| 否 |none|
|» uid|body|string| 是 |none|
|» channel|body|string| 是 |none|

> 返回示例

> 成功

```json
{
  "code": 0,
  "message": "ok",
  "extend": null,
  "data": {
    "Count": 2,
    "Users": [
      {
        "UID": "19821572026",
        "AppID": "hulk4015d",
        "ThirdParty": [
          {
            "UID": "19821572026",
            "AppID": "hulk4015d",
            "Channel": "email",
            "Token": "w.ihtjj@crf.am"
          },
          {
            "UID": "19821572026",
            "AppID": "hulk4015d",
            "Channel": "wechat",
            "Token": "w.ihtjj@wechat.am"
          }
        ]
      },
      {
        "UID": "18604578848",
        "AppID": "hulk4015d",
        "ThirdParty": [
          {
            "UID": "18604578848",
            "AppID": "hulk4015d",
            "Channel": "wechat",
            "Token": "h.rkntku@nhuzuysf.mt"
          }
        ]
      }
    ]
  }
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|Inline|

### 返回数据结构

## POST 新增用户第三方信息

POST /mb_api/pushmsg/hulk/v1/user/third_party/{appid}

> Body 请求参数

```json
{
  "uid": "123456",
  "third_part": [
    {
      "Token": "ojaOY5v2bAFZp-hfS9BWZZWngmh8",
      "Channel": "wechat"
    }
  ]
}
```

### 请求参数

|名称|位置|类型|必选|说明|
|---|---|---|---|---|
|appid|path|string| 是 |none|
|body|body|object| 否 |none|
|» uid|body|string| 是 |none|
|» third_part|body|[object]| 是 |none|
|»» Channel|body|string| 否 |none|
|»» Token|body|string| 否 |none|

> 返回示例

> 成功

```json
{
  "code": 0,
  "message": "ok",
  "extend": null,
  "data": {
    "count": 4
  }
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|Inline|

### 返回数据结构

# 任务相关

## POST 推送

POST /mb_api/pushmsg/hulk/v1/universal/{type_subtype}/{appid}

> Body 请求参数

```json
"{\n    \"uids\": [],\n    \"tids\": [],\n    \"sms\": {\n        \"template\": \"esse in\",\n        \"params\": \"est labore\"\n    },\n    \"email\": {\n        \"title\": \"京传美\",\n        \"content\": \"consectetur Duis\"\n    },\n    \"wechat\": {\n        \"template_id\": \"97\",\n        \"data\": {},\n        \"miniprogram\": {\n            \"appid\": \"30\",\n            \"pagepath\": \"ut velit Lorem\"\n        },\n        \"url\": \"http://uock.pf/gvjb\",\n        \"client_msg_id\": \"41\"\n    },\n    \"app\": {\n        \"title\": \"龙已改界\",\n        \"alert\": \"ut Ut ad et\",\n        \"intent\": {\n            \"url\": \"http://ocekafhs.dj/pbzdmdjajj\"\n        },\n        \"extras\": \"voluptate\",\n        \"small_icon_url\": \"http://dummyimage.com/100x100\",\n        \"full\": false,\n        \"voice\": 95,\n        \"vibrate\": 47\n    },\n    \"locations\": [],\n    \"alias\": [\n        \"Ut minim in\",\n        \"culpa ut minim\"\n    ],\n    \"created_at\": [\n        \"1975-05-28 01:20:47\",\n        \"1994-05-08 06:13:49\",\n    ],\n    \"system_versions\": [],\n    \"platform\": [\n        \"id\",\n        \"sed deserunt eu\",\n        \"exercitation id\"\n    ],\n    \"updated_at\": [\n        \"1971-05-26 16:45:07\",\n        \"2011-09-19 16:44:05\"\n    ],\n    \"phones\": [\n        \"18668778148\"\n    ]\n}"
```

### 请求参数

|名称|位置|类型|必选|说明|
|---|---|---|---|---|
|type_subtype|path|string| 是 |none|
|appid|path|string| 是 |none|
|push-channels|header|string| 否 |none|
|body|body|object| 否 |none|
|» uids|body|[string]| 是 |uid组|
|» app|body|object| 是 |none|
|»» title|body|string| 是 |none|
|»» alert|body|string| 是 |none|
|»» intent|body|object| 是 |none|
|»»» url|body|string| 是 |none|
|»» extras|body|string| 是 |none|
|»» small_icon_url|body|string| 是 |none|
|»» full|body|boolean| 是 |none|
|»» voice|body|integer| 是 |none|
|»» vibrate|body|integer| 是 |none|
|»» category|body|object| 是 |消息分类规则|
|»»» hpush|body|string| 是 |华为渠道规则|
|»»» xiaomi|body|string| 是 |小米渠道规则|
|» tids|body|[string]| 是 |tid组|
|» sms|body|object| 否 |短信|
|»» template|body|string| 是 |短信模板code|
|»» params|body|string| 是 |短息模板参数|
|» email|body|object| 否 |none|
|»» title|body|string| 是 |none|
|»» content|body|string| 是 |none|
|» wechat|body|object| 否 |微信推送|
|»» template_id|body|string| 是 |模板ID|
|»» data|body|object| 是 |模板参数|
|»» miniprogram|body|object| 否 |跳小程序所需数据|
|»»» appid|body|string| 是 |所需跳转到的小程序appid（该小程序 appid|
|»»» pagepath|body|string| 是 |所需跳转到小程序的具体页面路径，支持带参数,（示例index?foo=bar）|
|»» url|body|string| 是 |模板跳转链接|
|»» client_msg_id|body|string| 否 |防重入id|
|» created_at|body|[string]| 否 |注册时间段|
|» updated_at|body|[string]| 否 |活跃时间段|
|» system_versions|body|[string]| 否 |系统版本(string类型非int类型): ["10", "11"]|
|» alias|body|[string]| 否 |别名组|
|» locations|body|[string]| 否 |区域：028=成都|
|» phones|body|[string]| 否 |手机号组：[130xxxxxxxx]|
|» platform|body|[string]| 否 |平台组:["ios", "android"]|

> 返回示例

> 成功

```json
{
  "code": 0,
  "message": "",
  "extend": null,
  "data": {
    "req_id": "71034a0d-8048-11ed-ab0f-00163e017386"
  }
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» code|integer|true|none||none|
|» message|string|true|none||none|
|» extend|null|true|none||none|
|» data|object|true|none||none|
|»» req_id|string|true|none||none|

## GET 详情

GET /mb_api/pushmsg/hulk/v1/task/detail

### 请求参数

|名称|位置|类型|必选|说明|
|---|---|---|---|---|
|offset|query|integer| 否 |none|
|size|query|integer| 否 |none|
|req_id|query|string| 否 |none|
|uid|query|string| 否 |none|
|imei|query|string| 否 |none|
|phone|query|string| 否 |none|
|alias|query|string| 否 |none|
|channel|query|string| 否 |unknown=未知的渠道(默认的错误渠道)、ios=ios、thanos=自建渠道、hw=华为、vivo=vivo、oppo=oppo、mi=小米、meizu=魅族、wechat=微信公众号、spush=短信、email=邮箱|
|success|query|integer| 否 |0=未送达、1=推送中、2=未读、3=已读、4=撤回中、5=已撤回、如果不筛选这个字段传null或这个不传|

> 返回示例

> 成功

```json
{
  "count": 2,
  "data": [
    {
      "id": 1,
      "updated_at": "2022-05-26T11:53:19.907+08:00",
      "task_id": 348687,
      "tid": "199edc9f60e6ccdc83ecec1d1f8c6311",
      "bundle": "cn.zsmarter.hulk",
      "uid": "auid04008",
      "imei": "b8479d18cc58ddea",
      "alias": "aalias90316",
      "phone": "15892280079",
      "push_type": "hw",
      "success": 1,
      "message": ""
    },
    {
      "id": 2,
      "updated_at": "2022-05-26T11:53:19.907+08:00",
      "task_id": 348687,
      "tid": "90f4b3ffb7e97eab503174730a04d50e",
      "bundle": "cn.zsmarter.hulk",
      "uid": "auid41621",
      "imei": "adid03592",
      "alias": "这是我测试用的别名",
      "phone": "15892280079",
      "push_type": "hw",
      "success": 1,
      "message": ""
    }
  ],
  "expect_pushed": 2,
  "had_pushed": 3,
  "render": 0
}
```

```json
{
  "count": 0,
  "data": [],
  "expect_pushed": 0,
  "had_pushed": 0,
  "render": 0
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» count|integer|true|none||none|
|» data|[object]|true|none||none|
|»» id|integer|true|none||none|
|»» updated_at|string|true|none||none|
|»» task_id|integer|true|none||none|
|»» tid|string|true|none||none|
|»» bundle|string|true|none||none|
|»» uid|string|true|none||none|
|»» imei|string|true|none||none|
|»» alias|string|true|none||none|
|»» phone|string|true|none||none|
|»» push_type|string|true|none||none|
|»» success|integer|true|none||none|
|»» message|string|true|none||none|
|» expect_pushed|integer|true|none||none|
|» had_pushed|integer|true|none||none|
|» render|integer|true|none||none|

## POST 消息撤回

POST /mb_api/pushmsg/hulk/v1/task/rollback

> Body 请求参数

```json
{
  "reqid": "44333264-fd03-11ec-a605-00163e017386",
  "titla": "消息已被撤回",
  "tid": [
    "27c9e72716f3b11d05879bf35ba44cee"
  ]
}
```

### 请求参数

|名称|位置|类型|必选|说明|
|---|---|---|---|---|
|body|body|object| 否 |none|
|» titla|body|string| 否 |撤回的消息标题, iOS实现的是当前标题覆盖上一条消息|
|» tid|body|[string]| 否 |指定tid列表|
|» reqid|body|string| 是 |任务reqid|

> 返回示例

> 200 Response

```json
{
  "req_id": "string"
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» req_id|string|true|none||none|

## POST 推送(全局&群组)

POST /mb_api/pushmsg/hulk/v1/universal/{type_subtype}/{appid}/full

> Body 请求参数

```json
{
  "title": "照八省主百",
  "alert": "之算业广置据矿金说划消物可老管它。",
  "intent": {
    "url": "http://oddpoffbxc.se/qikplef"
  },
  "extras": "pariatur",
  "small_icon_url": "https://s1.ax1x.com/2022/09/02/vIMHyt.png",
  "sms": {
    "template": "名去铁花加即干经接各史价少变最区。",
    "params": "tempor ea"
  },
  "vibrate": 0,
  "voice": 0,
  "created_at": [
    "2022-06-06T16:48:57+08:00",
    "2022-06-09T16:48:57+08:00"
  ],
  "updated_at": [
    "2022-06-06T16:48:57+08:00",
    "2022-06-09T16:48:57+08:00"
  ],
  "system_versions": [],
  "uids": [],
  "tids": [],
  "alias": [],
  "locations": [],
  "phones": [],
  "platform": []
}
```

### 请求参数

|名称|位置|类型|必选|说明|
|---|---|---|---|---|
|type_subtype|path|string| 是 |none|
|appid|path|string| 是 |none|
|push-channels|header|string| 否 |none|
|body|body|object| 否 |none|
|» title|body|string| 是 |none|
|» alert|body|string| 是 |none|
|» intent|body|object| 是 |none|
|»» url|body|string| 是 |none|
|» extras|body|string| 是 |none|
|» sms|body|object| 否 |短信|
|»» template|body|string| 是 |短信模板code|
|»» params|body|string| 是 |短息模板参数|
|» vibrate|body|integer| 否 |振动：0=关闭，1=开启|
|» voice|body|integer| 否 |声音：0=关闭，1=开启|
|» created_at|body|[string]| 否 |注册时间段|
|» updated_at|body|[string]| 否 |活跃时间段|
|» system_versions|body|[string]| 否 |系统版本(string类型非int类型): ["10", "11"]|
|» uids|body|[string]| 否 |uid组|
|» tids|body|[string]| 否 |tid组|
|» alias|body|[string]| 否 |别名组|
|» locations|body|[string]| 否 |区域：028=成都|
|» phones|body|[string]| 否 |手机号组：[130xxxxxxxx]|
|» platform|body|[string]| 否 |平台组:["ios", "android"]|
|» small_icon_url|body|string| 是 |右侧小图片|
|» wechat|body|object| 否 |微信推送|
|»» template_id|body|string| 是 |模板ID|
|»» client_msg_id|body|string| 否 |防重入id|
|»» data|body|object| 是 |模板参数|
|»» url|body|string| 否 |模板跳转链接|
|»» miniprogram|body|string| 否 |跳小程序所需数据|
|» full|body|boolean| 是 |是否为全量推送|

> 返回示例

> 200 Response

```json
{
  "req_id": "string"
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» req_id|string|true|none||none|

## GET 详情列表

GET /mb_api/pushmsg/hulk/v1/task/detail/v2

### 请求参数

|名称|位置|类型|必选|说明|
|---|---|---|---|---|
|offset|query|integer| 否 |none|
|size|query|integer| 否 |none|
|req_id|query|string| 否 |none|

> 返回示例

> 成功

```json
{
  "code": 0,
  "message": "ok",
  "extend": null,
  "data": [
    {
      "id": 267307,
      "created_at": "2023-02-08T16:27:31.22+08:00",
      "updated_at": "2023-02-08T16:27:31.451+08:00",
      "req_id": "6e0fa757-a78a-11ed-87f6-00163e017386",
      "push_body": "{\"app\":null,\"sms\":{\"template\":\"SMS_253460031\",\"params\":\"{\\\"key1\\\":\\\"xxx\\\",\\\"key2\\\":\\\"100\\\"key3\\\":\\\"xxx\\\"}\"},\"wechat\":null,\"email\":null}",
      "push_count": 1,
      "Render": 0,
      "progress": "done",
      "exp_at": 61675844851,
      "app_id": "hulk4015d",
      "channels": "spush",
      "tmsn": "t7s2",
      "task_detail": [
        {
          "id": 11326,
          "updated_at": "2023-02-08T16:27:31.234+08:00",
          "task_id": 267307,
          "uid": "123456",
          "bundle": "hulk4015d",
          "device_type": "phone",
          "msg_id": "6e0fa757-a78a-11ed-87f6-00163e017386",
          "push_type": "unknown",
          "message": "{\"code\":10000,\"message\":\"user does not exist\",\"extend\":null}",
          "success": 0
        }
      ]
    }
  ]
}
```

```json
{
  "count": 0,
  "data": [],
  "expect_pushed": 0,
  "had_pushed": 0,
  "render": 0
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» code|integer|true|none||none|
|» message|string|true|none||none|
|» extend|null|true|none||none|
|» data|[object]|true|none||none|
|»» id|integer|false|none||none|
|»» created_at|string|false|none||none|
|»» updated_at|string|false|none||none|
|»» req_id|string|false|none||none|
|»» push_body|string|false|none||none|
|»» push_count|integer|false|none||none|
|»» Render|integer|false|none||none|
|»» progress|string|false|none||none|
|»» exp_at|integer|false|none||none|
|»» app_id|string|false|none||none|
|»» channels|string|false|none||none|
|»» tmsn|string|false|none||none|
|»» task_detail|[object]|false|none||none|
|»»» id|integer|false|none||none|
|»»» updated_at|string|false|none||none|
|»»» task_id|integer|false|none||none|
|»»» uid|string|false|none||none|
|»»» bundle|string|false|none||none|
|»»» device_type|string|false|none||none|
|»»» msg_id|string|false|none||none|
|»»» push_type|string|false|none||none|
|»»» message|string|false|none||none|
|»»» success|integer|false|none||none|

## GET 推送统计

GET /mb_api/pushmsg/hulk/v1/task/push_count/{req_id}

### 请求参数

|名称|位置|类型|必选|说明|
|---|---|---|---|---|
|req_id|path|string| 是 |推送任务的reqid|

> 返回示例

> 成功

```json
{
  "code": 2,
  "message": "Fail",
  "extend": "任务不存在: record not found"
}
```

```json
{
  "code": 0,
  "message": "",
  "extend": null,
  "data": {
    "wechat": {
      "// 微信渠道 \"Estimate\"": 1,
      "// 预计发送量 \"Actual\"": "0 // 实际发送量"
    },
    "thanos": {
      "// app推送渠道 \"Estimate\"": 1,
      "Actual": 0
    },
    "spush": {
      "// 短信渠道 \"Estimate\"": 1,
      "Actual": 0
    },
    "email": {
      "// 邮箱渠道 \"Estimate\"": 1,
      "Actual": 0
    }
  }
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» code|integer|true|none||none|
|» message|string|true|none||none|
|» extend|null|false|none||none|
|» data|object¦null|false|none||none|
|»» wechat|object|false|none||微信渠道|
|»»» Estimate|integer|true|none||预计发送量|
|»»» Actual|integer|true|none||实际发送量|
|»» thanos|object|false|none||app推送渠道|
|»»» Estimate|integer|true|none||预计推送量|
|»»» Actual|integer|true|none||实际推送量|
|»» spush|object|false|none||短信渠道|
|»»» Estimate|integer|true|none||none|
|»»» Actual|integer|true|none||none|
|»» email|object|false|none||邮箱渠道|
|»»» Estimate|integer|true|none||none|
|»»» Actual|integer|true|none||none|

## POST 推送 v2

POST /mb_api/pushmsg/hulk/v2/universal/{type_subtype}/{appid}

> Body 请求参数

```json
{
  "app": {
    "title": "太保使",
    "alert": "ut",
    "intent": {
      "url": "http://dyl.gf/pjppocdp"
    },
    "extras": "aliqua officia nisi",
    "small_icon_url": "http://dummyimage.com/100x100",
    "full": true,
    "voice": 15,
    "vibrate": 64,
    "category": {
      "hpush": "culpa ipsum nulla minim officia",
      "xiaomi": "aute ad adipisicing sint id"
    },
    "exp_at": 2
  },
  "strategy": [
    {
      "push_channel": [
        "thanos",
        "wechat"
      ],
      "where": "and"
    }
  ],
  "query": {
    "uids": [
      "123123"
    ],
    "tids": [
      "21",
      "35"
    ],
    "updated_at": [
      "2011-05-26 07:06:25",
      "2020-03-03 19:20:50",
      "1995-01-31 15:28:02"
    ],
    "alias": [
      "veniam fugiat consequat velit nostrud"
    ],
    "locations": [
      "fugiat sint",
      "magna exercitation dolor",
      "aliqua"
    ],
    "phones": [
      "18613840537",
      "13373761634",
      "18126739157"
    ],
    "system_versions": [
      "qui"
    ],
    "platform": [
      "ex sint",
      "id fugiat quis ex in"
    ],
    "created_at": [
      "1996-12-16 18:09:23"
    ]
  },
  "email": {
    "title": "的八果交务各",
    "content": "sed Lorem"
  },
  "wechat": {
    "data": {},
    "url": "http://ngfx.cu/idkwmryyz",
    "template_id": "19",
    "miniprogram": {
      "appid": "72",
      "pagepath": "officia"
    },
    "client_msg_id": "74"
  },
  "sms": {
    "template": "deserunt dolore irure fugiat pariatur",
    "params": "ut veniam Excepteur mollit culpa"
  }
}
```

### 请求参数

|名称|位置|类型|必选|说明|
|---|---|---|---|---|
|type_subtype|path|string| 是 |none|
|appid|path|string| 是 |none|
|body|body|object| 否 |none|
|» app|body|object| 是 |app推送|
|»» title|body|string| 是 |none|
|»» alert|body|string| 是 |none|
|»» intent|body|object| 是 |none|
|»»» url|body|string| 是 |none|
|»» extras|body|string| 是 |none|
|»» small_icon_url|body|string| 是 |none|
|»» full|body|boolean| 是 |none|
|»» voice|body|integer| 是 |none|
|»» vibrate|body|integer| 是 |none|
|»» category|body|object| 是 |消息分类规则|
|»»» hpush|body|string| 是 |华为渠道规则|
|»»» xiaomi|body|string| 是 |小米渠道规则|
|»» exp_at|body|integer| 是 |过期时间|
|»» cycle|body|boolean| 是 |none|
|» strategy|body|[object]| 是 |推送策略|
|»» push_channel|body|[string]| 是 |当前步骤并行推送渠道列表|
|»» care_channel|body|[string]| 是 |关注上一步骤的渠道列表|
|»» where|body|string| 是 |上一步骤用户筛选条件是“and”还是“or”|
|» query|body|object| 是 |none|
|»» uids|body|[string]| 是 |uid组|
|»» tids|body|[string]| 是 |tid组|
|»» updated_at|body|[string]| 是 |活跃时间段|
|»» alias|body|[string]| 是 |别名组|
|»» locations|body|[string]| 是 |区域：028=成都|
|»» phones|body|[string]| 是 |手机号组：[130xxxxxxxx]|
|»» system_versions|body|[string]| 是 |系统版本(string类型非int类型): ["10", "11"]|
|»» platform|body|[string]| 是 |平台组:["ios", "android"]|
|»» created_at|body|[string]| 是 |注册时间段|
|» email|body|object| 是 |邮箱推送|
|»» title|body|string| 是 |none|
|»» content|body|string| 是 |none|
|» wechat|body|object| 是 |微信推送|
|»» data|body|object| 是 |模板参数|
|»» url|body|string| 是 |模板跳转链接|
|»» template_id|body|string| 是 |模板ID|
|»» miniprogram|body|object| 是 |跳小程序所需数据|
|»»» appid|body|string| 是 |所需跳转到的小程序appid（该小程序 appid|
|»»» pagepath|body|string| 是 |所需跳转到小程序的具体页面路径，支持带参数,（示例index?foo=bar）|
|»» client_msg_id|body|string| 是 |防重入id|
|» sms|body|object| 是 |短信推送|
|»» template|body|string| 是 |短信模板code|
|»» params|body|string| 是 |短息模板参数|

> 返回示例

> 成功

```json
{
  "code": 0,
  "message": "",
  "extend": null,
  "data": {
    "req_id": "71034a0d-8048-11ed-ab0f-00163e017386"
  }
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» code|integer|true|none||none|
|» message|string|true|none||none|
|» extend|null|true|none||none|
|» data|object|true|none||none|
|»» req_id|string|true|none||none|

# dashboard

## GET 注册

GET /mb_api/pushmsg/hulk/v1/dashboard/login

### 请求参数

|名称|位置|类型|必选|说明|
|---|---|---|---|---|
|bundle|query|string| 是 |none|
|platform|query|string| 否 |none|
|end|query|string| 否 |none|
|start|query|string| 否 |none|

> 返回示例

> 200 Response

```json
{}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|Inline|

### 返回数据结构

## GET 活跃

GET /mb_api/pushmsg/hulk/v1/dashboard/active

### 请求参数

|名称|位置|类型|必选|说明|
|---|---|---|---|---|
|bundle|query|string| 是 |none|
|platform|query|string| 否 |none|
|end|query|string| 否 |none|
|start|query|string| 否 |none|

> 返回示例

> 200 Response

```json
{}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|Inline|

### 返回数据结构

## GET 推送

GET /mb_api/pushmsg/hulk/v1/dashboard/push

### 请求参数

|名称|位置|类型|必选|说明|
|---|---|---|---|---|
|bundle|query|string| 是 |none|
|platform|query|string| 否 |none|
|end|query|string| 否 |none|
|start|query|string| 否 |none|

> 返回示例

> 200 Response

```json
{}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|Inline|

### 返回数据结构

## GET 城市

GET /mb_api/pushmsg/hulk/v1/dashboard/city

### 请求参数

|名称|位置|类型|必选|说明|
|---|---|---|---|---|
|bundle|query|string| 是 |none|
|platform|query|string| 否 |none|
|end|query|string| 否 |none|
|start|query|string| 否 |none|

> 返回示例

> 200 Response

```json
{}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|Inline|

### 返回数据结构

## GET 用户和推送累计

GET /mb_api/pushmsg/hulk/v1/dashboard/userAndTaskCount

> 返回示例

> 200 Response

```json
{
  "user": 0,
  "send": 0
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» user|integer|true|none||用户累计总数|
|» send|integer|true|none||推送累计总数|

# 数据模型

