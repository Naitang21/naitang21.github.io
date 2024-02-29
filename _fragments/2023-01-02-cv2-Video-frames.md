---
layout: fragment
title: cv2从视频读取的帧与从重新创建的视频读取的帧不同
tags: Python
description: cv2从视频读取的帧与从重新创建的视频读取的帧不同
keywords: Python
typora-root-url: ..
---

对于MP4，因为它们使用有损编码来写入视频数据。 所以无法在两个视频之间获得精确的逐像素匹配。如果要获得完全匹配，则需要使用无损编解码器--使用PNG编码将视频帧写入文件

可参考[以下链接](以下链接)
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTY5NTg3NzM3OV19
-->