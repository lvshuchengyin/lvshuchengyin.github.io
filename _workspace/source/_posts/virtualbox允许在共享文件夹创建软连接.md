title: virtualbox允许在共享文件夹创建软连接
author: Lscy
tags:
  - windows
categories:
  - 编程
date: 2018-05-20 10:42:00
---
在virtualbox的共享文件夹中创建软连接会提示错误：
~~~ bash
cannot create symbolic link
~~~

原因：VirtualBox从安全角度出发，限制了软链接的创建，需要打开相应的Feature。
~~~ bash
VBoxManage setextradata YOURVMNAME VBoxInternal2/SharedFoldersEnableSymlinksCreate/YOURSHAREFOLDERNAME 1  
# YOURVMNAME为虚拟机中ubuntu系统的名称
# YOURSHAREFOLDERNAME 为共享的目录名称
 
# 例如：
C:\Program Files\Oracle\VirtualBox\VBoxManage setextradata ubuntu1404 VBoxInternal2/SharedFoldersEnableSymlinksCreate/share 1
~~~
设置完毕以管理者身份运行VirtualBox即可。