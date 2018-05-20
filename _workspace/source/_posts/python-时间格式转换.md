title: python 时间格式转换
author: Lscy
tags:
  - python
categories:
  - 编程
date: 2018-05-20 10:54:00
---
### datetime和str
~~~ python
# str转datetime
datetime.datetime.strptime('2017-04-23 00:00:00', '%Y-%m-%d %H:%M:%S')
# datetime转str
datetime.datetime.now().strftime('%Y-%m-%d %H:%M:%S');
# datetime转timestamp
time.mktime(dt.timetuple())
~~~

### utc时间转本地时间
~~~ python
from_zone = tz.tzutc()
to_zone = tz.tzlocal()
utc = datetime.strptime(utcs, '%Y-%m-%dT%H:%M:%SZ')
utc = utc.replace(tzinfo=from_zone)
local_dt = utc.astimezone(to_zone)
dts = local_dt.strftime('%Y-%m-%d %H:%M')
~~~

### datetime转timestamp
~~~ python
datetime.fromtimestamp(ts)
datetime.utcfromtimestamp(ts)
~~~