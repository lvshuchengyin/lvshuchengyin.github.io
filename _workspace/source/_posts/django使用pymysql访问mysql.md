title: django使用pymysql访问mysql
author: Lscy
tags:
  - python
categories:
  - 编程
date: 2018-05-20 11:31:00
---
### 在manage.py和wsgi.py顶部增加代码
~~~ python
import pymysql
pymysql.install_as_MySQLdb()
~~~