title: ie插件打包成cab文件使用和更新
author: Lscy
tags:
  - windows
categories:
  - 编程
date: 2018-05-20 10:23:00
---
### ie插件用ATL开发为dll后缀，用MFC开发为ocx后缀，打包的方法都一样。

### 打包步骤

* a.假如开发的插件文件名为：TransferAgent.dll。
<!-- more -->

* b.新建一个inf后缀的文本文件，例如为inf.inf,文件内容修改为：
 ~~~ text
[version] 
signature="$Chicago$"
AdvancedINF=2.0
[Add.Code]
TransferAgent.dll=TransferAgent.dll
[TransferAgent.dll]
file-win32-x86=thiscab
clsid={FD4972BA-686F-4F23-8EB4-9ACC62BA0FC9}
RegisterServer=yes
FileVersion=1.0.0.1
~~~
* c.主要参数说明

  上述的Add.Code中包含了所需的dll，如果有其它dll，可以自行添加，并且每一个dll都要另外进行说明，如上面的：[TransferAgent.dll]，特别注意的是要添加插件中组件的clsid，和FileVersion（即文件的版本号）。

* d.打包

  运行命令: CabArc.Exe -s 6144 n TransferAgent.cab TransferAgent.dll inf.inf

  (CabArc.Exe 可在vs2005目录中找到：C:\Program Files\Microsoft Visual Studio 8\Common7\Tools\Bin）。



### 插件使用

* a.在页面中设置插件：
~~~ html
<object id="ieplugin" codeBase="/TransferAgent.cab#Version=1,0,0,1"classid="clsid:FD4972BA-686F-4F23-8EB4-9ACC62BA0FC9"></object>
~~~
其中version和clsid都要和inf文件中的一致。

* b.Js调用
~~~ js
axobj = document.getElementById("ieplugin");
axobj.Test();  //Test为插件的一个函数。
~~~
### 插件更新

		重新编译插件时要注意修改插件的版本号，并且同时修改inf文件中的版本号，和页面元素的版本号。这样当ie加载页面时，发现版本号已修改，则会重新下载插件安装，实现自动更新。