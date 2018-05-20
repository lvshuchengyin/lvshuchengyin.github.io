title: python用gzip压缩string字符串，支持python2.6
author: Lscy
tags:
  - python
categories:
  - 编程
date: 2018-05-20 11:16:00
---
### 压缩
~~~ python
def gzip_compress(buf, compresslevel=6):
    out = StringIO.StringIO()
    f = gzip.GzipFile(fileobj=out, mode="w", compresslevel=compresslevel)
    f.write(buf)
    f.close()
    res = out.getvalue()
    return res
~~~

### 解压缩
~~~ python
def gzip_decompress(buf):
    obj = StringIO.StringIO(buf)
    f = gzip.GzipFile(fileobj=obj)
    result = f.read()
    f.close()
    return result
~~~