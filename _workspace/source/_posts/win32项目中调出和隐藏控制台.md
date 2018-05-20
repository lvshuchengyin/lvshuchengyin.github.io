title: win32项目中调出和隐藏控制台
author: Lscy
tags:
  - windows
categories:
  - 编程
date: 2018-05-20 10:20:00
---
### 显示控制台，并且能用print打印显示，方便调试
~~~ cpp
::AllocConsole();
::SetConsoleTitle(_T("测试控制台"));
freopen("conin$","r+t",stdin);
freopen("conout$","w+t",stdout);
freopen("conerr$","w+t",stderr);
//释放
FreeConsole();
~~~

### win32控制台工程隐藏dos窗口
~~~ cpp
#pragma comment( linker, "/subsystem:windows /entry:mainCRTStartup" )
~~~