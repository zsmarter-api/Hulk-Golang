# 部署文档

### 依赖以下中间件

| 名称            | 用途        |
|---------------|-----------|
| Redis         | 	数据缓存     |
| DB（MySQL/达梦）  | 	数据存储     |
| Kafka	        | 消息队列      |
| InfluxDB      | 	数据收集     |
| Etcd	         | 配置中心，数据同步 |
| ZooKeeper	    | 服务注册中心    |
| ElasticSearch | 	错误日志记录   |

### 运行 push 相关的服务

```shell
$ ./bin/hulk_xxx --help
Usage of ./bin/hulk_xxx:
-c string config file
-v bool   show version

$ ./bin/hulk_xxx -c ./conf/hulk_xxx.toml
```

### 运行 ZTP 协议相关的服务

```shell
$ ./bin/thanos_xxx --help
Usage of ./bin/thanos_xxx:
-c string config file
-v bool   show version

$ ./bin/thanos_xxx -c ./conf/thanos_xxx.toml
```
