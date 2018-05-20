title: linux date命令
author: Lscy
tags:
  - linux
categories:
  - 编程
date: 2018-05-20 10:53:00
---
### date格式化
~~~ bash
date +%Y-%m-%dT%H:%M:%S
~~~

### 昨天
~~~ bash
date -d "yesterday 13:00" '+%Y-%m-%d'
~~~