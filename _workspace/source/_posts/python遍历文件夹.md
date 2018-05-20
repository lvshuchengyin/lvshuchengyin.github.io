title: python遍历文件夹
author: Lscy
tags:
  - python
categories:
  - 编程
date: 2018-05-20 10:29:00
---
followlinks表示是否扫描软连接，topdown是否广度遍历
~~~ python
def get_file_path(dir_path):
    """获取文件夹下面的所有文件，包括子文件夹"""
    file_list = os.walk(dir_path, topdown=True, onerror=None, followlinks=False)
    for root, dirs, files in file_list:
        for f in files:
            path = os.path.join(root, f)
            yield path.replace('\\', '/')
~~~