title: curl
author: Lscy
tags:
  - linux
categories:
  - 编程
date: 2018-05-20 10:51:00
---
### post json
~~~ bash
curl -H "Content-Type: application/json" -X POST -d '{"a":"b","c":10}' http://127.0.0.1 -w %{time_connect}:%{time_starttransfer}:%{time_total}
~~~

### post form
~~~ bash
curl -d "param1=value1&param2=value2" "http://127.0.0.1/test"
~~~