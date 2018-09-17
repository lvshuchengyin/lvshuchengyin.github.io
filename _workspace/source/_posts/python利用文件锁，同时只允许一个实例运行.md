title: python利用文件锁，同时只允许一个实例运行
author: Lscy
tags:
  - python
categories:
  - 编程
date: 2018-09-17 09:43:00
---
### 使用文件锁，支持linux和windows
~~~ python
import os
import sys
import time
import logging

logger = logging

class SingleInstance:
    def __init__(self):
        py_file_path = os.path.abspath(__file__)
        basepath = os.path.dirname(py_file_path)
        self.lockfile = os.path.normpath(basepath + '/' + os.path.basename(__file__) + '.lock')
        if sys.platform == 'win32':
            try:
                # file already exists, we try to remove (in case previous execution was interrupted)
                if os.path.exists(self.lockfile):
                    os.unlink(self.lockfile)

                self.fd = os.open(self.lockfile, os.O_CREAT | os.O_EXCL | os.O_RDWR)
            except OSError as e:
                if e.errno == 13:
                    logger.error("Another instance is already running, quit.")
                    sys.exit(-1)
                raise e
        else:
            # non Windows
            import fcntl

            self.fp = open(self.lockfile, 'w')
            try:
                fcntl.lockf(self.fp, fcntl.LOCK_EX | fcntl.LOCK_NB)
            except IOError:
                logger.error("Another instance is already running, quit.")
                sys.exit(-1)

if __name__ == '__main__':
    instance = SingleInstance()
    time.sleep(10)

~~~