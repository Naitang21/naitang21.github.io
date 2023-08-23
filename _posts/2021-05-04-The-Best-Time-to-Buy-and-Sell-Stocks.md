---
layout: post
title: 买卖股票的最好时机
categories: leetcode
description: 买卖股票的最好时机--力扣题解
keywords: leetcode
typora-root-url: ..
---

﻿题目描述：
给定一个数组 prices ，它的第 i 个元素 prices[i] 表示一支给定股票第 i 天的价格。

你只能选择 某一天 买入这只股票，并选择在 未来的某一个不同的日子 卖出该股票。设计一个算法来计算你所能获取的最大利润。

返回你可以从这笔交易中获取的最大利润。如果你不能获取任何利润，返回 0 。

![img](/images/posts/The-Best-Time-to-Buy-and-Sell-Stocks/8fd82aaba3c24d6e9de2edc0290f51d7.png)

**方法一：暴力法**
这是我想到的第一个思路
使用两个for循环，遍历数组的每一个元素，对于元素 i ，再依次遍历该元素后面的每一个元素，找出最大差值

```java
class Solution {
    public int maxProfit(int[] prices) {
        int profit = 0;
        for (int i=0;i<prices.length;i++){
            for (int j=i+1;j<prices.length;j++){
// 有利润，可以卖出

                    if (prices[j]-prices[i]>profit){
                        profit = prices[j]-prices[i];
                    }
                
            }
        }

        return profit;
    }
}
```

但是在力扣的测试中，这个方法不能通过，原因是：超出时间限制
有一些测试用例的数组元素很多，所以超出了时间限制

分析：
这种方法需要两个for循环
时间复杂度：O（n<sup>2</sup>）
空间复杂度：O（1）



**方法二：**
因为方法一中，执行次数太多导致查出时间限制，因此要想办法减少执行次数
一次遍历数组，记录最小元素，也就是股票价格最低点，计算每一个元素和最小元素的差值，求最大的差值

```java
class Solution {
    public int maxProfit(int[] prices) {
            int profit = 0;
        int minPrice = prices[0];
        for (int i=0;i<prices.length;i++){
            if (prices[i]<minPrice){
                minPrice = prices[i];
            }
            else if (prices[i]-minPrice>profit){
                profit = prices[i]-minPrice;
            }
        }
        return profit;
    }
}
```
分析：
这种方法只需要遍历一次数组
时间复杂度：O（n）
空间复杂度：O（1）

方法三：
这是在评论区看到的一个方法，状态定义方法（来自力扣的DUNCAN用户）

```java
class Solution {
    public int maxProfit(int[] prices) {
        int len = prices.length;
        int res = 0;
        // 前一天卖出可以获得的最大利润
        int pre = 0;
        for (int i = 1; i < len; i++) {
            // 利润差
            int diff = prices[i] - prices[i - 1];
           // 状态转移方程：第i天卖出可以获得的最大利润 = 第i-1天卖出的最大利润 + 利润差
            pre = Math.max(pre + diff, 0);
            res = Math.max(res, pre);
        }
        return res;
    }
}
```