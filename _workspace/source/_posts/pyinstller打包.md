title: pyinstller打包
author: Lscy
tags:
  - python
categories:
  - 编程
date: 2018-05-20 10:38:00
---
### 安装
~~~ bash
pip install pyinstaller
~~~
<!-- more -->
### 参数说明
~~~ text
#构建前清除缓存和临时文件
--clean 
#指定日志级别 DEBUG, INFO, WARN, ERROR, CRITICAL
--log-level 
#构建的可执行文件和其它依赖文件放在同一个目录下（默认值）
-D, --onedir 
#全部依赖都包到一个巨大的exe文件中，不过经过实践，有时候windows会报格式错误，造成程序无法执行
-F, --onefile 
#指定程序名称
-n NAME, --name NAME 
#设置搜索的导入路径，可以用路径分隔符，windows用分号，linux用冒号，分隔指定多个目录，也可以使用多个-p分别指定
-p DIR, --paths DIR 
#不使用upx去压缩文件，因为经过实践，有时候windows会报格式错误，造成程序无法执行
--noupx 
#默认会打开控制台显示标准输出
-c, --console, --nowindowed 
#不显示控制台，制作窗口程序
-w, --windowed, --noconsole 
#Any Shared Assemblies bundled into the application will be changed into Private Assemblies. 
#This means the exact versions of these assemblies will always be used, 
#and any newer versions installed on user machines at the system level will be ignored. 
#只会使用私有的动态链接库
--win-private-assemblies 
#指定程序图标
--icon
~~~
### 打包pyqt5的示例

由于pyqt5只支持python3.5以上，并且pyinstaller支持3.5，则选用python3.5，另外py2exe不支持3.5，因此无法用py2exe打包pyqt5。

pyinstaller -w --noupx --clean --win-private-assemblies --path C:\Users\P\AppData\Local\Programs\Python\Python35-32\Lib\site-packages\PyQt5\Qt\bin main.py
出现error loading dll python35.dll error code=193，很可能是因为dll32位和64位不对应，或者是缺少dll，例如api-ms-win-crt*开头的dll

http://stackoverflow.com/questions/33265663/api-ms-win-crt-runtime-l1-1-0-dll-is-missing-when-opening-microsoft-office-file