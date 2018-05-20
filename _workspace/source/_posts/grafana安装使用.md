title: grafana安装使用
author: Lscy
tags:
  - 服务组件
categories:
  - 编程
date: 2018-05-20 11:22:00
---
### 安装
~~~ bash
wget https://s3-us-west-2.amazonaws.com/grafana-releases/release/grafana-4.3.2-1.x86_64.rpm 
sudo yum localinstall grafana-4.3.2-1.x86_64.rpm
~~~

### 配置文件
~~~ bash
/etc/grafana/grafana.ini
~~~

### 启动
~~~ bash
service grafana-server start
~~~

### 开机启动
~~~ bash
sudo systemctl enable grafana-server.service
~~~

### 设置template依赖选择参数
~~~ bash
$topic    SHOW TAG VALUES WITH KEY = "topic"    
$host    SHOW TAG VALUES WITH KEY = "host" WHERE "topic" =~ /^$topic$/
~~~