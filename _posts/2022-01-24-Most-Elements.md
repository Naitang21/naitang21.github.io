---
layout: post
title: 多数元素
categories: leetcode
description: 多数元素--力扣题解
keywords: leetcode
typora-root-url: ..
---

﻿题目描述：
给定一个大小为 n 的数组，找到其中的多数元素。多数元素是指在数组中出现次数 大于 ⌊ n/2 ⌋ 的元素。

你可以假设数组是非空的，并且给定的数组总是存在多数元素。

![在这里插入图片描述](/images/posts/Most-Elements/8de342c989c54e13beba9c64fc6dee99.png)
方法一：
先排序。由于多数元素的出现次数＞⌊ n/2 ⌋，所以排完序之后，数组中间的元素必定是多数元素
此处我使用了堆排序

```java
	class Solution {
    public int majorityElement(int[] nums) {
         heapSort(nums);
        return nums[nums.length/2];
    }

     public static void heapSort(int[] arr) {
        if (arr == null || arr.length == 0) {
            return;
        }
        int len = arr.length;
        // 构建大顶堆
        buildMaxHeap(arr, len);

        // 重置大顶堆
        for (int i = len - 1; i > 0; i--) {
            swap(arr, 0, i);
            len--;
            heapify(arr, 0, len);
        }
    }

    private static void buildMaxHeap(int[] arr, int len) {
        // 调整
        for (int i = (int)Math.floor(len / 2) - 1; i >= 0; i--) {
            heapify(arr, i, len);
        }
    }

    private static void heapify(int[] arr, int i, int len) {
        int left = 2 * i + 1;
        int right = 2 * i + 2;
        int largestIndex = i;
        if (left < len && arr[left] > arr[largestIndex]) {
            largestIndex = left;
        }
        if (right < len && arr[right] > arr[largestIndex]) {
            largestIndex = right;
        }

        if (largestIndex != i) {
            swap(arr, i, largestIndex);
            heapify(arr, largestIndex, len);
        }
    }

    private static void swap (int[] arr, int i, int j) {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }
}
```
分析：
由于使用了堆排序算法，时间复杂度为Ｏ（nlogn）
空间复杂度：O（1）


方法二：
摩尔投票法
如果把众数记为 +1，把其他数记为 −1，将它们全部加起来，显然和大于 0，从结果本身我们可以看出众数比其他数多
从第一个数开始，记count=1，遍历数组，如果遇到相同的元素，count+1，如果遇到不同的元素，count-1，当count减到0时，换一个数继续遍历和计数，最后总能找到多数元素

```java
class Solution {
    public int majorityElement(int[] nums) {
         int count=1,num=nums[0];
        for (int i=1;i< nums.length;i++){
            if (num==nums[i]){
                count++;
            }else {
                count--;
            }
            if (count==0){
                num=nums[i+1];
            }
        }
        return num;
    }
}
```
分析：
时间复杂度：O（n），因为只遍历了一次数组
空间复杂度：O（1）

方法三：
这是在官方题解中看到的思路
使用哈希映射来存储每个元素以及出现的次数。对于哈希映射中的每个键值对，键表示一个元素，值表示该元素出现的次数。

```java
class Solution {
    private Map<Integer, Integer> countNums(int[] nums) {
        Map<Integer, Integer> counts = new HashMap<Integer, Integer>();
        for (int num : nums) {
            if (!counts.containsKey(num)) {
                counts.put(num, 1);
            } else {
                counts.put(num, counts.get(num) + 1);
            }
        }
        return counts;
    }

    public int majorityElement(int[] nums) {
        Map<Integer, Integer> counts = countNums(nums);

        Map.Entry<Integer, Integer> majorityEntry = null;
        for (Map.Entry<Integer, Integer> entry : counts.entrySet()) {
            if (majorityEntry == null || entry.getValue() > majorityEntry.getValue()) {
                majorityEntry = entry;
            }
        }

        return majorityEntry.getKey();
    }
}

```

分析：
时间复杂度：O（n）
空间复杂度：O（n）