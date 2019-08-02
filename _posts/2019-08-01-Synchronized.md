---
layout: post
title: Synchronized 和 volatile
description: java关键字Synchronized he volation介绍
tag: javase
---

# java关键字Synchronized 和 volatile

### 前提我们得搞清楚三个性质

##### 可见性:

​       可见性，是指线程之间的可见性，一个线程修改的状态对另一个线程是可见的。也就是一个线程修改的结果。另一个线程马上就能看到。比如：用volatile修饰的变量，就会具有可见性。volatile修饰的变量不允许线程内部缓存和重排序，即直接修改内存。所以对其他线程是可见的。

##### 原子性:

​        可以简单的理解为是不能被分割的，例如:int  a = 0;这个操作不能被分割，具有原子性，这个操作被称为原子操作。例如:a++;实际操作是a=a+1;是可分割的，所以他不是一个原子操作。非原子操作都会存在线程安全问题，需要我们使用同步技术（sychronized）来让它变成一个原子操作。非原子操作不能包装线程安全。

##### 有序性

​         Java语言提供了volatile和synchronized两个关键字来保证线程之间操作的有序性，volatile是因为其本身包含“禁止指令重排序”的语义，synchronized是由“一个变量在同一个时刻只允许一条线程对其进行lock操作”这条规则获得的，此规则决定了持有同一个对象锁的两个同步块只能串行执行。

### Synchronized

### **用法**

​    **synchronized可以用了修饰一个普通方法，或者代码块**，这个时候synchronized锁定的是当前对象，只要有一个线程在访问对应的方法或代码块，其他线程必须等待。

​    **synchronized只对修饰的方法有效**，锁定对象的其他非synchronized方法还是可以访问的

​    **synchronized也可以用来锁定指定对象**，当一个线程访问指定对象时，其他试图访问指定对象的线程将会阻塞，直到该线程访问指定对象结束

​    **synchronized可以用了修饰一个静态方法**，静态方法是属于类的而不属于对象的。同样的，synchronized修饰的静态方法锁定的是这个类的所有对象

​    **synchronized(*.class)效果跟锁定静态方法相同，都是锁定这个类的所有对象**。

​    **注意**:实现同步是要很大的系统开销作为代价的，甚至可能造成死锁，所以尽量避免无谓的同步控制。

#### 实现原理:

1. 依赖 `JVM` 实现同步
2. 底层通过一个监视器对象`（monitor）`完成， `wait（）`、`notify（）` 等方法也依赖于 monitor 对象

####  synchronized代码案例

```java
 public class Test{ 
    // 对象锁：形式1(方法锁) 
    public synchronized void Method1(){ 
        System.out.println("我是对象锁也是方法锁"); 
        try{ 
            Thread.sleep(500); 
        } catch (InterruptedException e){ 
            e.printStackTrace(); 
        } 
 
    } 
 
    // 对象锁：形式2（代码块形式） 
    public void Method2(){ 
        synchronized (this){ 
            System.out.println("我是对象锁"); 
            try{ 
                Thread.sleep(500); 
            } catch (InterruptedException e){ 
                e.printStackTrace(); 
            } 
        } 
 
    } 
 ｝
/**
 * 类锁
 */
public class Test{ 
　　 // 类锁：形式1 ：锁静态方法
    public static synchronized void Method1(){ 
        System.out.println("我是类锁一号"); 
        try{ 
            Thread.sleep(500); 
        } catch (InterruptedException e){ 
            e.printStackTrace(); 
        } 
 
    } 
 
    // 类锁：形式2 ：锁静态代码块
    public void Method2(){ 
        synchronized (Test.class){ 
            System.out.println("我是类锁二号"); 
            try{ 
                Thread.sleep(500); 
            } catch (InterruptedException e){ 
                e.printStackTrace(); 
            } 
 
        } 
 
    } 
｝
```



### volatile

​       Java语言提供了一种稍弱的同步机制，即volatile变量，用来确保将变量的更新操作通知到其他线程。当把变量声明为volatile类型后，编译器与运行时都会注意到这个变量是共享的，因此不会将该变量上的操作与其他内存操作一起重排序。volatile变量不会被缓存在寄存器或者对其他处理器不可见的地方，因此在读取volatile类型的变量时总会返回最新写入的值。

　当对非 volatile 变量进行读写的时候，每个线程先从内存拷贝变量到CPU缓存中。如果计算机有多个CPU，每个线程可能在不同的CPU上被处理，这意味着每个线程可以拷贝到不同的 CPU cache 中。

![](C:\Users\zh\Desktop\volatile.png)

　　而声明变量是 volatile 的，JVM 保证了每次读变量都从内存中读，跳过 CPU cache 这一步。

需要注意的是volatile只能保证变量的原子性，但不能保证对变量操作的原子性

```java
public class Volatiletest extends Thread{
	//public static volatile boolean flag = false;//不用该关键字此程序无限循环
	public static boolean flag = false;//用此关键字，会跳出循环

	@Override
	public void run() {
		// TODO Auto-generated method stub
		while(!flag) {
			
		}
	}
	
	public static void main(String[] args) throws InterruptedException {
		new Volatiletest().start();
		Thread.sleep(2000);
		flag = true;
	}
```

