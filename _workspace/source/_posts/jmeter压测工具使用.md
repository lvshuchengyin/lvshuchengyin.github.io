title: jmeter压测工具使用
author: Lscy
tags:
  - java
categories:
  - 编程
date: 2018-05-20 11:20:00
---
### 安装

在官网下载压缩包，解压后进入文件夹即可
### 配置jmx
先在windows下执行 bin/jmeter.bat，
在图形界面下配置好参数，然后保存配置jmx文件

### 在linux上执行
~~~ bash
# 启动执行server
bin/jmeter-server
# 执行压测任务
bin/jmeter -n -t metrics_interface/dcs.jmx -l report/metrics_interface.jtl.alpha -R127.0.0.1
~~~

### 参数说明
~~~ text
-n  This specifies JMeter is to run in non-gui mode
-t  [name of JMX file that contains the Test Plan].
-l  [name of JTL file to log sample results to].
-j  [name of JMeter run log file].
-r  Run the test in the servers specified by the JMeter property "remote_hosts"
-R  [list of remote servers] Run the test in the specified remote servers
-g  [path to CSV file] generate report dashboard only
-e  generate report dashboard after load test
-o  output folder where to generate the report dashboard after load test. Folder must not exist or be empty
 
The script also lets you specify the optional firewall/proxy server information:
-H  [proxy server hostname or ip address]
-P  [proxy server port]
~~~