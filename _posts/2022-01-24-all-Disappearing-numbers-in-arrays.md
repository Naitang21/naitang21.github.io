---
layout: post
title: 找到所有数组中消失的数字
categories: leetcode
description: 找到所有数组中消失的数字--力扣题解
keywords: leetcode
typora-root-url: ..
---

﻿题目描述：
给你一个含 n 个整数的数组 nums ，其中 nums[i] 在区间 [1, n] 内。请你找出所有在 [1, n] 范围内但没有出现在 nums 中的数字，并以数组的形式返回结果。

![img](/images/posts/all-Disappearing-numbers-in-arrays/2eac030b784842119f6e3bcf383c8623.png)
方法一：
这是我想到的第一个思路
先排序，再遍历数组，由于元素区间为[1,n]，排序后，遍历数组可以找到在区间[1,n]内，数组不存在的元素，此处排序使用了快排算法

```java
class Solution {
    public List<Integer> findDisappearedNumbers(int[] nums) {
        List<Integer> list = new ArrayList<>();
//        排序
        quickSort(nums);

        int count=1;
        for (int i=0;i< nums.length;i++){
            if (nums[i]==count){
                count++;
                continue;
            }else if( nums[i]>count){
                list.add(count);
                count++;
                i--;
            }
        }
        if (nums[nums.length-1]<nums.length){
            int num = nums[nums.length-1];
            while (num<nums.length){
                list.add(num+1);
                num++;
            }
        }
        return list;
    }

    /**
     * 快速排序
     * @param array
     */
    public  void quickSort(int[] array) {
        int len;
        if(array == null
                || (len = array.length) == 0
                || len == 1) {
            return ;
        }
        sort(array, 0, len - 1);
    }

    /**
     * 快排核心算法，递归实现
     * @param array
     * @param left
     * @param right
     */
    public  void sort(int[] array, int left, int right) {
        if(left > right) {
            return;
        }
        // base中存放基准数
        int base = array[left];
        int i = left, j = right;
        while(i != j) {
            // 顺序很重要，先从右边开始往左找，直到找到比base值小的数
            while(array[j] >= base && i < j) {
                j--;
            }

            // 再从左往右边找，直到找到比base值大的数
            while(array[i] <= base && i < j) {
                i++;
            }

            // 上面的循环结束表示找到了位置或者(i>=j)了，交换两个数在数组中的位置
            if(i < j) {
                int tmp = array[i];
                array[i] = array[j];
                array[j] = tmp;
            }
        }

        // 将基准数放到中间的位置（基准数归位）
        array[left] = array[i];
        array[i] = base;

        // 递归，继续向基准的左右两边执行和上面同样的操作
        // i的索引处为上面已确定好的基准值的位置，无需再处理
        sort(array, left, i - 1);
        sort(array, i + 1, right);
    }
}
```
分析：
使用了快排算法，时间复杂度O（nlogn），使用其他的排序算法，可以降低时间复杂度，但是无法达到线性的时间复杂度


方法二：
（这是在力扣看到的官方题解）
利用哈希表的思想
因为数组的每一个元素都在[1，n]的范围内，我们可以利用**在该范围之外**的数字，来表示**是否存在**的这一含义
     用原数组来充当哈希表，遍历原数组nums，对于每一个数组元素x，令 nums [x-1] 的值加上n，由于nums 中所有数均在[1,n] 中，增加以后，这些数必然大于 n。最后我们遍历nums，若 nums[i] 未大于 n，就说明没有遇到过数 i+1。这样我们就找到了缺失的数字
注意：因为当我们遍历到某个位置时，其中的数可能已经被增加过，因此需要对 n 取模来还原出它本来的值

```java
class Solution {
    public List<Integer> findDisappearedNumbers(int[] nums) {
        int n = nums.length;
        for (int num : nums) {
            int x = (num - 1) % n;
            nums[x] += n;
        }
        List<Integer> ret = new ArrayList<Integer>();
        for (int i = 0; i < n; i++) {
            if (nums[i] <= n) {
                ret.add(i + 1);
            }
        }
        return ret;
    }
}
```

分析：
时间复杂度：O(n)
空间复杂度：O(1)


方法三：
（思路来自力扣的ₑπi₊₁₌₀用户）
利用鸽笼原理，1-n的位置表示1~n个笼子，如果出现过，相应的“鸽笼”就会被占掉，我们将数字置为负数表示被占掉了。 最后再遍历一遍，如果“鸽笼”为正数就是没出现的数字

```java
public List<Integer> findDisappearedNumbers(int[] nums) {
        for (int i = 0; i < nums.length; i++) {
            nums[Math.abs(nums[i])-1] = -Math.abs(nums[Math.abs(nums[i])-1]);
        }
        List<Integer> list = new ArrayList<>();
        for (int i=0;i< nums.length;i++){
            if (nums[i]>0){
                list.add(i+1);
            }
        }
        return list;
    }

```
分析：
时间复杂度：O(n)，但是在提交的测试用例中，这个方法比方法二慢
空间复杂度：O(1)