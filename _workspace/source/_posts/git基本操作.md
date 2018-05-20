title: git基本操作
author: Lscy
tags:
  - 服务组件
categories:
  - 编程
date: 2018-05-20 11:28:00
---
### clone远端项目
~~~ bash
git clone https://github.com/jquery/jquery.git
git clone username@host:/path/to/repository
~~~

### 远程主机
~~~ bash
# 克隆版本库的时候，所使用的远程主机自动被Git命名为origin
git remote -v
# 将你的仓库连接到某个远程服务器
git remote add origin <server>
~~~

### 提交，拉取
~~~ bash
# 注意，分支写法是<来源地>:<目的地>
# git fetch <远程主机名> <分支名>，使用"远程主机名/分支名"读取。比如origin主机的master：origin/master
git fetch origin master
git pull <远程主机名> <远程分支名>:<本地分支名>
git push <远程主机名> <本地分支名>:<远程分支名>
~~~
<!-- more -->
### 分支
~~~ bash
# 合并分支
git merge <branch>
# 查看
git branch -a
# 新建
git checkout -b branch_1
# 切换
git checkout master
# 删除
git branch -d branch_2
# 差异
git diff branch_1 branch_2
~~~

### 恢复
~~~ bash
# 替换掉本地改动
git checkout -- <filename>
# 丢弃本地的所有改动与提交，获取服务器最新的版本
git fetch origin
git reset --hard origin/master
~~~

### 历史记录
~~~ bash
git log
~~~