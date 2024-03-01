---
layout: fragment
title: FileNotFoundException - manifest\LOCAL_env_config.json
tags: Java
description: FileNotFoundException - manifest\LOCAL_env_config.json
keywords: Java
typora-root-url: ..
---

启动项目时，出现以下错误：
```
[Error][ConfigAgent] class java.io.FileNotFoundException - manifest\LOCAL_env_config.json (The system cannot find the path specified): null java.io.FileNotFoundException: manifest\LOCAL_env_config.json (The system cannot find the path specified)
```
有两种情况：
1. manifest目录下确实没有LOCAL_env_config.json这个文件（但一般不会是这个原因）
2. 程序运行时的工作目录不是预期的路径，但是相对路径`manifest\LOCAL_env_config.json`不正确
针对第二种情况，可以使用以下命令来打印出当前的目录，检查是否正确
```
System.out.println(new File(".").getAbsolutePath());
```

如果不正确，可能确实配置`work directory`


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE1MDMzOTk1OTRdfQ==
-->