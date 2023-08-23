---
layout: post
title: 链表中倒数第k个节点
categories: leetcode
description: 链表中倒数第k个节点--力扣题解
keywords: leetcode
typora-root-url: ..
---

﻿**题目**
输入一个链表，输出该链表中倒数第k个节点。为了符合大多数人的习惯，本题从1开始计数，即链表的尾节点是倒数第1个节点。

例如，一个链表有 6 个节点，从头节点开始，它们的值依次是 1、2、3、4、5、6。这个链表的倒数第 3 个节点是值为 4 的节点。

![img](/images/posts/The-k-th-node-from-the-bottom-in-the-linked-list/f6ec9310648849e6870f9ad5221c8b57.png)

**方法一，设置两个指针**

- 设置两个指针p1，p2，让p1先走 k-1 步，然后p1和p2同时往后移动，当p1到达了最后一个节点，此时，p2所在节点，就是倒数第k个节点

```java
public ListNode getKthFromEnd(ListNode head, int k) {
        ListNode p1 = head;
        ListNode p2 = head;

        for (int i=0;i<k;i++){
            p1=p1.next;
        }
        while (p1.next!=null){
            p1=p1.next;
            p2=p2.next;
        }
        return p2;
    }
```