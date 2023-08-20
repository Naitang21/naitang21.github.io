---
title: 启动nginx失败，80端口被占用 
date: 2021-12-23 17:19:58.0
updated: 2022-12-16 08:44:29.558
url: /archives/qi-dong-nginx-shi-bai-80-duan-kou-bei-zhan-yong-
categories: 
tags: Linux | nginx
---

查看占用80端口的进程
```Linux
netstat -ntlp|grep 80
```
杀死进程
```Linux
kill 端口号
```
启动nginx
```Linux
cd /usr/local/nginx/sbin
./nginx
```