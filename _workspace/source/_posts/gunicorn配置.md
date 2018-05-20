title: 'gunicorn配置 '
author: Lscy
tags:
  - linux
categories:
  - 编程
date: 2018-05-20 10:03:00
---
### 启动
~~~ bash
gunicorn --workers=4 mysite.wsgi:application
     --bind=127.0.0.1:8000 
     --bind=[::1]:8000
     --worker-class=gevent 
     --worker-connections=1000
     --env DJANGO_SETTINGS_MODULE=myproject.settings.main
~~~