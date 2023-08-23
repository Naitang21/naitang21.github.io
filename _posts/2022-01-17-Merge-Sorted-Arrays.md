---
layout: post
title: 合并排序的数组
categories: leetcode
description: 合并排序的数组--力扣题解
keywords: leetcode
typora-root-url: ..
---

﻿题目描述：
![在这里插入图片描述](/images/posts/Merge-Sorted-Arrays/8b9ef269384c4fccb61ddec155bce171.png)
方法一：
我的思路：
先判断是升序还是降序
假如是升序：
利用两个指针a和b，分别指向数组A和数组B，从数组A的后端开始插入元素，指针a和b分别逐个遍历数组A和数组B，把较大的元素插入到数组A的后端

```
class Solution {
    public void merge(int[] A, int m, int[] B, int n) {
         if (m==0){
            for (int i=0;i<n;i++){
                A[i]=B[i];
            }
            return;
        }

        if (n==0)
            return;

        int flag = 0;//升序
//        先分析是升序还是降序
        if (m>=2){
            if (A[1]<A[0])
                flag=1;//降序
        }else if (n>=2){
            if (B[1]<B[0])
                flag=1;//降序
        }

        int a=m;
        int b=n;

        while (a!=0 && b!=0){
            if (flag==0){
                //升序
                if (A[a-1]<B[b-1]){
                    A[a+b-1]=B[b-1];
                    b--;
                }else {
                    A[a+b-1]=A[a-1];
                    a--;
                }
            }
        }
        if (a==0){
            while (b!=0){
                A[a+b-1]=B[b-1];
                b--;
            }
        }
       else if (b==0){
            while (a!=0){
                A[a+b-1]=A[a-1];
                a--;
            }
        }
    }
}
```
时间复杂度：O（n+m）
空间复杂度：O（1）