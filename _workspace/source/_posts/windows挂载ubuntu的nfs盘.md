title: windows挂载ubuntu的nfs盘
author: Lscy
tags:
  - windows
categories:
  - 编程
date: 2018-05-20 10:44:00
---
### 安装Ubuntu nfs
~~~ bash
sudo apt-get install nfs-kernel-server
~~~

### 配置/etc/exports

允许挂载的目录及权限在文件/etc/exports中进行定义。
~~~ bash

# 例如要共享目录/var/www，需要在/etc/exports文件末尾添加如下一行
/var/www *(rw,sync,no_root_squash)
 
# /var/www是要共享的目录
# *代表允许所有的网络段访问
# rw是可读写权限
# sync是资料同步写入内存和硬盘
# no_root_squash是Ubuntu nfs客户端分享目录使用者的权限,
#    如果客户端使用的是root用户，那么对于该共享目录而言，该客户端就具有root权限
~~~
<!-- more -->
### 重启nfs服务
~~~ bash
sudo /etc/init.d/nfs-kernel-server restart
~~~

### 显示挂载盘
~~~ bash
showmount -e
~~~

### windows下连接ubuntu的nfs盘
~~~ bash
mount \\127.0.0.1\var\www x:\
 
# 127.0.0.1需替换为ubuntu的ip
# \var\www为共享的目录
# x:\为挂载到windows的x盘
 
# 打开我的电脑，即可看到ubuntu共享的x盘
~~~

### windows取消挂载
~~~ bash
umount -a
~~~