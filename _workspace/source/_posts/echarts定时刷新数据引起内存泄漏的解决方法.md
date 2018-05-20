title: echarts定时刷新数据引起内存泄漏的解决方法
author: Lscy
tags:
  - js
categories:
  - 编程
date: 2018-05-20 11:24:00
---
### 先销毁，再更新
~~~ js
var chart = echarts.getInstanceByDom(document.getElementById(chart_id));
echarts.dispose(chart);
chart = echarts.init(document.getElementById(chart_id));
chart.setOption(option);
~~~