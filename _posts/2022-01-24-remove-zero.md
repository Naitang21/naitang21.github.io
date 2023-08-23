---
layout: post
title: 移动零
categories: leetcode
description: 移动零--力扣题解
keywords: leetcode
typora-root-url: ..
---


双指针遍历
左指针指向已处理好的序列的尾部，右指针指向待处理的序列的首部，右指针不断向右移动，每次右指针指向非零数，则将左右指针对应的数交换，同时左指针右移

```java
class Solution {
    public void moveZeroes(int[] nums) {
        int n = nums.length, left = 0, right = 0;
        while (right < n) {
            if (nums[right] != 0) {
                swap(nums, left, right);
                left++;
            }
            right++;
        }
    }

    public void swap(int[] nums, int left, int right) {
        int temp = nums[left];
        nums[left] = nums[right];
        nums[right] = temp;
    }
}

```

分析：
时间复杂度：O（n）
空间复杂度：O（1）