---
layout: post
title: StringBuilder，StringBuffer，String
categories: Java
description: StringBuilder，StringBuffer，String
keywords: Java
typora-root-url: ..
---

| <p><strong>运行速度：</strong><br />
StringBuilder&gt;StringBuffer&gt;String</p>

<p>String是字符串常量，不可变，而StringBuilder和StringBuffer是字符串变量，可以更改</p>
<p><strong>适用情况</strong><br />
String：适用于少量字符串操作的情况<br />
StringBuilder：适用于单线程下在字符缓冲区进行大量操作的情况<br />
StringBuffer：适用多线程下在字符缓冲区进行大量操作的情况</p>
<p><strong>线程安全：</strong><br />
StringBuilder线程不安全<br />
String，StringBuffer线程安全</p>
**运行速度:**

StringBuilder>StringBuffer>String

String是字符串常量，不可变，而StringBuilder和StringBuffer是字符串变量，可以更改

**适用情况**
String：适用于少量字符串操作的情况
StringBuilder：适用于单线程下在字符缓冲区进行大量操作的情况
StringBuffer：适用多线程下在字符缓冲区进行大量操作的情况

**线程安全：**
StringBuilder线程不安全
String，StringBuffer线程安全

  