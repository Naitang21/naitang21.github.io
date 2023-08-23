---
title: BufferedReader和BufferedWriter同时使用会清空文件--原因及解决方法.md
date: 2022-01-22 23:28:20.651
updated: 2022-01-22 23:28:20.651
url: /archives/bufferedreader和bufferedwriter同时使用会清空文件--原因及解决方法md
categories: 
tags: 
---

﻿比如这样使用
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201113114433399.png#pic_center)
会清空文件内容，读的时候文件是没有数据的

原因：读写是互斥的，读的时候已经打开了文件，写的时候就不能打开了

解决方法
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020111311502049.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3hidG50,size_16,color_FFFFFF,t_70#pic_center)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201113115036449.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3hidG50,size_16,color_FFFFFF,t_70#pic_center)