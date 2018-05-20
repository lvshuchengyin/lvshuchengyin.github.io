title: shadowshocks配置
author: Lscy
tags:
  - linux
categories:
  - 编程
date: 2018-05-20 10:42:00
---
### 服务端
~~~ bash
ssserver -p 6001 -k 123456abc -m aes-256-cfb -s 0.0.0.0 -v
~~~

### 客户端
~~~ bash
sudo sslocal -s 127.0.0.1 -p 6001 -k 123456abc -m aes-256-cfb -v
~~~