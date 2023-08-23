---
layout: post
title: 两数之和
categories: leetcode
description: 两数之和--力扣题解
keywords: leetcode
typora-root-url: ..
---

﻿**题目**
给定一个整数数组 nums 和一个整数目标值 target，请你在该数组中找出 和为目标值 target  的那 两个 整数，并返回它们的数组下标。

你可以假设每种输入只会对应一个答案。但是，数组中同一个元素在答案里不能重复出现。

你可以按任意顺序返回答案。

![img](/images/posts/Sum-of-two-numbers/15f774678a6240b18806de0776484417.png)

**方法一，枚举**
用两个for循环，遍历数组的每一个元素，对于元素i，遍历元素i之后的元素，看是否存在target-i元素，如果存在，则输出

**分析**
这是我想到的第一种方法，用到了两个for循环，如果数组有n个元素，其时间复杂度为O（n^2^），空间复杂度为O(1)

```java
public int[] twoSum(int[] nums, int target) {
        int[] result = new int[2];
        for(int i=0;i<nums.length;i++){
            for(int j=i+1;j<nums.length;j++){
                if(nums[j]==target-nums[i]){
                    result[0]=i;
                    result[1]=j;
                    return result;
                }
            }
        }
        return result;
    }
```

**方法二，利用哈希表**
方法一在查询 target-i 时，是在原数组上进行查询的，在数组中查询一个定值的时间复杂度是O(n)，我们利用哈希表，则可以把时间复杂度降到O(1)

**具体步骤**
遍历数组的元素，对于每一个元素 i ，去哈希表中查询是否有 target -i 元素，如果有，则记录下来以返回，然后再把元素插入到哈希表中

```java
public int[] twoSum(int[] nums, int target){
        int result[] = new int[2];
        HashMap<Integer,Integer> hashMap = new HashMap<>();
        for (int i=0;i< nums.length;i++){
            if (hashMap.containsKey(target-nums[i])){
                result[0]=i;
                result[1]=hashMap.get(target-nums[i]);
            }
            hashMap.put(nums[i],i);
        }
        return result;
    }
```