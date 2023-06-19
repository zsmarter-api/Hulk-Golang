# ZTP消息数据协议

v1.0.1

[TOC]

## 1. 协议格式

协议全部使用小端模式

### 1.1 核心协议格式（ZTP）

以下协议段简称为：ZTP

| Head | Verify | Version | Type   | SubType | Ack  | Encrypt | Seq    | Reserved | DataLen | Data   |
| ---- | ------ | ------- | ------ | ------- | ---- | ------- | ------ | -------- | ------- | ------ |
| 0x7E | uint32 | uint8   | uint16 | uint16  | 4bit | 4bit    | uint16 | 16byte   | uint32  | N byte |
| 1    | 4      | 1       | 2      | 2       | 0.5  | 0.5     | 2      | 16       | 4       |        |

> **Head** : 协议头, 固定为0x7E

> **Verify** ：将Type到Data(包含)所有bytes, 采用CRC32算法(Table为IEEE 802.3)求得的uint32值

> **Version** : 协议头版本，暂时固定为0x01

> **Type** ：协议type

> **SubType** ：协议subtype

> **ACK** : 协议回复标记，0x0为无需回复;0x1需要回复;0x2为回复。

> **Encrypt** : 加密情况。0x0不加密，0x1为AES加密。

> **Seq** :  命令序列号。

> **Reserved** : 预留位，待扩展。

> **DataLen** : 标记Data的长度。Max:2^20

> **Data** : 业务数据。使用UTF-8编码的字符串。

***备注：**** *

1. 当`ACK==1` 时，必须回复`ACK=2` 的消息

2. 当`ACK==2` 时，seq为所回复信息的seq

3. 当`bytes == "crc32"` 时，`verify == 2947273566` ，以上数据用于测试crc32算法

### 1.2 例子：

A: ack = 1

Send:

```text
7e 23 2e d1 82 01 01 00 01 00 10 01 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 0c 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
```

Recv:

```text
7e b6 40 1d e6 01 01 00 02 00 10 01 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 10 00 00 00 19 cc e4 2c 09 c2 86 cd 3d a8 6a ce dd 67 55 f9
```

B: ack = 0

Send:

```text
7e 3d f7 83 62 01 02 00 01 00 00 fd ff 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
```

Recv: 不会返回

## 2. 登录

### 2.1 验证服务端

由C端主动发起，值如下：

```text
Type: 1
SubType: 1
ACK: 0
DataLen: 12
Data: 12byte的随机值
```

服务端会将C端的Data后面拼接一个SecData，然后求MD5 sum，并返回给C端

值如下：

```text
Type: 1
SubType: 2
ACK: 0
DataLen: 16
Data: md5.Sum(C端Data + SecData)
```



### 2.2 C端注册设备

C端校验md5.Sum无误后，返回给S端设备信息

值如下：

```text
Type: 1
SubType: 3
ACK: 1
```



Data为json字符串具体格式如下：

```json
{
	"device_id": "string", // 客户端唯一id，imei，最长32byte
	"bundle": "string", // app bundle id名，最长64byte
	"appkey": "string", // 分配给业务方的appkey
	"session": "string", // md5.sum(appsec+device_id)
	"platform": "string", // ios, android, wp，最长8byte
	"model": "string", // xiaomi, huawei, iphone,最长16byte
	"version": "string", // app版本，最长16byte
}
```

**注意** :

> session的计算方式为客户端将appsec和device_id两个字符串拼接后，采用md5算法计算16位长的bytes，并使用全小写16进制输出为字符串。最终session字符串长度将为32。

>

> 例如`appsec` =`abc` , `device_id` =`device_imei` 时，`session` =`900150983cd24fb0d6963f7d28e17f72`

C端收到此信息的ack，标志已经登录完成。

示例: [登录流程示意ztzh](https://www.processon.com/view/link/5cb3f93fe4b0362994d877ee)

### 2.3 C端维持心跳

完成设备注册后，C端开始心跳维持。每60s一跳。

值如下：

```text
Type: 2
SubType: 1
ACK: 0
DataLen: 0
```



## 2.4. 业务错误返回

值如下：

```text
Type: 2
SubType: 2
ACK: 0
Seq: 同接收到的seq
DataLen: N
Data: Nbyte
```

S端出错，返回给C端的数据

Data如下

```json
{
	"code": int, // 错误码
	"msg": string, // 错误提示
}
```



错误码表

| 错误码  | 释义     |
| ---- | ------ |
| 1001 | 未定义的错误 |
| 1002 | 未登录    |
| 1003 | 不支持的协议 |



## 2.5. 提交JPushID

请使用 `2.9. 提交userinfo`

## 2.6. 提交APNS ID

请使用 `2.9. 提交userinfo`

## 2.7. 提交UID

请使用 `2.9. 提交userinfo`

## 2.8. 提交phone

请使用 `2.9. 提交userinfo`

## 2.9. 提交userinfo

值如下：

```text
Type: 1
SubType: 9
DataLen: N
Data: Nbyte

```

Data: 为用户的所有属性，每个字段都为可选(填充为修改，不填充为不修改)，json结构如下

```json
{
	"device_id": "string", // 客户端唯一id，imei，最长32byte
	"uid": "string", // 用户uid，最长64byte
	"phone": "string", // 用户phone，最长11byte
	"jpush_id": "string", // 极光push_id，最长48byte
	"hw": "string", // 华为推送id，最长255
	"mi": "string", // 小米推送id，最长128
	"oppo": "string", // oppo推送id，最长64
	"vivo": "string", // vivo推送id，最长32
	"apns_id": "string", // iphone push id，最长64byte
	"token_id": "string", // token, kafka 心跳消息中会带上此值（业务视情况选择填充值）,
	"location" : "string", //地理位置，如"成都"
    "ext" : "",//扩展字段
	"u_status": 1, // 0 常用设备，1 非常用设备
}
```



**tip** : 可以用t1s9替代t1s5/6/7/8

## 3. PUSH（Type7）

### 3.1 SDK 上报消息已读给 Server Push

值如下：

```text
Type: 7
SubType: 1
```

Data数据为Json字符串，具体定义待定。

```text
{
	"m_id": "对应消息的m_id"
}
```

### 3.2 SDK 上报关闭消息给 Server Push

```text
Type: 7
SubType: 3
```

Data数据为Json字符串，具体定义待定。

```json
{
	"notification": true // true：开启通知， false：关闭通知
}
```

### 3.3 Server Push 发送信息给 Client

值如下：

```text
Type: 7
SubType: 2
```

Data数据为Json字符串，具体定义待定。

```json
{
	"alert": "Hi, ztzh!",
	"title": "Send to Android",
	"intent": {
		"url": "点击后跳转到某页面",
	},
	"m_id": task_id,
	"extras": {
		"xxx": "xxx"
	}
}
```

### 3.4 Server Push 透传信息给 Client

值如下：

```text
Type: 7
SubType: 4
```

Data 数据为 Json 字符串，具体定义待定。

```json
{
  "alert": "Hi, ztzh!",
  "title": "Send to Android",
  "intent": {
    "url": "点击后跳转到某页面"
  },
  "extras": {
    "xxx": "xxx"
  }
}
```



## 4. 包更新（Type8）

> 差异打包法 : `git diff commit-id1 commit-id2 --name-only | xargs zip update.zip`

### 4.1 Server 通知更新给 Client

值如下：

```text
Type: 8
SubType: 1
```

> **注意** 服务端会保证 inc 增量包的有序性

Data 数据为 Json 字符串，具体定义如下。

```json
{
  "module": "module.code",
  "must_update": true,
  "full": {
    "uri": "https://xxx.xxx",
    "md5": "xx",
    "ver": "xxx"
  },
  "inc": [
    {
      "uri": "https://1.zip",
      "ver": "v1",
      "md5": "xxx"
    },
    {
      "uri": "https://2.zip",
      "ver": "v2",
      "md5": "xxx"
    }
  ],
}
```

### 4.2 Client 上报当前版本

值如下：

```text
Type: 8
SubType: 2
```

Data 数据为 Json 字符串，具体定义如下。

```json
{
  "module1.code": "v1",
  "module2.code": "v2"
}
```

## 5. 日志上报（Type9）

### 5.1 客户端日志上报 (暂不接入)

> **注意** 文件大小需在 1MB 内

值如下：

```text
Type: 9
SubType: 1
Reserved：低位第 1byte 为 data 中 filename 的长度; 低位第 2byte 为 data 中 proxy_url 的长度
```

**注意** `filename`不能为空；如果 `proxy_url` 为 0，则文件转发到服务端配置的默认地址

Data 构成如下：

`filename` +`proxy_url` +`file_md5` +`file_data`

### 5.2 服务器唤起客户端日志及时上报

值如下：

```text
Type: 9
SubType: 2
```

Data 数据为 Json 字符串，具体定义由前端决定。

## 6. 同步（Type11）

### 6.1 同步数据下发

```text
Type: 11
SubType: 2
```

Data 数据为 Json 字符串，具体定义参考下述格式:

```json
{
    "persistence":"1"  //是否持久化
    "pl": {
          // 内容自定义
    },
    "key":"bizkey" // 业务方定义的key
}
```

## 7. 部署（Type12）

### 7.1 安装包更新下发

```text
Type: 12
SubType: 2
```

Data 数据为 Json 字符串，具体定义参考下述格式:

```json
{
  "title": "检测到新版本！",
  "desc": "邀请您参加内测",
  "forceUpdate": 0,
  "needUpdate": 1,
  "upgradeUrl": "http://itunes.apple.com/cn/app/id1109333848",
  "signature": "asfsbd1212"
}
```

### 7.2 客户端上报离线包信息

T12S3:客户端上报离线包版本信息：

```text
Type: 12
SubType: 3
```

Data 数据为 Json 字符串

```json
[
  {
    "module_code": "transfer",
    "module_version": "1.0.1"
  },
  {
    "module_code": "wmp",
    "module_version": "1.0.2"
  }
]
```

###  7.3 服务端下发需要更新的离线包信息

T12S4:服务端下发需要更新的离线包信息：

```text
Type: 12
SubType: 4
```

Data 数据为 Json 字符串

```json
[
  {
    "code": "paySdk",
    "version": "1.0.1",
    "is_basic": 1,
    "online_url": "http://www.baidu.com",
    "download_url": "http://cgbank.oss-cn-shenzhen.aliyuncs.com/visual/moduleZip/1606992987719.zip?Expires=1617445380&OSSAccessKeyId=LTAIRzBqOxPqCJ3i&Signature=CGo1D3rQLFpgE0l9gEEeUvMTT80%3D",
    "callback_url": "https://www.baidu.com/callback",
    "auto_install": 1,
    "datakey": "yuwZZmjb6mvwfjOVl8TNit8rYM7Il6Ez",
    "icon_url": "http://cgbank.oss-cn-shenzhen.aliyuncs.com/visual/advertisingImg/1578573765630.png",
    "main_url": "/index.html",
    "extend_info": "xxxxx",
    "need_wifi": 1
  }
]
```

### 7.4 客户端上报客户端版本

```text
Type: 12
SubType: 1
```

Data 数据为 Json 字符串，具体定义参考下述格式:

```json
{
  "ts": 1620812217000, // 客户端时间戳（毫秒）
  "dt": "1" //iOS发布渠道，1代表Appstore,2代表Inhouse
}
```

