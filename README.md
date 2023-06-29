# 项目名称
> Hulk消息推送系统为用户提供多渠道、多平台的推送服务。提供灵活、可选、组合的推送策略，满足不同场景的推送需求。消息通道稳定、消息送达高效、全球服务覆盖。


## 目录结构

```
├── bin
│   ├── hulk_consumers
│   ├── hulk_crons
│   ├── hulk_email
│   ├── hulk_group
│   ├── hulk_hpush
│   ├── hulk_ios
│   ├── hulk_jpush
│   ├── hulk_manager
│   ├── hulk_meizu
│   ├── hulk_oppo
│   ├── hulk_spush
│   ├── hulk_thanos
│   ├── hulk_vivo
│   ├── hulk_wechat
│   ├── hulk_xiaomi
│   ├── thanos_push
│   ├── thanos_register
│   └── thanos_server
├── conf
│   ├── hulk_consumers.toml
│   ├── hulk_crons.toml
│   ├── hulk_email.toml
│   ├── hulk_group.toml
│   ├── hulk_hpush.toml
│   ├── hulk_ios.toml
│   ├── hulk_manager.toml
│   ├── hulk_meizu.toml
│   ├── hulk_oppo.toml
│   ├── hulk_spush.toml
│   ├── hulk_thanos.toml
│   ├── hulk_wechat.toml
│   ├── hulk_xiaomi.toml
│   ├── thanos_push.toml
│   ├── thanos_register.toml
│   └── thanos_server.toml
├── docs
└── README.md
```

### bin 目录
> 该目录下存放的是一些可执行的二进制文件，其中以`hulk_`开头的文件问`push`相关的服务，以`thanos_`开头的是`thanos`相关的服务，包括以下内容：

- `hulk_consumers`: 队列、持续任务。
- `hulk_crons`: 定时任务。
- `hulk_email`: 邮箱推送渠道。
- `hulk_group`: 旧版全局推送。
- `hulk_hpush`: 华为推送渠道。
- `hulk_ios`: iOS推送渠道。
- `hulk_manager`: 推送网关入口。
- `hulk_meizu`: 魅族推送渠道。
- `hulk_oppo`: OPPO推送渠道。
- `hulk_spush`: 短信推送渠道。
- `hulk_thanos`: 自建推送渠道。
- `hulk_vivo`: vivo推送渠道。
- `hulk_wechat`: 微信推送渠道。
- `hulk_xiaomi`: 短信推送渠道。
- `thanos_push`: 自建渠道的消息推送服务
- `thanos_register`: 自建渠道的用户信息注册服务
- `thanos_server`: 自建渠道的socket服务

###  conf 目录
> 该目录下存放的是一些配置文件

# 运行方式
  ```shell
  bin/hulk_xxx -c config/hulk_xxx.toml
  ```

### docs 目录
> 该目录存放的是项目的文档，包括 API 文档、[文档手册](./docs/README.md)等。
