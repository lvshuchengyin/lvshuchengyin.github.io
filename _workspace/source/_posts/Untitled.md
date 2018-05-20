title: supervisor配置
author: Lscy
tags:
  - linux
categories:
  - 编程
date: 2018-05-20 09:50:00
---
### 安装
~~~ bash
pip install supervisor
~~~

### 生成配置文件
~~~ bash
echo_supervisord_conf > /home/stat/venv/web/etc/supervisord.conf
~~~
<!-- more -->
### 配置gunicorn的运行程序
~~~ text
[program:myapp]
command=/home/stat/venv/web/bin/gunicorn -w4 -b0.0.0.0:2170 myapp:app
directory=/path/myproject
autorestart=true
~~~

### 常用命令
指定配置文件则加上 -c supervisord.conf
~~~ bash
# 通过配置文件启动supervisor
supervisord
# 察看supervisor的状态
supervisorctl status
# 重新载入配置文件
supervisorctl reload
# 启动指定/所有supervisor管理的程序进程
supervisorctl start [all]|[appname]
# 关闭指定/所有 supervisor管理的程序进程
supervisorctl stop [all]|[appname]
~~~

### web管理界面(需要激活)
~~~ text
[inet_http_server]        ; inet (TCP) server disabled by default
port=127.0.0.1:9001       ; (ip_address:port specifier, *:port for all iface)
username=user          ; (default is no username (open server))
password=123           ; (default is no password (open server))
 
[supervisorctl]
serverurl=unix:///tmp/supervisor.sock ; use a unix:// URL  for a unix socket
serverurl=http://127.0.0.1:9001       ; use an http:// url to specify an inet socket
username=user             ; should be same as http_username if set
password=123              ; should be same as http_password if set
;prompt=mysupervisor          ; cmd line prompt (default "supervisor")
;history_file=~/.sc_history          ; use readline history if available
~~~