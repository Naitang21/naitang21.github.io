---
title: Nginx启动成功，浏览器无法访问页面.md
date: 2022-01-12 23:33:57.514
updated: 2022-01-12 23:33:57.514
url: /archives/nginx启动成功浏览器无法访问页面md
categories: 
tags: 
---

﻿查看nginx进程

ps -ef | grep nginx

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210304213147850.png)
显示启动成功

然后查看8端口是否被分配给了Nginx 执行：

netstat -ntlp
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210304213227320.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3hidG50,size_16,color_FFFFFF,t_70)
可以看到是正常

再配置下防火墙

firewall-cmd --zone=public --add-port=80/tcp --permanent

重启防火墙

systemctl restart firewalld.service

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210304213322937.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3hidG50,size_16,color_FFFFFF,t_70)