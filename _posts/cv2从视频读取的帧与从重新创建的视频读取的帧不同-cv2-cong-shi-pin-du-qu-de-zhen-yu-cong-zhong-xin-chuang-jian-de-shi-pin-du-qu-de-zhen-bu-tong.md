---
title: cv2从视频读取的帧与从重新创建的视频读取的帧不同
date: 2023-01-02 16:33:15.274
updated: 2023-01-02 16:33:15.274
url: /archives/cv2-cong-shi-pin-du-qu-de-zhen-yu-cong-zhong-xin-chuang-jian-de-shi-pin-du-qu-de-zhen-bu-tong
categories: 
tags: python
---

对于MP4，因为它们使用有损编码来写入视频数据。 所以无法在两个视频之间获得精确的逐像素匹配。如果要获得完全匹配，则需要使用无损编解码器--使用PNG编码将视频帧写入文件

可参考[以下链接](以下链接)