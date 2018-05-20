title: linux有序查看进程打开的文件描述符数量
author: Lscy
tags:
  - linux
categories:
  - 编程
date: 2018-05-20 11:25:00
---
### lsof
~~~ bash
lsof -n | awk '{print $2}'| sort | uniq -c | sort -nr | more
~~~