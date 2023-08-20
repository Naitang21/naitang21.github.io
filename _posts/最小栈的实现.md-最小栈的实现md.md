---
title: 最小栈的实现.md
date: 2022-01-12 23:34:06.49
updated: 2022-01-12 23:34:06.49
url: /archives/最小栈的实现md
categories: 
tags: 
---

﻿《小灰的算法之旅》学习笔记

**题目：** 
实现一个栈，该栈带有出栈（pop），入栈（push），取最小元素（getMin）3个方法，要保证这3个方法的事件复杂度都是O(1)

**解决方法：**
1. 设原有的栈为A，新建一个辅助栈B
2. 当第1个元素进入栈A时，让新元素也进入栈B，此时，这个唯一的元素就是栈A的最小值
3. 之后，当新元素进入栈A时，比较新元素和栈A当前最小值的大小，如果小于栈A当前最小值，则让新元素也进入栈B
4. 每当栈A有元素出栈时，若出栈元素是栈A当前最小值，则让栈B的栈顶元素出栈，此时，栈B余下的栈顶元素所指向的，就是栈A中原本第2小的元素
5. 当调用getMin方法时，返回栈B的栈顶元素的值，该值就是栈A的最小值

**分析：** 
该方法中，进栈，。出栈，取最小值的时间复杂度都为O(1)，最坏情况下的空间复杂度为O(n)，最坏情况就是，进入栈A中的元素，原本就有序（倒序）

![在这里插入图片描述](https://img-blog.csdnimg.cn/0b104e22d74047ce9da6d702f604bfa9.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5bCP55m95YWU5aW257OWaQ==,size_20,color_FFFFFF,t_70,g_se,x_16)

```java
//    进栈
    public void push(Stack A,int element,Stack B){
//        栈A为空 或 新元素小于等于B的栈顶元素，则新元素压入B
        if (A.getMaxSize()==0 || element<=B.getTop()){
            B.push(element,B);
        }
        A.push(element,A);
    }

//    出栈
    public int pop(Stack A,Stack B){
        int element;
        element = A.pop(A);
//        若出栈元素和B栈顶元素相等，则B栈顶出栈
        if (element == B.getTop()){
            B.pop(B);
        }
        return element;
    }

    public int getMin(Stack A,Stack B){
        int minElement;
        minElement = B.getTop();
        return minElement;
    }
```