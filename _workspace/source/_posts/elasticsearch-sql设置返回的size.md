title: elasticsearch-sql设置返回的size
author: Lscy
tags:
  - 服务组件
categories:
  - 编程
date: 2018-05-20 11:38:00
---
elasticsearch-sql 默认返回的size是200，10。

可以在查询的时候显式设置size：
~~~ sql
SELECT  SUM(succ) AS s FROM test1 GROUP BY terms(field='domain',size='1000',alias='domain'), terms(field='server',size='1000',alias='server')
~~~