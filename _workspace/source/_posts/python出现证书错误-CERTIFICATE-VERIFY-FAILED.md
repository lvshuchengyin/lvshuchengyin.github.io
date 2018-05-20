title: python出现证书错误 CERTIFICATE_VERIFY_FAILED
author: Lscy
tags:
  - python
categories:
  - 编程
date: 2018-05-20 11:30:00
---
### django-cas或其它python程序，出现错误 CERTIFICATE_VERIFY_FAILED
~~~ text
SSL: CERTIFICATE_VERIFY_FAILED] certificate verify failed
 
# 增加代码，不检验自签名证书
import ssl
ssl._create_default_https_context = ssl._create_unverified_context
~~~