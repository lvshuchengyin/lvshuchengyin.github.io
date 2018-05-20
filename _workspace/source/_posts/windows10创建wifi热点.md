title: 'windows10创建wifi热点 '
author: Lscy
tags:
  - windows
categories:
  - 编程
date: 2018-05-20 10:01:00
---
### 启动
~~~ bash
netsh wlan set hostednetwork mode=allow ssid=wifiname key=12345678
netsh wlan start hostednetwork
~~~
<!-- more -->
### 设置联网

* a.在“网络连接”界面中，右击“宽带连接”或“本地连接”图标，从弹出的右键菜单中选择“属性”项
* b.此时将打开“属性”界面，切换到“共享”选项卡
* c.勾选“允许其它网络用户通过此计算机的Internet连接来连接”项
* d.同时从家庭网络连接下拉列表中选择“本地连接*1”（即新创建的WiFi热点），点击“确定”完成设置
### 关闭
~~~ bash
netsh wlan set hostednetwork mode=disallow
~~~