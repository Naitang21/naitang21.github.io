---
layout: fragment
title: BeanCreationException: Error creating bean with name xxx
tags: Bug
description: BeanCreationException: Error creating bean with name xxx
keywords: Bug
typora-root-url: ..
mermaid: false
sequence: false
flow: false
mathjax: false
mindmap: false
mindmap2: false
---

```
org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'xxxSvcClientConfiguration': Injection of autowired dependencies failed; nested exception is java.lang.IllegalArgumentException: Could not resolve placeholder 'xxx-service.application-service-id' in value "${xxx-service.application-service-id}"



Caused by: java.lang.IllegalArgumentException: Could not resolve placeholder 'xxx-service.application-service-id' in value "${xxx-service.application-service-id}"


Exception in thread "Thread-2" zipkin2.reporter.ClosedSenderException
	at zipkin2.reporter.AsyncReporter$BoundedAsyncReporter.flush(AsyncReporter.java:265)
	at org.springframework.cloud.sleuth.autoconfig.zipkin2.ZipkinAutoConfiguration$2.run(ZipkinAutoConfiguration.java:142)
Disconnected from the target VM, address: '127.0.0.1:53279', transport: 'socket'

```
```
[Error][ConfigAgent] class java.io.FileNotFoundException - Exception when loading environment variable: null
java.io.FileNotFoundException: manifest\LOCAL_env_config.json (The system cannot find the path specified)
```
在application配置中没有加working directory
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTc5NzMwNDQxM119
-->