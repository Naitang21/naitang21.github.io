---
title: IDEA打包maven项目，并部署到云服务器 
date: 2021-12-14 17:22:28.0
updated: 2022-12-16 08:44:30.999
url: /archives/idea-da-bao-maven-xiang-mu--bing-bu-shu-dao-yun-fu-wu-qi-
categories: 
tags: tomcat
---

1. 点击右侧“**maven**”的**Lifecycle**

2. 点击**package**进行打包
（如果之前打包过，但是修改了项目，可以先点击**clean**，再点击**package**进行打包）
3. 在项目目录的target目录下找到war包
4. 用SSH工具把war传输到云服务器
5. 在云服务器中，将war包

放到tomcat的webapps目录下，即可以在网页中访问项目
**注意：**
比如，项目war包名为：a.var
云服务器的ip地址为：111.222.333.444
则访问项目的路径为：111.222.333.444：端口/a/