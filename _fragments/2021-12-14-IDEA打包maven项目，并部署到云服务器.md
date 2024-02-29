---
layout: fragment
title: IDEA打包maven项目，并部署到云服务器
tags: Tool
description: IDEA打包maven项目，并部署到云服务器
keywords: IDEA Maven
typora-root-url: ..
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
<!--stackedit_data:
eyJoaXN0b3J5IjpbNDAxNzE3NzA3XX0=
-->