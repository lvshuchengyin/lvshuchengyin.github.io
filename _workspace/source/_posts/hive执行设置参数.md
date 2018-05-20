title: hive执行设置参数
author: Lscy
tags:
  - 服务组件
categories:
  - 编程
date: 2018-05-20 10:38:00
---
### 参数
~~~ bash
set hive.merge.mapredfiles=true;
set hive.merge.mapfiles=true;
set hive.merge.smallfiles.avgsize=500000000;
set mapred.max.split.size=4000000000;
~~~