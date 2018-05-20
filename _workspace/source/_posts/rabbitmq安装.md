title: rabbitmq安装
author: Lscy
tags:
  - 服务组件
categories:
  - 编程
date: 2018-05-20 10:35:00
---
### 安装
~~~ bash
yum install erlang
rpm --import https://www.rabbitmq.com/rabbitmq-signing-key-public.asc
yum install rabbitmq-server
~~~

### 添加hostname
~~~ bash
vim /etc/hosts
# 添加一行：
127.0.0.1 rabbitmq-server
~~~

### 常用命令
~~~ bash
# 启动：
service rabbitmq-server start
# 停止：
service rabbitmq-server stop
# 重启：
service rabbitmq-server restart
# 设置开机启动：
chkconfig rabbitmq-server on
~~~
<!-- more -->
### 管理后台
~~~ bash
# 开启 Web 界面管理：
rabbitmq-plugins enable rabbitmq_management
http://rabbitmq-server:15672
~~~

### broker地址
~~~ bash
broker_url = amqp://guest:guest@localhost:5672/vhost
~~~

### python连接出错
Received and deleted unknown message.  Wrong destination?!?
~~~ bash
pip uninstall librabbitmq
~~~