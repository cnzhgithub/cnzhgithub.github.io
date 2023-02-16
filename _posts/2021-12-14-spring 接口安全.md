---
layout: post
title: springcloud 接口安全
description: springcloud 接口RequestMapping配置
tag: spring
---

## 1.CONTENT-TYPE

```
 MediaType，即是Internet Media Type，互联网媒体类型；也叫做MIME类型，在Http协议消息头中，使用Content-Type来表示具体请求中的媒体类型信息。
```

### 2.spring mvc RequestMapping

```
@Target({ElementType.METHOD, ElementType.TYPE})
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Mapping
public @interface RequestMapping {
    String name() default ""

    @AliasFor("path") 
    String[] value() default {};

    @AliasFor("value")-----表示请求的具体路径
    String[] path() default {};

    RequestMethod[] method() default {};-----请求类型，GET,PUT,DELETE,POST

    String[] params() default {};-----请求参数，根据有无此参数来判断是否处理此请求

    String[] headers() default {};-----请求头中，必须包含的信息，否则不处理

    String[] consumes() default {};---- 指定处理请求的提交内容类型（Content-Type），例如application/json, text/html;

    String[] produces() default {};---- 指定返回的内容类型，仅当request请求头中的(Accept)类型中包含该指定类型才返回
}
```

