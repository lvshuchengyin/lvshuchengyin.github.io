title: python 序列化json 包含中文
author: Lscy
tags:
  - python
categories:
  - 编程
date: 2018-05-20 11:23:00
---
包含中文
~~~ python
html_dict = {'key': 'value'}
json_str = json.dumps(html_dict, ensure_ascii=False, encoding='utf-8')
~~~