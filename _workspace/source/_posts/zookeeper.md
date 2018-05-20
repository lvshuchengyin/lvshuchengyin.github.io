title: zookeeper
author: Lscy
tags:
  - 服务组件
categories:
  - 编程
date: 2018-05-20 10:34:00
---
### 客户端连接
~~~ bash
bin/zkCli.sh -server 127.0.0.1:2181
 
# 创建节点，其中"-s"表示创建一个"有序"节点,"-e"表示创建一个临时节点.默认为持久性节点
create [-s] [-e] /path data acl
# 获取节点数据
get /path
# 查看子节点列表
ls /path
# 设置节点值
set path data [version]
# 删除节点
delete /path [version]
# 删除节点，及其子节点
rmr path
# 设置ACL
setAcl path acl
# 添加授权信息
addauth schema auth
~~~