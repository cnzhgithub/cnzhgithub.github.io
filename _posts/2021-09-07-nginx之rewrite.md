---
layout: post
title: nginx之rewrite命令
description: rewrite
tag: nginx
---

#### 1.rewrite介绍 

```
作用：实现对URL的重写，以及重定向
场景: url访问跳转、后台维护、流量转发等
```

#### 2.rewrite规则

```
rewrite(关键字) ^/(.*)(正则表达式) 新的url 标记;
```

#### 3.正则表达式

```
常用的正则表达式
^:匹配开始
$:匹配结束
[a-z]:匹配26个小写字母的任意一个
\d:匹配数字
{n}:重复的次数
?:重复0次或一次
+:重复1次或多次
.:匹配除/的任何字符
```

#### 4.关键字flag

```
last:如果没有匹配到，继续匹配下一个
break:没有匹配到则使用当前资源，不会匹配下一个
redirect:临时重定向
permanent:永久重定向
```

