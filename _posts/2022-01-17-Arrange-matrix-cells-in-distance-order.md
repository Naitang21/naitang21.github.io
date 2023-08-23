---
layout: post
title: 距离顺序排列矩阵单元格
categories: leetcode
description: 距离顺序排列矩阵单元格--力扣题解
keywords: leetcode
typora-root-url: ..
---

﻿题目描述：
![img](/images/posts/1030.%20%E8%B7%9D%E7%A6%BB%E9%A1%BA%E5%BA%8F%E6%8E%92%E5%88%97%E7%9F%A9%E9%98%B5%E5%8D%95%E5%85%83%E6%A0%BC--%E5%8A%9B%E6%89%A3%E9%A2%98%E8%A7%A3.md-1030%E8%B7%9D%E7%A6%BB%E9%A1%BA%E5%BA%8F%E6%8E%92%E5%88%97%E7%9F%A9%E9%98%B5%E5%8D%95%E5%85%83%E6%A0%BC--%E5%8A%9B%E6%89%A3%E9%A2%98%E8%A7%A3md/5307f4c3c0594dd695aeeac9986817f9.png)
方法一：
我的思路：
画图可知，需要输出的二维数组的顺序如下：（1，2，3为输出的顺序）
![在这里插入图片描述](https://img-blog.csdnimg.cn/7312baa7396642afbb8fa7b28e717e06.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5bGx5Lit5pyJ5pyo,size_20,color_FFFFFF,t_70,g_se,x_16)

主要是要分析边界问题

```
class Solution {
    public int[][] allCellsDistOrder(int rows, int cols, int rCenter, int cCenter) {
        int[][] result = new int[rows*cols][];
        result[0] =new int[] {rCenter,cCenter};
        int nums = 0;
        int i=1;
        int index=1;

        while (nums<rows*cols && i<rows*cols){
            for (int j=0;j<=i;j++){
                if (j==0){
                    if (rCenter+j<rows && cCenter+(i-j)<cols ){
                        result[index]=new int[] {rCenter+j,cCenter+(i-j)};
                        index++;
                        nums++;
                    }
                    if (rCenter+j<rows && cCenter-(i-j)>=0 ){
                        result[index]=new int[] {rCenter+j,cCenter-(i-j)};
                        index++;
                        nums++;
                    }
                }
                else if (i-j==0){
                    if (rCenter+j<rows && cCenter+(i-j)<cols ){
                        result[index]=new int[] {rCenter+j,cCenter+(i-j)};
                        index++;
                        nums++;
                    }
                    if (rCenter-j>=0 && cCenter+(i-j)<cols ){
                        result[index]=new int[] {rCenter-j,cCenter+(i-j)};
                        index++;
                        nums++;
                    }
                }
                else {
                    if (rCenter+j<rows && cCenter+(i-j)<cols ){
                        result[index]=new int[] {rCenter+j,cCenter+(i-j)};
                        index++;
                        nums++;
                    }
                    if (rCenter+j<rows && cCenter-(i-j)>=0 ){
                        result[index]=new int[] {rCenter+j,cCenter-(i-j)};
                        index++;
                        nums++;
                    }
                    if (rCenter-j>=0 && cCenter+(i-j)<cols ){
                        result[index]=new int[] {rCenter-j,cCenter+(i-j)};
                        index++;
                        nums++;
                    }
                    if (rCenter-j>=0 && cCenter-(i-j)>=0 ){
                        result[index]=new int[] {rCenter-j,cCenter-(i-j)};
                        index++;
                        nums++;
                    }
                }


            }
            i++;

    }

        return result;

    }
}
```
时间复杂度：O（rows*cols）<sup>2</sup>
空间复杂度：O（1）