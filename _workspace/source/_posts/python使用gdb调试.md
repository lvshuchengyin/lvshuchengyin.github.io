title: python使用gdb调试
author: Lscy
tags:
  - python
categories:
  - 编程
date: 2018-05-20 10:57:00
---
### 调试运行进程
~~~ bash
gdb -p pid
~~~

### 增加libpython来获取更多调试信息
* a)下载python2.7的源码中的Tools/gdb/libpython.py
* b)引入libpython.py
~~~ text
# 在gdb -p pid之后运行
(gdb) python
>import sys
>sys.path.append('/path/to/libpython.py')
>import libpython
>end
(gdb)
~~~
* c)之后可使用命令
~~~ bash
py-bt py-bt-full py-down py-list py-locals py-print py-up
~~~
注：python2.6的源码中提供了部分预定义函数以便大家使用gdb调试，我们只需将文件Python-2.6/Misc/gdbinit所包括的内容加入到用户目录下的.gdbinit文件中即可，这样每次启动gdb时会自动完成这些宏的定义。但可惜的是Python2.6.2 gdbini对于pylocals的定义居然有错误， 看来是没有随着代码的更新而同步更新。我们只需将 while $_i < f->f_nlocals修改为 while $_i < f->f_code->co_nlocals即可。