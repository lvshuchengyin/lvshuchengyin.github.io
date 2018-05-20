title: 使用virtualenv隔离python环境
author: Lscy
tags:
  - python
categories:
  - 编程
date: 2018-05-19 15:26:00
---
### 安装virtualenv
~~~ bash
apt-get install python-virtualenv
~~~
### 安装扩展包，Virtaulenvwrapper是virtualenv的扩展包，用于更方便管理虚拟环境
~~~ bash
pip install virtualenvwrapper
~~~
<!-- more -->
### 设置环境，在~/.bashrc中添加
~~~ bash
source /usr/local/bin/virtualenvwrapper.sh
~~~
设置完后要运行一次：
~~~ bash
source /usr/local/bin/virtualenvwrapper.sh
~~~
### 常用命令
~~~ bash
#创建一个tmp的环境
mkvirtualenv tmp
#切换到tmp的环境
workon tmp
#退出环境
deactivate
#移除虚拟环境tmp
rmvirtualenv tmp
~~~
### uwsgi中配置使用virtualenv中安装的包：
~~~ bash
#只要告诉uwsgi，virtualenv创建的虚拟目录路径
virtualenv=/home/tmpuser/.virtualenvs/tmp
~~~