---
title: tomcat配置域名访问 
date: 2021-12-23 17:24:14.0
updated: 2022-12-16 08:44:31.0
url: /archives/tomcat-pei-zhi-yu-ming-fang-wen-
categories: 
tags: tomcat
---

进入tomcat的conf目录中，修改server.xml文件
1. 找到下面这个标签，修改**defaultHost**的值为你的域名
```Linux
<Engine name="Catalina" defaultHost="localhost">
```
比如：我的域名是naitang21.cc，则修改成：
```Linux
<Engine name="Catalina" defaultHost="naitang21.cc">
```

2. 找到下面这个标签，修改**name**为你的域名
```Linux
<Host name="localhost" appBase="webapps" unpackWARs="true" autoDeploy="true">
```
比如我修改成：
```Linux
<Host name="naitang21.cc" appBase="webapps" unpackWARs="true" autoDeploy="true">
```

也可以修改端口号，找到下面这个标签
```Linux
<Connector port="8080" protocol="HTTP/1.1"
               connectionTimeout="20000"
               redirectPort="8443" />
```