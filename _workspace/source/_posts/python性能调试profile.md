title: python性能调试profile
author: Lscy
tags:
  - python
categories:
  - 编程
date: 2018-05-20 11:02:00
---
### 工具
* cProfile：基于lsprof的用C语言实现的扩展应用，运行开销比较合理，适合分析运行时间较长的程序
* profile：纯Python实现的性能分析模块，接口和cProfile一致。但在分析程序时增加了很大的运行开销。不过，如果想扩展profiler的功能，可以通过继承这个模块实现

### 基本用法
~~~ python
python -m cProfile -s cumulative test.py
~~~

### 结果说明
* ncalls：表示函数调用的次数
* tottime：表示指定函数的总的运行时间，除掉函数中调用子函数的运行时间
* percall：（第一个percall）等于 tottime/ncalls
* cumtime：表示该函数及其所有子函数的调用运行的时间，即函数开始调用到返回的时间
* percall：（第二个percall）即函数运行一次的平均时间，等于 cumtime/ncalls
* filename:lineno(function)：每个函数调用的具体信息
另外，上面分析的时候，排序方式使用的是函数调用时间(cumulative)，
还有其它排序方式：calls, cumulative, file, line, module, name, nfl, pcalls, stdname, time
