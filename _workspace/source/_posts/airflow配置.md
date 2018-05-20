title: airflow配置
author: Lscy
tags:
  - 服务组件
categories:
  - 编程
date: 2018-05-20 10:46:00
---
### 修改数据库为mysql
~~~ text
sql_alchemy_conn = mysql://root:123@localhost:3066/airflow?charset=utf8
~~~

### 修改celery的broker为redis
~~~ text
broker_url = redis://localhost:6379/0
# rabbitmq: amqp://guest:guest@localhost:5672//
celery_result_backend =  redis://localhost:6379/0
~~~

### 添加user
~~~ python
import airflow
from airflow import models, settings
from airflow.contrib.auth.backends.password_auth import PasswordUser
user = PasswordUser(models.User())
user.username = 'test_user'
user.email = 'test_user@example.com'
user.password = 'test_user'
session = settings.Session()
session.add(user)
session.commit()
session.close()
exit()
~~~