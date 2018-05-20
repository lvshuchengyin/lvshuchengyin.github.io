title: influxdb安装
author: Lscy
tags:
  - 服务组件
categories:
  - 编程
date: 2018-05-20 11:18:00
---
### influxdb
~~~ bash
wget https://dl.influxdata.com/influxdb/releases/influxdb-1.2.4.x86_64.rpm
sudo yum localinstall influxdb-1.2.4.x86_64.rpm
~~~

### chronograf
~~~ bash
wget https://dl.influxdata.com/chronograf/releases/chronograf-1.3.2.1.x86_64.rpm
sudo yum localinstall chronograf-1.3.2.1.x86_64.rpm
~~~

### influxdb配置文件
~~~ bash
/etc/influxdb/influxdb.conf
~~~

### 命令
~~~ bash
service influxdb start
~~~

### 创建数据保存策略
~~~ bash
CREATE RETENTION POLICY "roll" ON "dc" DURATION 3d REPLICATION 1 DEFAULT
ALTER RETENTION POLICY "roll" ON "dc" DURATION 3d REPLICATION 1 SHARD DURATION 6h DEFAULT
~~~

### 常用命令
~~~ bash
# 查看series
influx -port 10086 -database dc -execute 'show series'
~~~