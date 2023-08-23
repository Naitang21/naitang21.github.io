---
layout: post
title: 比赛中的配对次数
categories: leetcode
description: 比赛中的配对次数--力扣题解
keywords: leetcode
typora-root-url: ..
---

题目描述：
给你一个整数 n ，表示比赛中的队伍数。比赛遵循一种独特的赛制：

如果当前队伍数是 偶数 ，那么每支队伍都会与另一支队伍配对。总共进行 n / 2 场比赛，且产生 n / 2 支队伍进入下一轮。
如果当前队伍数为 奇数 ，那么将会随机轮空并晋级一支队伍，其余的队伍配对。总共进行 (n - 1) / 2 场比赛，且产生 (n - 1) / 2 + 1 支队伍进入下一轮。
返回在比赛中进行的配对次数，直到决出获胜队伍为止。

![img](/images/posts/2023-08-22-The-number-of-pairs-in-the-match/3a6c2531874242ec81aafeca86d7017e.png)
方法一：
把n分奇偶讨论

```java
public int numberOfMatches(int n) {
        int count = 0;
        int num = n;
        while (num!=1){
            if (num%2==0){
                num=num/2;
                count=count+num;
            }else {
                num=(num-1)/2;
                count=count+num+1;

            }
        }
        return count;
```

分析：
时间复杂度：O（logn）
空间复杂度：O（1）

方法二:
因为每比赛一次，就会淘汰一只队伍，最后只剩下一只队伍，那必然比赛了n-1次
，即配对了n-1次

```java
public int numberOfMatches(int n) {
        return n-1;
    }
```



