title: 'python xml,html转义字符'
author: Lscy
tags:
  - python
categories:
  - 编程
date: 2018-05-20 11:24:00
---
### xml转义字符
~~~ python
from xml.sax.saxutils import escape
def xmlescape(data):
    if data is None:
        data = ''
    elif not isinstance(data, str):
        data = str(data)
    return escape(data, entities={"'": "&apos;", '"': "&quot;"})
~~~

### html转义字符
~~~ python
def html_escape(s):
    htmlcodes = (
        ('&', '&amp;'),
        ("'", '&#39;'),
        ('"', '&quot;'),
        ('>', '&gt;'),
        ('<', '&lt;'),
    )
    for code in htmlcodes:
        s = s.replace(code[0], code[1])
    return s
~~~