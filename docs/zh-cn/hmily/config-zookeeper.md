---
title: Hmily-Config-Zookeeper
keywords: config
description: zookeeper配置中心模式
---

### 本地配置

 * 文件名为 : `hmily.yml`。
 
 * 路径： 默认路径为项目的 `resource`目录下，也可以使用 `-Dhmily.conf` 指定，也可以把配置放在 `user.dir` 目录下。
         优先级别 `-Dhmily.conf` > `user.dir` > `resource`
         
 * 具体的全内容如下 : 注意设置 `hmily.server.configMode` = zookeeper  
 
 * 框架的或首先根据你的 `zookeeper` 配置，然后从 `zookeeper` 获取配置   

```yaml
hmily:
  server:
    configMode: zookeeper
    appName: 
  #  如果server.configMode eq local 的时候才会读取到这里的配置信息.

remote:
  zookeeper:
    serverList: 127.0.0.1:2181 #你的zookeeper服务地址，多个使用逗号分隔
    fileExtension: yml #zookeeper上配置文件的格式（properties或者yml）二选一
    path: /hmily/xiaoyu #zookeeper上配置文件的路径
    update :   #默认是false ，是否需要将本地的配置文件写到zookeeper
    updateFileName:  #update属性为true时候 ，配置文件名称，位于项目的 resource文件夹下的yaml格式
```

* 然后，你可以在上述的 `path` 配置路径下，去写入`hmily`框架所需要的配置，配置格式如果下（yml）：
```yaml
hmily:
  config:
    appName: 
    serializer: kryo
    contextTransmittalMode: threadLocal
    scheduledThreadMax: 16
    scheduledRecoveryDelay: 60
    scheduledCleanDelay: 60
    scheduledPhyDeletedDelay: 600
    scheduledInitDelay: 30
    recoverDelayTime: 60
    cleanDelayTime: 180
    limit: 200
    retryMax: 10
    bufferSize: 8192
    consumerThreads: 16
    asyncRepository: true
    autoSql: true
    phyDeleted: true
    storeDays: 3
    repository: mysql

repository:
  database:
    driverClassName: com.mysql.jdbc.Driver
    url :
    username:
    password:
    maxActive: 20
    minIdle: 10
    connectionTimeout: 30000
    idleTimeout: 600000
    maxLifetime: 1800000
  file:
    path:
    prefix: /hmily
  mongo:
    databaseName:
    url:
    userName:
    password:
  zookeeper:
    host: localhost:2181
    sessionTimeOut: 1000
    rootPath: /hmily
  redis:
    cluster: false
    sentinel: false
    clusterUrl:
    sentinelUrl:
    masterName:
    hostName:
    port:
    password:
    maxTotal: 8
    maxIdle: 8
    minIdle: 2
    maxWaitMillis: -1
    minEvictableIdleTimeMillis: 1800000
    softMinEvictableIdleTimeMillis: 1800000
    numTestsPerEvictionRun: 3
    testOnCreate: false
    testOnBorrow: false
    testOnReturn: false
    testWhileIdle: false
    timeBetweenEvictionRunsMillis: -1
    blockWhenExhausted: true
    timeOut: 1000

metrics:
  metricsName: prometheus
  host:
  port: 9091
  async: true
  threadCount : 16
  jmxConfig:
```

* 注意 `repository`的配置是SPI的扩展方式，几种方式由你去选择一种，并不需要全部配置。

* `metrics` 配置可有可无，如果不配置，则代表不开启`metrics`

 