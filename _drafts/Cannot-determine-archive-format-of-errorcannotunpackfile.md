---
title:  ERROR: Cannot unpack file 或 ERROR: Cannot determine archive format of
date: 2023-01-02 16:29:35.0
updated: 2023-01-02 16:30:04.916
url: /archives/errorcannotunpackfile
categories: 
tags: bug合集 | python
---

出错
```
 ERROR: Cannot unpack file C:\Users\ZHANGW~1\AppData\Local\Temp\pip-unpack-ikp51qe3\simple.htm (downloaded from C:\Users\ZHANGW~1\AppData\Local\Temp\pip-req-build-7u4k70qf, content-type: text/html); cannot detect archive format
ERROR: Cannot determine archive format of C:\Users\ZHANGW~1\AppData\Local\Temp\pip-req-build-7u4k70qf


```

**解决方法**
设置信任该镜像
```

pip install -i http://pypi.douban.com/simple/ --trusted-host pypi.douban.com pakegename
```

常用国内镜像网站
阿里云 http://mirrors.aliyun.com/pypi/simple

豆瓣 http://pypi.douban.com/simple

清华大学 https://pypi.tuna.tsinghua.edu.cn/simple

中国科技大学 http://pypi.mirrors.ustc.edu.cn/simple

网易云 https://mirrors.163.com/pypi/simple


