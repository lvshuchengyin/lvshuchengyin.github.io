title: ambari安装
author: Lscy
tags:
  - 服务组件
categories:
  - 编程
date: 2018-05-20 11:11:00
---
### 添加yum源
~~~ bash
wget -nv http://public-repo-1.hortonworks.com/ambari/centos6/2.x/updates/2.2.2.0/ambari.repo -O /etc/yum.repos.d/ambari.repo
~~~

### 安装
~~~ bash
yum repolist
yum install ambari-server
~~~

### 配置
~~~ bash
ambari-server setup
~~~

### 启动
~~~ bash
ambari-server start
~~~
<!-- more -->
### 手动安装agent
~~~ bash
yum install ambari-agent
~~~
如果网络太慢，则可以配置本地的自定义源，这样就不用去远程下载
* 1)下载ambari包：
wget http://public-repo-1.hortonworks.com/ambari/centos6/2.x/updates/2.2.2.0/ambari-2.2.2.0-centos6.tar.gz
* 2)解压到http服务器中（nginx）
* 3)修改ambari.repo为目标ip
~~~ text
#VERSION_NUMBER=2.2.2.0-460
 
[Updates-ambari-2.2.2.0]
name=ambari-2.2.2.0 - Updates
baseurl=http://<target_ip>/AMBARI-2.2.2.0/centos6/2.2.2.0-460
gpgcheck=1
gpgkey=http://<target_ip>/AMBARI-2.2.2.0/centos6/2.2.2.0-460/RPM-GPG-KEY/RPM-GPG-KEY-Jenkins
enabled=1
priority=1
~~~
* 4)手动安装agent时需要改agent的配置
~~~ bash
vi /etc/ambari-agent/conf/ambari-agent.ini
[server]
hostname=<your.ambari.server.hostname>
url_port=8440
secured_url_port=8441
~~~
### 清除metrics的数据
~~~ text
先停止metrics server服务和ambari-server
找到metrics配置中的以下两项，然后删除对应文件夹
删除hbase.rootdir：/data11/data11/var/lib/ambari-metrics-collector/hbase
删除hbase.tmp.dir：/data10/var/lib/ambari-metrics-collector/hbase-tmp
启动服务
~~~
### 删除服务
~~~ bash
curl -u admin:admin -H "X-Requested-By: ambari" -X DELETE  http://localhost:8080/api/v1/clusters/test/services/SAMPLE
~~~
### api
~~~ bash
# 添加机器
curl --user admin:admin -i -X POST -H "X-Requested-By: ambari"  http://127.0.0.1:8080/api/v1/clusters/ODF/hosts/am123
# 添加服务
curl --user admin:admin -i -X POST -H "X-Requested-By: ambari" http://127.0.0.1:8080/api/v1/clusters/ODF/hosts/am123/host_components/METRICS_MONITOR
# 安装组件
curl --user admin:admin -i -X PUT -d '{"HostRoles": {"state": "INSTALLED"}}' -H "X-Requested-By: ambari" http://127.0.0.1:8080/api/v1/clusters/ODF/hosts/am123/host_components/METRICS_MONITOR
# 启动组件
curl --user admin:admin -i -X PUT -d '{"HostRoles": {"state": "STARTED"}}' -H "X-Requested-By: ambari" http://127.0.0.1:8080/api/v1/clusters/ODF/hosts/am123/host_components/METRICS_MONITOR
~~~