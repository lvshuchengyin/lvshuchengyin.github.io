title: nodejs npm包安装
author: Lscy
tags: []
categories: []
date: 2018-05-27 18:31:00
---
### 设置下载镜像地址
~~~ bash
# 国内地址
npm config set registry https://registry.cnpmjs.org
# 淘宝npm代理
npm config set registry https://registry.npm.taobao.org
# 安装包错误 npm ERR! Unexpected end of JSON input while parsing near...
# 则切换回国内代理或者清除缓存
npm cache clean --force
~~~
### 代理
~~~ bash
npm config set proxy http://127.0.0.1:1080
npm config delete proxy
~~~
### windows
~~~ bash
# 安装包时提示 MSBUILD : error MSB3428: 未能加载 Visual C++ 组件“VCBuild.exe”
# 则需要以管理员权限运行
npm install --global windows-build-tools
npm install -g node-gyp
~~~
### 安装sass
binding.node 下载地址：https://github.com/sass/node-sass/releases/
安装方法：
* set SASS_BINARY_SITE=https://npm.taobao.org/mirrors/node-sass/ && npm install node-sass
* set SASS_BINARY_PATH=D:\code\nodejs\bin\win32-x64-64_binding.node && npm install node-sass
