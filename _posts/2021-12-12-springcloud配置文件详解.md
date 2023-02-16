---
layout: post
title: springcloud配置文件
description: springcloud配置文件详解
tag: spring
---

## 1.BOOTSTARP.XML

```
server:
  port:访问该服务时的端口
  undertow:容器（替换默认的tomat）
    allow-unescaped-characters-in-url: true
```

### 2.application.xml

```
spring:
  application:
    name:----应用名称(自己定义)
  datasource:
    url:--数据库连接地址(IP、端口、字符集、时区等等)
    username:--用户名称
    password:--用户密码
  hikari:---连接池
    pool-name:--连接池名称(自己定义)
    minimum-idle:--最小空闲连接数量(自己定义)
    maximum-pool-size:--连接池最大连接数(默认20)
    connection-timeout: 30000 # 数据库连接超时时间,默认30秒，即30000
  cloud:
    inetutils:--回环网卡设置
      ignored-interfaces[0]: lo --忽略回环网卡(使其注册到EUREKA是真实有效的地址，不是虚拟机的地址)
      preferred-networks[0]: 10.90 --选择正确的网段
    stream:--消息队列中间件配置
      rocketmq:--具体实现类
        binder:--抽象接口
         namesrv-addr:--消息队列地址
  redis:--缓存组件
    host: --IP
    port: --端口
    database: --选择哪个库
    password：--密码
    jedis:--连接池
      pool:
        # 资源池中最大连接数
        # 默认8，-1表示无限制；可根据服务并发redis情况及服务端的支持上限调整
        max-active: ${SPRING_REDIS_POOL_MAX_ACTIVE:50}
        # 资源池运行最大空闲的连接数
        # 默认8，-1表示无限制；可根据服务并发redis情况及服务端的支持上限调整，一般建议和max-active保持一致，避免资源伸缩带来的开销
        max-idle: ${SPRING_REDIS_POOL_MAX_IDLE:50}
        # 当资源池连接用尽后，调用者的最大等待时间(单位为毫秒)
        # 默认 -1 表示永不超时，设置5秒
        max-wait: ${SPRING_REDIS_POOL_MAX_WAIT:5000}
  servlet:
    multipart:--上传文件大小的限制
feign:
  hystrix:
    enabled: true --开启FEIGN调用熔断器

hystrix:
  threadpool:
    default:
      # 执行命令线程池的核心线程数，也是命令执行的最大并发量
      # 默认10
      core-size: #${HYSTRIX_THREADPOOL_DEFAULT_CORE_SIZE:1000}
      # 最大执行线程数
      maximum-size: ${HYSTRIX_THREADPOOL_DEFAULT_MAXMUM_SIZE:1000}
  command:
    default:
      execution:
        timeout:
          enabled: true
        isolation:
          thread:--熔断时间/默认为1000毫秒
            timeoutInMilliseconds: ${HYSTRIX_COMMAND_TIMEOUT_IN_MILLISECONDS:90000}

ribbon:--设置feign调用的超时时间(小于熔断时间)
  ReadTimeout: ${RIBBON_READ_TIMEOUT:60000}
  ConnectTimeout: ${RIBBON_CONNECT_TIMEOUT:60000}
  eureka:
    enabled: ${RIBBON_EUREKA_ENABLE:true}
    

```

