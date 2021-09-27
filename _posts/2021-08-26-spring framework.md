---
layout: post
title: spring framework
description: spring、springBoot、springCloud区别
tag: spring
---

#### 1.依赖注入

```
管理bean对象，将对象的创建和初始化交给容器管理(实现以下三个功能)
```

- 创建一个Bean
- 创建一个Bean所依赖的类
- 需要能够执行和初始化和销毁方法

#### 2.依赖关系的建立

```
xml和注解两种方式(转换成spring能够识别的数据结构)
```

- xml：通过xml文件配置的方式
- 注解：通过@Autowired等注解实现

#### 3.触发依赖注入的时间

```
spring容器启动初始化的时候（所有单例非懒加载的Bean）
第一次进行懒加载的时候
```

#### 4.事务管理

```
实现数据ACID
```

- **原子性(Atomicity)**：事务是一个不可分割的工作单位，事务中的操作要么都发生，要么都不发生
- **一致性(Consistency)**：事务在完成后数据的完整性必须保持一致
- **隔离性(Isolation)**：多个用户并发访问数据库时，一个用户的事务不能被其他用户的事务所干扰，多个并发事务之间的数据要相互隔离
- **持久性（Durability）**：一个事务一旦被提交，它对数据库中数据的改变应该是永久性的，即使数据库发生故障也不应该对其有任何影响

#### 5.spring事务管理器

```
spring并没有实现事务管理功能,是通过PlatformTransactionManager事务管理器为不同的持久层框架提供了实现类
```

#### 6.实现spring事务的两种方式

```
声明式事务管理和编程式事务管理（主要介绍声明式事物三种方法）
```

- **基于TransactionProxyFactoryBean的方式**

```
<!--配置事务管理器-->
    <bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
        <property name="dataSource" ref="dataSource" />
    </bean>

    <!--配置业务层的代理,使用代理类来实现事务-->
    <bean id="transferServiceProxy" class="org.springframework.transaction.interceptor.TransactionProxyFactoryBean">
        <!--配置目标对象-->
        <property name="target" ref="Bean的名称" />
        <!--注入事务管理器-->
        <property name="transactionManager" ref="transactionManager" />
        <!--注入事务属性-->
        <property name="transactionAttributes">
            <props>
                <!--
                    prop的格式：
                        * PROPAGATION :事务的传播行为
                        * ISOLATION :事务的隔离级别
                        * readOnly :是否只读
                        * -Exception :发生哪些异常回滚事务
                        * +Exception :发生哪些异常不回滚事务
                -->
                <prop key="transfer*">PROPAGATION_REQUIRED</prop>
            </props>
        </property>
    </bean>
```

- ##### 基于AspectJ的XML方式

  ```
  <!--配置事务管理器-->
      <bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
          <property name="dataSource" ref="dataSource" />
      </bean>
  
     <!--配置事务的通知-->
      <tx:advice id="txAdvice" transaction-manager="transactionManager">
          <tx:attributes>
              <tx:method name="transfer*" propagation="REQUIRED" />
          </tx:attributes>
      </tx:advice>
  
      <!--配置切面-->
      <aop:config>
          <aop:pointcut id="pointcut1" expression="execution(* com.tx.service.impl.*ServiceImpl.*(..))" />
          <aop:advisor advice-ref="txAdvice" pointcut-ref="pointcut1" />
      </aop:config>
  ```

  

- ##### 基于注解的方式

  ```
  <!--配置事务管理器-->
      <bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
          <property name="dataSource" ref="dataSource" />
      </bean>
  
      <!--开启事务注解-->
      <tx:annotation-driven transaction-manager="transactionManager" />
  ```

#### 7.web应用

```
以mvc架构思想实现(model对象-v视图-c控制器)
```

![1629099872934](C:\Users\zh\AppData\Roaming\Typora\typora-user-images\1629099872934.png)

#### 8.数据访问