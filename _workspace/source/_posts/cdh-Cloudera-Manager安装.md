title: cdh-Cloudera Manager安装
author: Lscy
tags:
  - 服务组件
categories:
  - 编程
date: 2018-05-20 11:05:00
---
### 安装
~~~ bash
wget http://archive.cloudera.com/cm5/installer/latest/cloudera-manager-installer.bin
chmod u+x cloudera-manager-installer.bin
sudo ./cloudera-manager-installer.bin
~~~

### 服务命令
~~~ bash
service cloudera-scm-server start|stop|restart
service cloudera-scm-agent start|stop|restart
~~~