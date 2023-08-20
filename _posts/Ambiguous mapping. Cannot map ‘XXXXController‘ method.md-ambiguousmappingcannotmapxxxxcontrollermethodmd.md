---
title: Ambiguous mapping. Cannot map ‘XXXXController‘ method.md
date: 2022-01-12 23:34:06.568
updated: 2022-01-12 23:34:06.568
url: /archives/ambiguousmappingcannotmapxxxxcontrollermethodmd
categories: 
tags: 
---

﻿```java
org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'org.springframework.web.servlet.mvc.method.annotation.RequestMappingHandlerMapping': Invocation of init method failed; nested exception is java.lang.IllegalStateException: Ambiguous mapping. Cannot map 'buildingController' method 
com.item.Controller.BuildingController#dijstra()
to { [/buildingController]}: There is already 'buildingController' bean method
com.item.Controller.BuildingController#aStar() mapped.
		at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.initializeBean(AbstractAutowireCapableBeanFactory.java:1786)
		at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.doCreateBean(AbstractAutowireCapableBeanFactory.java:602)
		at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.createBean(AbstractAutowireCapableBeanFactory.java:524)
		at org.springframework.beans.factory.support.AbstractBeanFactory.lambda$doGetBean$0(AbstractBeanFactory.java:335)
		at org.springframework.beans.factory.support.DefaultSingletonBeanRegistry.getSingleton(DefaultSingletonBeanRegistry.java:234)
		at org.springframework.beans.factory.support.AbstractBeanFactory.doGetBean(AbstractBeanFactory.java:333)
		at org.springframework.beans.factory.support.AbstractBeanFactory.getBean(AbstractBeanFactory.java:208)
		at org.springframework.beans.factory.support.DefaultListableBeanFactory.preInstantiateSingletons(DefaultListableBeanFactory.java:944)
		at org.springframework.context.support.AbstractApplicationContext.finishBeanFactoryInitialization(AbstractApplicationContext.java:918)
		at org.springframework.context.support.AbstractApplicationContext.refresh(AbstractApplicationContext.java:583)
		at org.springframework.web.servlet.FrameworkServlet.configureAndRefreshWebApplicationContext(FrameworkServlet.java:702)
		at org.springframework.web.servlet.FrameworkServlet.createWebApplicationContext(FrameworkServlet.java:668)
		at org.springframework.web.servlet.FrameworkServlet.createWebApplicationContext(FrameworkServlet.java:716)
		at org.springframework.web.servlet.FrameworkServlet.initWebApplicationContext(FrameworkServlet.java:591)
		at org.springframework.web.servlet.FrameworkServlet.initServletBean(FrameworkServlet.java:530)
		at org.springframework.web.servlet.HttpServletBean.init(HttpServletBean.java:170)
		at javax.servlet.GenericServlet.init(GenericServlet.java:158)
		at org.apache.catalina.core.StandardWrapper.initServlet(StandardWrapper.java:1134)
		at org.apache.catalina.core.StandardWrapper.loadServlet(StandardWrapper.java:1089)
		at org.apache.catalina.core.StandardWrapper.allocate(StandardWrapper.java:761)
		at org.apache.catalina.core.StandardWrapperValve.invoke(StandardWrapperValve.java:135)
		at org.apache.catalina.core.StandardContextValve.invoke(StandardContextValve.java:96)
		at org.apache.catalina.authenticator.AuthenticatorBase.invoke(AuthenticatorBase.java:541)
		at org.apache.catalina.core.StandardHostValve.invoke(StandardHostValve.java:139)
		at org.apache.catalina.valves.ErrorReportValve.invoke(ErrorReportValve.java:92)
		at org.apache.catalina.valves.AbstractAccessLogValve.invoke(AbstractAccessLogValve.java:690)
		at org.apache.catalina.core.StandardEngineValve.invoke(StandardEngineValve.java:74)
		at org.apache.catalina.connector.CoyoteAdapter.service(CoyoteAdapter.java:343)
		at org.apache.coyote.http11.Http11Processor.service(Http11Processor.java:373)
		at org.apache.coyote.AbstractProcessorLight.process(AbstractProcessorLight.java:65)
		at org.apache.coyote.AbstractProtocol$ConnectionHandler.process(AbstractProtocol.java:868)
		at org.apache.tomcat.util.net.NioEndpoint$SocketProcessor.doRun(NioEndpoint.java:1589)
		at org.apache.tomcat.util.net.SocketProcessorBase.run(SocketProcessorBase.java:49)
		at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1149)
		at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:624)
		at org.apache.tomcat.util.threads.TaskThread$WrappingRunnable.run(TaskThread.java:61)
		at java.lang.Thread.run(Thread.java:748)
```

**错误原因：**
从log里面就可以看出原因，是Controller层，类或方法里面有相同的路径
![在这里插入图片描述](https://img-blog.csdnimg.cn/505bd3acd38b4f1da3a59eb3d9020fff.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5bCP55m95YWU5aW257OWaQ==,size_18,color_FFFFFF,t_70,g_se,x_16)
这两个方法中，没有写路径