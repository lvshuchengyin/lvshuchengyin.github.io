title: beeline连接
author: Lscy
tags:
  - 服务组件
categories:
  - 编程
date: 2018-05-20 10:49:00
---
### 连接
~~~ bash
beeline -n hive -p hive -u jdbc:hive2://127.0.0.1:10000
~~~

### 执行
~~~ bash
/usr/bin/beeline --color=true --showHeader=true --outputformat=tsv2 -n hive -p hive -u jdbc:hive2://hiveserver2.simpledao.com:10000 -e "
set hive.merge.mapredfiles=true;
set hive.merge.mapfiles=true;
set hive.merge.smallfiles.avgsize=500000000;
set mapred.max.split.size=4000000000;
 
select * from table1 limit 10;"
~~~