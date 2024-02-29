---
layout: fragment
title: BufferedReader和BufferedWriter同时使用会清空文件
tags: Java
description: BufferedReader和BufferedWriter同时使用会清空文件
keywords: Java BufferedReader BufferedWriter
typora-root-url: ..
---

﻿比如这样使用
![在这里插入图片描述](/images/posts/BufferedReader-BufferedWriter/20201113114433399.png)
会清空文件内容，读的时候文件是没有数据的

原因：读写是互斥的，读的时候已经打开了文件，写的时候就不能打开了

解决方法
![在这里插入图片描述](/images/posts/BufferedReader-BufferedWriter/2020111311502049.png)
![在这里插入图片描述](/images/posts/BufferedReader-BufferedWriter/20201113115036449.png)
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIwNTUzOTA1MjJdfQ==
-->