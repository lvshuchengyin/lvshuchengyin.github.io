title: kafka常用命令
author: Lscy
tags:
  - 服务组件
categories:
  - 编程
date: 2018-05-20 10:48:00
---
### 查看topic列表
~~~ bash
kafka-topics --zookeeper 127.0.0.1 --list
~~~

### 修改分区数
~~~ bash
kafka-topics --zookeeper 127.0.0.1  --alter --topic topic1 --partitions 16
~~~