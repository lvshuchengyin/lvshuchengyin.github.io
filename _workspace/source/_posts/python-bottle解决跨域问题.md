title: python bottle解决跨域问题
author: Lscy
tags:
  - python
categories:
  - 编程
date: 2018-05-20 11:32:00
---
### 同意跨域
~~~ python
from bottle import route, run, template, Bottle, response
 
app = Bottle()
 
@app.hook('after_request')
def enable_cors():
    response.headers['Access-Control-Allow-Origin'] = '*'
    response.headers['Access-Control-Allow-Methods'] = 'GET, POST, PUT, OPTIONS'
    response.headers['Access-Control-Allow-Headers'] = 'Origin, Accept, Content-Type, X-Requested-With, X-CSRF-Token'
~~~