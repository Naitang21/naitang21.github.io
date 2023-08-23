---
layout: post
title: 移出元素
categories: leetcode
description: 移出元素--力扣题解
keywords: leetcode
typora-root-url: ..
---

﻿**题目描述：**
给你一个数组 nums 和一个值 val，你需要 原地 移除所有数值等于 val 的元素，并返回移除后数组的新长度。

不要使用额外的数组空间，你必须仅使用 O(1) 额外空间并 原地 修改输入数组。

元素的顺序可以改变。你不需要考虑数组中超出新长度后面的元素。



**方法一：**
**我的思路：**
	由于需要原地修改数组，并且数组的顺序可以改变
	返回值为count，也就是该数组移除掉特定元素 val 的长度
	遍历数组，当元素 nums[i] == val 时，把数组后面的元素移到 nums[i] 的位置，并且count-1
 此处，有一种情况就是，数组后面的元素等于 val ，所以我做了处理：当数组后面的元素等于 val 时，先把数组后面这些等于 val 的元素移除

```
class Solution {
    public int removeElement(int[] nums, int val) {
        if (nums.length==0){
            return 0;
        }

        int count = nums.length;

        while (count>0 && nums[count-1]==val){
            count--;
        }
        for (int i=0;i<count;i++){
                if (nums[i]==val){
                    while (nums[count-1]==val){
                        count--;
                    }
                   if (i<count){
                       nums[i]=nums[count-1];
                       count--;
                   }
            }
        }
        return count;
    }
}
```

分析：
时间复杂度：O（n）
空间复杂度：O（1）


（看了一下题解，发现自己想太复杂了）

**方法二：**
**双指针**
![img](/images/posts/2022-01-17-Remove-the-element/1a2cc3e9506740bf95d867212a303b5d.png)

```
class Solution {
    public int removeElement(int[] nums, int val) {
        int n = nums.length;
        int left = 0;
        for (int right = 0; right < n; right++) {
            if (nums[right] != val) {
                nums[left] = nums[right];
                left++;
            }
        }
        return left;
    }
}

```


![a154d27bd60248f0ba5024921bc0492a](/images/posts/2022-01-17-Remove-the-element/a154d27bd60248f0ba5024921bc0492a.png)

方法三：
对方法二进行优化
![a154d27bd60248f0ba5024921bc0492a](/images/posts/2022-01-17-Remove-the-element/a154d27bd60248f0ba5024921bc0492a.png)

```
class Solution {
    public int removeElement(int[] nums, int val) {
        int left = 0;
        int right = nums.length;
        while (left < right) {
            if (nums[left] == val) {
                nums[left] = nums[right - 1];
                right--;
            } else {
                left++;
            }
        }
        return left;
    }
}

```
![1](/images/posts/2022-01-17-Remove-the-element/1.png)