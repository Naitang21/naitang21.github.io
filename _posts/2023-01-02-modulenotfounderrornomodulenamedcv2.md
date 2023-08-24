---
layout: post
title: No module named 'cv2'
categories: Bug Python
description: No module named 'cv2'
keywords: Python Bug
typora-root-url: ..
---

**出错原因**
很明显是缺少了cv2模块

**解决方法**

- pip install opencv-python   （如果只用主模块，使用这个命令安装）
- pip install opencv-contrib-python （如果需要用主模块和contrib模块，使用这个命令安装）

如果需要指定版本安装，则可以使用
pip install package-name=版本号