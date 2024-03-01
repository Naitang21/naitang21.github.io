---
layout: fragment
title: Annotation-specified bean name xxx for bean class conflicts with existing
tags: Java Bug
description: Annotation-specified bean name xxx for bean class conflicts with existing
keywords: Java Bug
typora-root-url: ..
---

启动项目时，出现以下错误：
```
Failed to parse configuration class [xxx]; nested exception is org.springframework.context.annotation.ConflictingBeanDefinitionException: Annotation-specified bean name 'xxx' for bean class [xxx] conflicts with existing, non-compatible bean definition of same name and class [xxx]
```

根据错误信息可以知道，是因为有两个相同的Bean冲突了，程序不知道该使用哪一个Bean。根据错误信息可以找到冲突的两个Bean的位置。
但是我在jia
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEyMjM3MDYyNDBdfQ==
-->