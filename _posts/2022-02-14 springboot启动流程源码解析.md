---
layout: post
title: springboot启动流程源码解析
description: springboot启动流程
tag: springboot
---

## 1.

### java基本数据类型和其包装类

想知道int和Integer的区别，首先我们得搞清楚基本数据类型和其包装类的一个关系.学过java的人都知道，java是一个面向对象的编程语言，但是为了平常编写程序的方便，

java引入8种基本的数据类型：int,short,long,char,boolean,byte,float,double,但是为了更好的使用对象，java引入每种对应的包装类，在java1.5开始引入了自动装箱和拆箱机制，使其二者可以相互的转换。

### 何为自动装箱何拆向机制

自动装箱就是Java自动将原始类型值转换成对应的对象，比如将int的变量转换成Integer对象，这个过程叫做装箱，反之将Integer对象转换成int类型值，这个过程叫做拆箱。

<!--例如我们有一个integer对象的集合，添加的参数为原始数据类型，则java会将其转换成对应的包装类在进行添加-->

```java
        List<Integer> list = new ArrayList();
		list.add(1);//会将原始类型数据装箱为Integer包装类
		int num = list.get(0);//此时会将去出的intger包装类拆箱为int
```

在java1.5之前需要手动去转换

```java
        Integer object = Integer.valueOf(3);
		int n = object.intValue();
```

这种机制也有一个弊端，当我们用包装类来进行循环时，会额外创建不必要的对象，会影响运行速率

```java
        Integer i =0;
		for (int j = 0; j < args.length; j++) {
			i+=j;//由于包装类i不适合+运算符，会将i拆箱后进行+运算后，在装箱。
		}
        //每次循环都会经历如下过程,创建额外的对象
        int result = i.intValue()+j;
        Integer i = new Integer(result);
```

知道这些后在通过如下代码，你就能明白int何Integer之间的区别

```java
public class Intdata {
	public static void main(String[] args) {
		Integer i = new Integer(3);
		Integer j = 3;
		System.out.println(i==j);//值为false,由于给j赋值时，会将3转换成包装类，相当于new了一新对象
		int k = 3;
		System.out.println(i==k);//i何k比较时，i会先拆箱，最后进行的值比较
	}
}
```
