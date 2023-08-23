---
layout: post
title: string split（）
categories: Java
description: string split（）
keywords: Java
typora-root-url: ..
---

<pre><code class="language-Java">string Object.split(separator,howmany)
</code></pre>
<p>作用：把一个字符串a分割成字符串数组<br />
值得注意的是：</p>
<pre><code class="language-Java">String aa = &quot;&quot;;
System.out.println(aa.split(&quot;,&quot;).length);
</code></pre>
<p>输出的结果是：1<br />
因为当字符串a是“”时，会把它当作一个长度为1的字符串放到数组的第一个元素中，所以长度为1</p>
<pre><code class="language-Java">String aa = &quot;aa&quot;;
System.out.println(aa.split(&quot;,&quot;).length);
</code></pre>
<p>输出的结果为：1<br />
因为aa字符串中，没有 ， 符号，将aa作为第一个字符串放到字符串数组的第一个位置，并返回字符串数组</p>
<pre><code class="language-Java">String aa = &quot;aa,bb&quot;;
System.out.println(aa.split(&quot;,&quot;).length);
</code></pre>
<p>输出的结果为：2<br />
<strong>，</strong> 号将<strong>aa,bb</strong>分割成两个字符串</p>

```Java
string Object.split(separator,howmany)
```


作用：把一个字符串a分割成字符串数组
值得注意的是：
```Java
String aa = "";
System.out.println(aa.split(",").length);
```
输出的结果是：1
因为当字符串a是“”时，会把它当作一个长度为1的字符串放到数组的第一个元素中，所以长度为1

```Java
String aa = "aa";
System.out.println(aa.split(",").length);
```
输出的结果为：1
因为aa字符串中，没有 ， 符号，将aa作为第一个字符串放到字符串数组的第一个位置，并返回字符串数组

```Java
String aa = "aa,bb";
System.out.println(aa.split(",").length);
```
输出的结果为：2
**，** 号将**aa,bb**分割成两个字符串   