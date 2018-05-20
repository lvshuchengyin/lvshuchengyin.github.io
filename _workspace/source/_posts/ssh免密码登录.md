title: ssh免密码登录
author: Lscy
tags:
  - linux
categories:
  - 编程
date: 2018-05-20 11:11:00
---
### 生成公私密钥
~~~ bash
ssh-keygen -t rsa
# 提示输入的话直接回车即可
# 生成的密钥在~/.ssh/，公钥：id_rsa.pub，私钥：id_rsa
~~~

### 将公钥设置到目标机器
~~~ bash
# 添加公钥到authorized_keys
cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
# 修改authorized_keys权限
chmod 600 ~/.ssh/authorized_keys
~~~