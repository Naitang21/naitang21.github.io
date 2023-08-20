---
title: 判断整数奇偶性.md
date: 2022-01-12 23:34:08.708
updated: 2022-01-12 23:34:08.708
url: /archives/判断整数奇偶性md
categories: 
tags: 
---

﻿**一：模2求余**


```java
public void judgeParity(int num){
        if (num%2==0)
            System.out.println("偶数");
        else
            System.out.println("奇数");
    }
```

**二：移位运算**

```java
public void judgeParity(int num){
        if ((num & 1)==0)
            System.out.println("偶数");
        else
            System.out.println("奇数");
    }
```