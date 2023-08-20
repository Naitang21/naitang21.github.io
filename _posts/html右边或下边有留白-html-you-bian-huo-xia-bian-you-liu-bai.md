---
title: html右边或下边有留白
date: 2021-12-05 16:48:47.0
updated: 2022-12-16 08:44:32.454
url: /archives/html-you-bian-huo-xia-bian-you-liu-bai
categories: 
tags: html
---

问题：html页面右边或者底部总有一部分空白区域，需要拉动滚动条才能看到
在知乎看到的一个很有用的方法（来自知乎的“表酱紫”大佬）

控制台运行：
```html
[].forEach.call($$("*"),function(a){
a.style.outline="1px solid #"+(~~(Math.random()*(1<<24))).toString(16)
})
```
可以查看是哪些元素溢出了

