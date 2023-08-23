---
layout: post
title: 盛最多水的容器
categories: leetcode
description: 盛最多水的容器--力扣题解
keywords: leetcode
typora-root-url: ..
---

﻿题目描述：
给你 n 个非负整数 a1，a2，...，an，每个数代表坐标中的一个点 (i, ai) 。在坐标内画 n 条垂直线，垂直线 i 的两个端点分别为 (i, ai) 和 (i, 0) 。找出其中的两条线，使得它们与 x 轴共同构成的容器可以容纳最多的水。

说明：你不能倾斜容器。

![img](/images/posts/2022-01-26-Container-for-the-most-water/e1e89e4c5cff440aa79b5264331854db.png)
**方法一：**
暴力法，两个for循环，但是这种方法会超时

```java
class Solution {
    public int maxArea(int[] height) {
         int max=0;
        for(int i=0;i< height.length;i++){
            for (int j=i+1;j< height.length;j++){
                int water = (j-i)*Math.min(height[i],height[j] );
                if (water>max)
                    max=water;
            }
        }
        return max;
    }
}
```
分析：
时间复杂度：O（n<sup>2</sup>）
空间复杂度：O（1）

**方法二：**
双指针
设置两个指针l，r，分别指向数组的两端，两个指针向内移动，当height[l]<height[j]时，l向内移动，反之，r向内移动

```java
class Solution {
    public int maxArea(int[] height) {
        int max=0;
        int i=0,j= height.length-1;
        while (i!=j){
            int maxIJ =(j-i)*Math.min(height[i],height[j] );
            if (maxIJ>max)
                max=maxIJ;
            if (height[i]<height[j])
                i++;
            else
               j--;


        }
        return max;
    }
}
```
分析：
时间复杂度：O（n）
空间复杂度：O（1）