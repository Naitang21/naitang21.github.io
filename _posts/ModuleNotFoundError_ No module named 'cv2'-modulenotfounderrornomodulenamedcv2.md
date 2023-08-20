---
title: ModuleNotFoundError: No module named 'cv2'
date: 2023-01-02 15:50:21.526
updated: 2023-01-02 15:54:17.78
url: /archives/modulenotfounderrornomodulenamedcv2
categories: 
tags: bug合集 | python
---

**出错原因**
很明显是缺少了cv2模块

**解决方法**
- pip install opencv-python   （如果只用主模块，使用这个命令安装）
- pip install opencv-contrib-python （如果需要用主模块和contrib模块，使用这个命令安装）

如果需要指定版本安装，则可以使用
pip install package-name=版本号
