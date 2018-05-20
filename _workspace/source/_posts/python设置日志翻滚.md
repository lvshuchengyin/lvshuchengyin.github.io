title: python设置日志翻滚
author: Lscy
tags:
  - python
categories:
  - 编程
date: 2018-05-20 10:52:00
---
### 可翻滚的日志: logger.py
~~~ python
# -*- coding: utf-8 -*-
import os
import logging
from logging.handlers import RotatingFileHandler
 
def get_full_path(local_path):
    file_path = os.path.abspath(__file__)
    base_path = os.path.dirname(file_path)
    return os.path.join(base_path, local_path)
     
LOG_LEVEL = logging.DEBUG
LOG_FORMAT = '%(asctime)s %(levelname)s [%(filename)s:%(funcName)s:%(lineno)s] %(message)s'
DATEFMT = '%Y-%m-%d %H:%M:%S'
LOG_FILE_NAME = get_full_path('logs/app.log')
LOG_FILE_MAX_SIZE = 10 * 1024 * 1024
LOG_FILE_BACKUP_COUNT = 5
 
formatter = logging.Formatter(LOG_FORMAT, datefmt=DATEFMT)
 
console = logging.StreamHandler()
console.setFormatter(formatter)
 
rotate = RotatingFileHandler(LOG_FILE_NAME, maxBytes=LOG_FILE_MAX_SIZE, backupCount=LOG_FILE_BACKUP_COUNT)
rotate.setFormatter(formatter)
 
logger = logging.getLogger('app_common')
logger.propagate = False
logger.setLevel(LOG_LEVEL)
logger.addHandler(console)
logger.addHandler(rotate)
~~~

### 使用方法
~~~ python
from logger import logger
 
logger.info('log')
~~~