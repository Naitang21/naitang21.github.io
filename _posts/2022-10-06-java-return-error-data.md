---
layout: post
title: Java后端接口收到数据但返回error
categories: Java
description: Java后端接口收到数据但返回error
keywords: Java
typora-root-url: ..
---

有可能是后端接口返回的数据类型与前端接受的数据类型不一致。
比如我后端接口返回的是void，但是前端使用ajax中，写了
```Java
dataType:"json"
```
这个的意思是前端接受数据的类型是json
因此前后端数据类型不一致，跳到了error情况
把上面那条代码注释掉就可以了（针对后端返回void情况，如果是返回其他类型，就改成相应的类型）

**注**：在网上搜索时，也看到别的错误原因：controller层使用了@Controller，@Controller 是视图解析器的，即Return返回的是视图，即jsp或者html页面的。如果返回数据json、xml等，需要在对应的方法上加上@ResponseBody注解。

@RestController 是@Controller和@ResponseBody两个注解的结合，返回json数据不需要在方法前面加@ResponseBody注解了，但使用@RestController这个注解，就不能返回jsp,html页面，视图解析器无法解析jsp,html页面

而我使用的是@RestController 