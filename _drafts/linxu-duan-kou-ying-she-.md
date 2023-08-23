---
title: linxu端口映射 
date: 2021-12-17 17:18:46.0
updated: 2022-12-16 08:44:29.559
url: /archives/linxu-duan-kou-ying-she-
categories: 
tags: Linux
---

Halo的默认端口是8090，在web端访问时总是要带上端口，很不方便，可以通过以下方法，将80映射到8090端口
```Linux
iptables -t nat -A PREROUTING -p tcp --dport 80 -j REDIRECT --to-port 8090
```
设置完之后，要重启nginx
```Linux
cd /usr/local/nginx/sbin
./nginx -s reload
```