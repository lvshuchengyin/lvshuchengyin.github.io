title: gevent协程
author: Lscy
tags:
  - python
categories:
  - 编程
date: 2018-05-20 10:30:00
---
### 模拟多线程运行
~~~ python
from gevent import monkey
monkey.patch_all()
import gevent
 
def foo():
    print('Running in foo')
    gevent.sleep(0)
    print('Explicit context switch to foo again')
 
def bar():
    print('Explicit context to bar')
    gevent.sleep(0)    
    print('Implicit context switch back to bar')
 
gevent.joinall([
    gevent.spawn(foo),
    gevent.spawn(bar),
])
~~~