---
title: 34.在排序数组中查找元素的第一个和最后一个位置.md
date: 2022-01-26 22:28:47.57
updated: 2022-12-16 08:49:51.417
url: /archives/34在排序数组中查找元素的第一个和最后一个位置md
categories: 
tags: 力扣 | 题解
---

﻿题目描述：
给定一个按照升序排列的整数数组 nums，和一个目标值 target。找出给定目标值在数组中的开始位置和结束位置。

如果数组中不存在目标值 target，返回 [-1, -1]。

进阶：你可以设计并实现时间复杂度为 O(log n) 的算法解决此问题吗？

![在这里插入图片描述](https://img-blog.csdnimg.cn/cdbb5a752498436b93cf3a348e7a0d9b.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5bGx5Lit5pyJ5pyo,size_20,color_FFFFFF,t_70,g_se,x_16)
方法一：
由于给出的是有序数组，因此可以先用二分查找，找到某个target元素所在的位置索引index，再设置两个指针，分别从index处前后移动，寻找target元素的第一个和最后一个位置

```java
class Solution {
    public int[] searchRange(int[] nums, int target) {
        int[] result = new int[] {-1,-1};
        //index=-1，表明数组中不存在target元素
        int index=-1;
        //二分查找
        int right = nums.length-1,left=0;
        while (left<=right){
            if (left==right){
                if (nums[left]!=target){
                    left=nums.length;
                    break;
                }
                else if (nums[left]==target){
                    index=left;
                    break;
                }
            }
            int middle = (right+left)/2;
            if (nums[middle]>target)
                right=middle;
            else if (nums[middle]<target)
                left=middle+1;
            else {
                index=middle;
                break;
            }
        }
        //设置两个指针i，j，分别寻找target的第一个和最后一个位置
        int i,j;
        if (left> nums.length-1 || right<0 ){
            return result;
        }
        else {
            i=index;
            j=index;
        }

        while (i>0 && nums[i]==target ){
            i--;
        }
        while (nums[j]==target && j< nums.length-1){
            j++;
        }
        if (nums[i]!=target)
            i++;
        if (nums[j]!=target)
            j--;
       result[0]=i;
       result[1]=j;
        return  result;
    }
}
```
分析：
时间复杂度：二分查找的时间复杂度是O（logn），后面查找第一个和最后一个位置，当数组所有的元素都等于target时，相当于遍历一遍数组，因此时间复杂度是O（n），综上，时间复杂度为O（n）
空间复杂度：O（1）

上面的方法虽然用了二分的思想，但是最后还是可能要遍历一次数组，无法达到
O（logn）的时间复杂度，因此需要改进一下二分查找：

在进行二分查找时，low会增大，high会减小。
如果循环条件是low<=high,则循环结束时high在low前面。
要找右边的某个数时，要借助low实现，因为low会不断变大。
要找左边的某个数时，要借助high实现，因为high会不断变小。
要找=target的最左边的数时，也就是找满足>=target的最左边的数。
但是，当nums[mid]>=target时,无法判断nums[mid]是否是满足nums[mid]>=target的最左边的数。
所以不能让high = mid。
但是，当nums[mid]>=target时，可以判断nums[mid]是满足nums[mid]>=target的数。
所以，让high = mid - 1。这样，只要满足条件，high就变小，最终high会停在第一个不满足条件的点。
所以，当nums[mid]>=target时, high = mid - 1。
这样,最终high就会停在第一个不满足>=target的地方。
同理，要找=target的最右边的数时，也就是找<=target的最右边的数。
所以，当nums[mid]<=target时, low = mid + 1。
这样，最终low就会停在第一个不满足<=target的地方。
（作者：wjy1126）

```java
class Solution {
    public int[] searchRange(int[] nums, int target) {
        int left = getLeft(nums, target);
        int right = getRight(nums, target);
        if(right-left>1) return new int[] {left+1,right-1};
        else return new int[] {-1,-1};
    }
    public int getLeft(int[] nums, int target){
        int low = 0;
        int high = nums.length - 1;
        while (low <= high) {
            int mid = low + (high - low) / 2;
            if (nums[mid] > target) {
                high = mid - 1;
            } else if (nums[mid] < target) {
                low = mid + 1;
            } else {
                high = mid - 1;
            } 
        }
        return high;
    }
    public int getRight(int[] nums, int target) {
        int low = 0;
        int high = nums.length - 1;
        while (low <= high) {
            int mid = low + (high - low) / 2;
            if (nums[mid] > target) {
                high = mid - 1;
            } else if (nums[mid] < target) {
                low = mid + 1;
            } else {
                low = mid + 1;
            }
        }
        return low;
    }
}

作者：wjy1126
链接：https://leetcode-cn.com/problems/find-first-and-last-position-of-element-in-sorted-array/solution/xin-shou-ti-jie-er-fen-jie-jue-by-wjy112-h6su/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```