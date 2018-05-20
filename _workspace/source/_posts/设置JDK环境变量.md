title: 设置JDK环境变量
author: Lscy
tags:
  - java
categories:
  - 编程
date: 2018-05-20 10:47:00
---
设置JDK的环境变量
~~~ bash
export JAVA_HOME=/opt/jdk1.7.0_79
export JRE_HOME=${JAVA_HOME}/jre
export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib
export PATH=${JAVA_HOME}/bin:$PATH
~~~