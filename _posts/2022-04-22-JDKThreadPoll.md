---
layout: post
title: 线程池
description: jdk-线程池
tag: java
---

## 1.ThreadPoolExecutor

```
此为JDK自带线程池
构建参数
corePoolSize：核心线程-默认不会销毁，可通过allowCoreThreadTimeOut这个属性设置
maximumPoolSize：最大的线程数
keepAliveTime:线程存活时间-空闲时间
TimeUnit:时间单位
BlockingQueue<Runnable>:缓存任务对列
```

### 2.缓存任务队列

#### 2.1 SynchronousQueue

```
特点：该队列不会暂存任务。所以没有空闲线程是机会立马创建一个新的线程来处理任务
```

#### 2.2 LinkedBlockingDeque

```
特点:大小为Integer.MAX_VALUE,有新任务进来时，会在该队列中暂存
```

#### 2.3ArrayBlockingQueue

```
特点：需要指定大小，新提交任务时，会先判断队列容量是否已满。没满则暂存到队列中，否则新建一个工作线程来处理，且先进先出
```

#### 2.4 PriorityBlockingQueue

```
特点:是一个按照优先级进行内部元素排序的无界阻塞队列。队列中的元素必须实现 Comparable 接口，这样才能通过实现compareTo()方法进行排序。优先级最高的元素将始终排在队列的头部；PriorityBlockingQueue 不会保证优先级一样的元素的排序。
```

### 3.拒绝策略

![1652065659603](C:\Users\zh\AppData\Roaming\Typora\typora-user-images\1652065659603.png)

