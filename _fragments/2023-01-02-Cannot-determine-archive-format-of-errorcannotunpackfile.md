---
layout: fragment
title: Cannot unpack file or Cannot determine archive format of
tags: Bug
description:
typora-root-url: ..
---

出错

![image-20230824235057917](/images/posts/2023-01-02-Cannot-determine-archive-format-of-errorcannotunpackfile/image-20230824235057917.png)

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


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE4NzQ3MjUxMzVdfQ==
-->