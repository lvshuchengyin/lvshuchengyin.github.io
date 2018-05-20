title: 'pssh,pscp工具使用'
author: Lscy
tags:
  - linux
categories:
  - 编程
date: 2018-05-20 11:21:00
---
### pssh在多个主机上并行地运行命令
~~~ text
-h 执行命令的远程主机列表,文件内容格式[user@]host[:port] 如 test@172.16.10.10:229
-H 执行命令主机，主机格式 user@ip:port
-l 远程机器的用户名
-p 一次最大允许多少连接
-P 执行时输出执行信息
-o 输出内容重定向到一个文件
-e 执行错误重定向到一个文件
-t 设置命令执行超时时间
-A 提示输入密码并且把密码传递给ssh(如果私钥也有密码也用这个参数)
-O 设置ssh一些选项
-x 设置ssh额外的一些参数，可以多个，不同参数间空格分开
-X 同-x,但是只能设置一个参数
-i 显示标准输出和标准错误在每台host执行完毕后
 
pssh -H stat@192.168.1.100:18822 -i -A "ls -l"
~~~

### pscp
~~~ bash
pscp -h ip文件 本地文件 远程目录
pscp -h hosts.txt -l root -r /tmp/i.txt /tmp
~~~