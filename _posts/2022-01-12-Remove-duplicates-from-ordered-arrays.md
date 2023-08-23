---
layout: post
title: 删除有序数组中的重复项
categories: leetcode
description: 删除有序数组中的重复项--力扣题解
keywords: leetcode
typora-root-url: ..
---

﻿**题目**
给你一个有序数组 nums ，请你 原地 删除重复出现的元素，使每个元素 只出现一次 ，返回删除后数组的新长度。

不要使用额外的数组空间，你必须在 原地 修改输入数组 并在使用 O(1) 额外空间的条件下完成。
![在这里插入图片描述](/images/posts/Remove-duplicates-from-ordered-arrays/ad75af4f880143e9864873ef6482ffef.png)
![在这里插入图片描述](/images/posts/Remove-duplicates-from-ordered-arrays/877008a20e8f4e7083e54349f36c60a4.png)

**分析**
- 当数组nums为空（长度为0）时，直接返回0
- length是要返回的值，即新数组的长度，也就是不含重复元素的范围的长度
- 因为nums数组的第一个元素，一定不重复，因此可以从nums[1]开始遍历数组
- 当元素 i 和元素 i-1 相同时，说明元素重复，此时不作操作，继续遍历
- 当元素i 和元素 i-1 不同时，把元素 i 放到 nums[length] 位置（数组nums 的前length个元素是不重复的），并让length+1

**例子**
![在这里插入图片描述](/images/posts/Remove-duplicates-from-ordered-arrays/a64908d2783c496eb35ef3542de939a6.png)



```java
public int removeDuplicates(int[] nums) {
        int length=1;
        if (nums.length==0)
            return 0;
        for (int i=1;i< nums.length;i++){
            if (nums[i]!=nums[i-1]){
                nums[length]=nums[i];
                length=length+1;
            }
        }
        return length;
    }
```