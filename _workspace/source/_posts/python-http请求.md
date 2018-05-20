title: python http请求
author: Lscy
tags:
  - python
categories:
  - 编程
date: 2018-05-20 10:50:00
---
http请求
~~~ python
def open_url(url, method='GET', headers=None, postform=None, postdata=None, timeout=10):
    """http请求"""
    try:
        if headers is None:
            headers = {}
        if postform is None:
            postform = {}
 
        if len(postform) > 0:
            data = urllib.urlencode(postform)
            headers['Content-Type'] = 'application/x-www-form-urlencoded'
        else:
            data = postdata
 
        req = urllib2.Request(url=url, data=data, headers=headers)
        req.get_method = lambda: method.upper()
        res = urllib2.urlopen(req, timeout=timeout)
        data = res.read()
        res.close()
        return res.code, res.headers, data
    except urllib2.HTTPError, e:
        data = e.read()
        e.close()
        return e.code, e.headers, data
    except Exception:
        log = traceback.format_exc().replace('\n', ' ')
        return 500, {}, log
~~~