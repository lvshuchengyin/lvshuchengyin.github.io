title: python编译安装
author: Lscy
tags:
  - python
categories:
  - 编程
date: 2018-05-20 11:15:00
---
### 依赖
~~~ bash
yum install zlib-devel bzip2-devel openssl-devel ncurses-devel sqlite-devel cyrus-sasl cyrus-sasl-devel
~~~

### 安装
~~~ bash
tar zxvf Python-2.7.3.tgz
cd Python-2.7.3
./configure
make && make install
~~~