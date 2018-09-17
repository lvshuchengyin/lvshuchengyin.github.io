title: hdfs设置账号权限
author: Lscy
tags:
  - 服务组件
categories:
  - 编程
date: 2018-09-17 09:29:00
---
### 设置目录的默认权限
~~~ bash
# 设置目录的默认权限，这样用户新创建的目录和子目录就会自动有权限
hdfs dfs -setfacl -R -m default:group:group1:rwx /hive-dw/db1
# 设置已有目录的权限
hdfs dfs -setfacl -R -m group:group1:rwx /hive-dw/db1
~~~