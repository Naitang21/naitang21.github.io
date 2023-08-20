---
title: 判断一个数是否为2的整数次幂.md
date: 2022-01-12 23:34:08.754
updated: 2022-01-12 23:34:08.754
url: /archives/判断一个数是否为2的整数次幂md
categories: 
tags: 
---

﻿《小灰的算法之旅》学习笔记
**题目**
判断一个正整数是否为2的整数次幂，如果是，则返回true，否则，返回false

**方法一：穷举法**

**步骤**
1. 创建一个中间变量temp，初始值为1，然后进入一个循环，每次循环都让temp乘以2，并和该整数相比较
2. 如果不相等，则让temp*2；如果temp>目标整数，则说明目标整数不是2的整数次幂；如果相等，则说明目标整数是2的整数次幂


**分析**
如果目标整数的大小为n，则此方法的时间复杂度为O(logn)


```java
public boolean exhaustively(int num){
        int temp=1;
       while (temp<=num){
           if (temp==num)
               return true;
           temp=temp*2;
       }
        return false;
    }
```

**方法二：移位法**
把方法一中，乘以2 的操作，换成移位运算

**分析**
移位的性能比乘法高，但这种方法，本质上并没有变，算法的时间复杂度依然是O（logn）
此处写出这种方法，是为了提醒自己，乘以2的操作，可以用移位运算来代替

```java
public boolean exhaustively(int num){
        int temp=1;
       while (temp<=num){
           if (temp==num)
               return true;
          temp = temp<<1;
       }
        return false;
    }
```

**方法三：位运算**
1. 当把2的整数次幂转换为二进制时，可以发现，如果一个数是2的整数次幂，那么当它转换为二进制时，它的最高位为1，其余位为0
2. 根据这个特点，可以知道，2的整数次幂和它本身减1的结果，进行位运算，的结果一定是0，反之，如果一个数不是2的整数次幂，那么结果一定不是0

**分析**
这种方法，只需要计算 num & （num-1）的结果是否为0，时间复杂度为0(1)

```java
public boolean bitOperation(int num){
        return (num & num-1) ==0;
    }
```