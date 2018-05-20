title: gevent超时逻辑
author: Lscy
tags:
  - python
categories:
  - 编程
date: 2018-05-20 10:31:00
---
~~~ python
from gevent import monkey
monkey.patch_all()
import time
import gevent
 
i = 0
with gevent.Timeout(2, False) as timeout:
    time.sleep(3)
    i = 1
print i
~~~