---
title: ==和equals（）
date: 2021-12-03 17:12:31.0
updated: 2022-12-16 08:44:24.975
url: /archives/-he-equals
categories: 
tags: Java
---

<p><strong>==：</strong></p>
<ol>
<li>如果作用于基本数据类型的变量，则直接比较其存储的<strong>值</strong>是否相等</li>
<li>如果作用域引用类型的变量，则比较所指向的<strong>对象的地址</strong></li>
</ol>
<p><strong>equals()：</strong></p>
<ol>
<li>equals（）不能作用于基本数据类型的变量</li>
<li>Object类中，equals方法用来比较指向的字符串对象所存储的字符串是否相等</li>
<li>其他类，比如Double，Date，Integer等，对equals方法进行了重写，用来比较所指向的对象所存储的<strong>值的内容</strong>是否相等</li>
</ol>
<pre><code class="language-Java">       String a = &quot;abc&quot;;
        String b = &quot;abc&quot;;
        String c = new String(&quot;abc&quot;);
        String d = new String(&quot;abc&quot;);

        System.out.println(a==b);
        System.out.println(a==c);
        System.out.println(c==d);
        System.out.println(a.equals(c));
        System.out.println(c.equals(d));
</code></pre>
<p>输出结果：<br />
true<br />
false<br />
false<br />
true<br />
true</p>

**==：**
1. 如果作用于基本数据类型的变量，则直接比较其存储的**值**是否相等
2. 如果作用域引用类型的变量，则比较所指向的**对象的地址**


**equals()：**
1. equals（）不能作用于基本数据类型的变量
2. Object类中，equals方法用来比较指向的字符串对象所存储的字符串是否相等
3. 其他类，比如Double，Date，Integer等，对equals方法进行了重写，用来比较所指向的对象所存储的**值的内容**是否相等


```Java
        String a = "abc";
        String b = "abc";
        String c = new String("abc");
        String d = new String("abc");

        System.out.println(a==b);
        System.out.println(a==c);
        System.out.println(c==d);
        System.out.println(a.equals(c));
        System.out.println(c.equals(d));
```

输出结果：
true
false
false
true
true