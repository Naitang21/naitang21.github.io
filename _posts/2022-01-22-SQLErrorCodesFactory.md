---
layout: post
title: 解决org.springframework.jdbc.support.SQLErrorCodesFactory错误
categories: Bug
description: Bug
keywords: Bug
typora-root-url: .. 
---

﻿出现org.springframework.jdbc.support.SQLErrorCodesFactory错误，是因为数据表名字，或数据段段名写错，要回去检查

错误可能的原因：

1. 参数与数据库字段不匹配，可能是映射文件sql语句写错了，字段名与数据库中的字段名不匹配。

2. 也有可能是传递的参数超过了数据库字段限定的长度。

3. 也有可能是resultMap映射字段不对。

[参考的文章](https://www.cnblogs.com/jasonboren/p/10674718.html)