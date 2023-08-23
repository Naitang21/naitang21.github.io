---
layout: post
title: 求最大公约数
categories: leetcode
description: 求最大公约数
keywords: leetcode
typora-root-url: ..
---

﻿@[TOC]
《小灰的算法之旅》学习笔记

# 题目：
求两个整数的最大公约数

**解决方法**

## 一 ：辗转相除法（欧几里得算法）
**定理：**
两个正整数a和b（a>b），它们的最大公约数等于a除以b的余数c和b之间的最大公约数

**步骤：**
根据以上定理，不断把两个较大的整数之间的运算，简化成两个较小整数之间的运算，直到两个数可以整除，或其中一个数减小到1为止

**分析：**
当两个整数较大时，a%b取模运算的性能会比较差,时间复杂度可近似为O(log(max(a,b)))

**举例：**
![img](/images/posts/the-max-common-divisor/e290d6292d874b4aa24262ea491904d0.png)


```java
public int rollingPhaseDivision(int a,int b){
        int max = a>b?a:b;
        int min = a>b?b:a;
        if (max%min==0)
            return min;
        return rollingPhaseDivision(max%min,min);
    }
```



## 二： 更相减损术
**原理：**
两个正整数a和b（a>b），它们的最大公约数 = a-b的差值c和较小数b的最大公约数

**步骤：**
根据以上定理，不断把两个较大的整数之间的运算，简化成两个较小整数之间的运算，直到两个数相等为止，最大公约数就是最终相等的这两个数的值

**分析：**
更相减损术是不稳定的算法，依靠两数求差的方式来递归，运算次数远大于辗转相除法的取模方式

**举例：**
![img](/images/posts/the-max-common-divisor/5ffbe5562a98432c998dc533251c7c73.png)

```java
public int modifiedSubtraction(int a,int b){
        if (a==b)
                return a;
        int max = a>b?a:b;
        int min = a>b?b:a;
        return modifiedSubtraction(max-min,min);
    }
```

## 三：在更相减损术的基础上使用移位运算
以下分析中，gcd()为求最大公约数的方法
![img](/images/posts/the-max-common-divisor/612241f82dfa4b908d4f252868048580.png)
**分析：**
这种方法在两数都较小时，可能看不出计算次数的优势，但当两数越大时，计算次数的减少就会越明显，避免了取模运算，算法性能稳定，最坏时间复杂度为O(max(a,b))

```java
//    移位运算
    public int shiftOperation(int a,int b){
        if (a==b)
            return a;
//        a b均为偶数
        if ((a&1)==0 && (b&1)==0)
            return shiftOperation(a>>1,b>>1)<<1;
//        a为偶数，b为奇数
        else if ((a&1)==0 && (b&1)!=0)
            return shiftOperation(a>>1,b);
//        a为奇数，b为偶数
        else if ((a&1)!=0 && (b&1)==0)
            return shiftOperation(a,b>>1);
//        a b为奇数
        else {
//       先更相减损一次
            int big = a>b?a:b;
            int small = a>b?b:a;
            return shiftOperation(big-small,small);
        }
    }
```