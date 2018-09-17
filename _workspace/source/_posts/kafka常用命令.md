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
### 创建topic
~~~ bash
kafka-topics.sh --create --zookeeper 127.0.0.1:2181/kafkastreaming --replication-factor 2 --partitions 24 --topic test 
~~~
### 删除topic
~~~ bash
kafka-topics.sh --delete --zookeeper 127.0.0.1:2181/kafkastreaming --topic test
~~~
### 修改分区数
~~~ bash
kafka-topics --zookeeper 127.0.0.1  --alter --topic topic1 --partitions 16
~~~
### 生产
~~~ bash
kafka-console-producer.sh --broker-list 127.0.0.1:9092 --topic test
~~~
### 消费
~~~ bash
kafka-console-consumer.sh --bootstrap-server 127.0.0.1:9092 --topic test --from-beginning
~~~