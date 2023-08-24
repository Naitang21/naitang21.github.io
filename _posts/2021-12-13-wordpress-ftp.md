---
layout: post
title: wordpress更新下载插件需要ftp 
categories: Wordpress
description: wordpress更新下载插件需要ftp 
keywords: Wordpress
typora-root-url: ..
---

因为之前的博客丢失，所以忘了怎么解决了qwq
网上很多解决方法都是给777权限，但是不安全
先运行Ps -ef 查看php-fpm对应的进程账号，如www

```Linux
chown -R www wordpress目录
```