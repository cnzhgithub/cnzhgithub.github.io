---
layout: post
title: springboot
description: springBoot详解
tag: spring
---

#### 1.springboot 官方详解

```
用来简化spring应用的初始搭建以及开发过程。
以往搭建spring的应用，需要引用大量的配置，和引入依赖。而spring boot引入了stater的概念，由stater自己去引入依赖，并使用默认配置
```

- 创建一个Bean
- 创建一个Bean所依赖的类
- 需要能够执行和初始化和销毁方法

#### 2.springboot 核心

```
核心机制为stater,利用pom文件的继承机制来实现的
预定义依赖包版本+根据应用场景，抽取依赖包，并封装，利用pom的传递依赖，完成完整的依赖包引入，分为三个过程(springboot依赖版本管理、spring boot启动器、spring boot启动过程)
```

#### 3.依赖版本管理

```
 <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId> 指向spring-boot-dependencies
        <version>2.3.0.RELEASE</version>
        <relativePath/> <!-- lookup parent from repository -->
    </parent>
    
 <parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-dependencies</artifactId>
    <version>2.3.0.RELEASE</version>
  </parent>
 spring-boot-dependencies 包含几乎所有常用的jar包 
```

#### 4.springboot 启动器

```
<dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter</artifactId>
        <version>${spring-boot.version}</version>
</dependency>
spring-boot-starter这个就是springboot的启动器
spring-boot-starter-名称来引入适合各种场景的依赖
```

#### 5.springboot启动过程

- ## @SpringBootConfiguration

```
根据Javadoc可知，该注解作用就是将当前的类作为一个JavaConfig，然后触发注解@EnableAutoConfiguration和@ComponentScan的处理，本质上与@Configuration注解没有区别。
```

- ## @ComponentScan

```
扫描的 Spring 对应的组件，如 @Componet，@Repository。
```

- ## @EnableAutoConfiguration

```
将扫描到的类装载到容器中
```

#### 