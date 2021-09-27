---
layout: post
title: application和bootstrap区别
description: java全局配置文件
tag: java
---

#### 1.bootstarp.yml

```
时间:在spring cloud才会用到配置文件
条件:使用时需要引入依赖
 <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-context</artifactId>
            <version>2.1.4.RELEASE</version>
 </dependency>
 场景:当用到spring cloud config时，需要在该配置文件里定义路由信息
 创建:bootstrap.yml由父Spring ApplicationContext加载
```

#### 2.application.yml

```
主要用于 Spring Boot 项目的自动化配置。
```

#### 3.区别

```
Spring Cloud 构建于 Spring Boot 之上，在 Spring Boot 中有两种上下文，一种是 bootstrap, 另外一种是 application, bootstrap 是应用程序的父上下文，也就是说 bootstrap 加载优先于 applicaton。bootstrap 主要用于从额外的资源来加载配置信息，还可以在本地外部配置文件中解密属性。这两个上下文共用一个环境，它是任何Spring应用程序的外部属性的来源。bootstrap 里面的属性会优先加载，它们默认也不能被本地相同配置覆盖。
```

#### 4.spring boot 启动注意点

```
需要引入该jar包(内含tomcat)
<dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```
