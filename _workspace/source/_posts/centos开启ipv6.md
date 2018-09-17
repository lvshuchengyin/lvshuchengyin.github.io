title: centos开启ipv6
author: Lscy
tags:
  - linux
categories:
  - 编程
date: 2018-09-17 09:21:00
---
### 编辑/etc/sysconfig/network-scripts/ifcfg-eth0，添加
~~~ text
IPV6INIT=yes
IPV6ADDR=primary_ipv6_address/64
IPV6_DEFAULTGW=ipv6_gateway
IPV6_AUTOCONF=no
DNS1=2001:4860:4860::8844
DNS2=2001:4860:4860::8888
DNS3=209.244.0.3
~~~
### 测试
~~~ bash
ping6 2001:4860:4860::8888
~~~
### 参考
~~~
https://www.digitalocean.com/community/tutorials/how-to-enable-ipv6-for-digitalocean-droplets
~~~