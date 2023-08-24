---
layout: post
title: 找不到bean  ‘mvcContentNegotiationManager’错误
categories: Java
description: 找不到bean  ‘mvcContentNegotiationManager’错误
keywords: Java
typora-root-url: ..
---

在使用smm框架时，启动tomcat，在浏览器中打开html页面，遇到这个错误
```Java
org.springframework.beans.factory.BeanCreationException: Error creating bean with name ‘mvcContentNegotiationManager’

```
网上有搜到解决方法：
1. 缺少servlet.spi，补上该jar包
2. 注释掉以下代码
```Java
    <mvc:annotation-driven />

```

我有servlet.api这个包，使用第二个方法注释掉那段代码也不行。
最后发现，我的文件目录中多了lib目录，把lib删去即可
以下是我的文件目录（已删去lib目录）----------目前并不明白为什么会这样
![image.png](/images/posts/can-not-find-beanmvccontentnegotiationmanager/image-bce9901d98d644a9a4e43052bb45c1b4.png)


