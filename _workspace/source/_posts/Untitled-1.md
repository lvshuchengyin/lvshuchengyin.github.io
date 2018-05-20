title: 'linux设置虚拟内存 '
author: Lscy
tags:
  - linux
categories:
  - 编程
date: 2018-05-20 09:45:00
---
### 决定修改swap大小
首先在空间合适处创建用于分区的swap文件
~~~ bash
dd if=/dev/zero of=/swap/swap bs=1024 count=4194304
~~~

### 将目的文件设置为swap分区文件
~~~ bash
mkswap /swap/swap
~~~
<!-- more -->
### 激活swap，立即启用交换分区文件
~~~ bash
swapon /swap/swap
~~~

### 查看
~~~ bash
free -m
~~~

### 开机时自启用
修改文件/etc/fstab中的swap行
~~~ bash
/swap/swap  swap  swap  defaults  0 0
~~~