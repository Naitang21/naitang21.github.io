---
layout: fragment
title: conda常用命令
tags: Python 
description: conda常用命令
keywords: Python Conda
typora-root-url: ..
---



1. 查看安装了哪些包

```
conda list
//也可以使用pip list
```

2. 查看当前存在哪些虚拟环境

```
conda env list 
conda info -e
```

3. 检查更新当前conda
```
conda update conda
```
4. Python创建虚拟环境
```
conda create -n your_env_name python=x.x
```

anaconda命令创建python版本为x.x，名字为your_env_name的虚拟环境。your_env_name文件可以在Anaconda安装目录envs文件下找到。

5. 激活或者切换虚拟环境

打开命令行，输入python --version检查当前 python 版本。

Linux:  `source activate your_env_nam`
Windows: `activate your_env_name`
6. 对虚拟环境中安装额外的包
```
conda install -n your_env_name [package]
```
7. 关闭虚拟环境(即从当前环境退出返回使用PATH环境中的默认python版本)
```
deactivate env_name
```
或者`activate root`切回root环境
Linux下：source deactivate 

8. 删除虚拟环境
```
conda remove -n your_env_name --all
```
9. 删除环境钟的某个包
```
conda remove --name $your_env_name  $package_name 
```
10. 设置国内镜像
http://Anaconda.org的服务器在国外，安装多个packages时，conda下载的速度经常很慢。清华TUNA镜像源有Anaconda仓库的镜像，将其加入conda的配置即可：
```
//添加Anaconda的TUNA镜像

conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/

// TUNA的help中镜像地址加有引号，需要去掉

//设置搜索时显示通道地址

conda config --set show_channel_urls yes
```

11. 恢复默认镜像
```
conda config --remove-key channels
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTkxOTc5NzMzMl19
-->