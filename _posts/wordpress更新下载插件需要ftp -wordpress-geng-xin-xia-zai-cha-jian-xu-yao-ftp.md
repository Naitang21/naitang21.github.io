---
title: wordpress更新下载插件需要ftp 
date: 2021-12-13 17:17:06.0
updated: 2022-12-16 08:44:18.869
url: /archives/wordpress-geng-xin-xia-zai-cha-jian-xu-yao-ftp
categories: 
tags: wordpress
---

因为之前的博客丢失，所以忘了怎么解决了qwq
网上很多解决方法都是给777权限，但是不安全
先运行Ps -ef 查看php-fpm对应的进程账号，如www

```Linux
chown -R www wordpress目录
```