title: mysql数据库设置
author: Lscy
tags:
  - mysql
categories:
  - 编程
date: 2018-05-20 10:06:00
---
### 修改密码
~~~ bash
mysqladmin -u用户名 -p旧密码 password 新密码
~~~

### 备份还原数据库
~~~ bash
# 设置从特定地址的服务器导出数据, 缺省主机是localhost, 则设置参数-h 或 --host=
# 备份所有数据库:
mysqldump -u root -p123  --all-database  >  test.sql
# 备份数据库test
mysqldump -u root -p123  dbname >  dbname.$(date "+%Y-%m-%d").sql
# 备份数据库test下的temp表:
mysqldump -u root -p123  test demp >  test.sql
# 还原数据库test
mysqldump -u root -p123  test  <  test.sql
# 还原数据库test下的temp表:
mysqldump -u root -p123  test demp < test.sql
# 但是有时候这样还原不了，那就进入mysql控制台，使用命令：
source test.sql
~~~
<!-- more -->
### 权限设置，会自动创建账号
~~~ sql
# 授权
grant all on dbname.* to username@'192.168.0.10' identified by 'passwd';
# 删除权限
revoke all on dbname.* from username@'192.168.0.10' identified by 'passwd';
# 刷新权限
FLUSH PRIVILEGES;
~~~

### 编码设置
~~~ sql
set character_set_client=utf8;
set character_set_connection=utf8;
set character_set_database=utf8;
set character_set_results=utf8;
set character_set_server=utf8;
~~~

### 数据库及表转换成utf编码
~~~ sql
# 转换
alter table table_name convert to character set utf8;
# 和上面的不同，这个应该是设置编码
alter database database_name character set utf8;
alter table table_name character set utf8;
~~~

### 创建时指定编码
~~~ sql
# 创建数据库
# create database name character set utf8;
CREATE DATABASE 'test2' DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci
# 创建表
CREATE TABLE 'table1' (
`id` int(10) unsigned NOT NULL auto_increment,
`flag_deleted` enum('Y','N') character set utf8 NOT NULL default 'N',
`flag_type` int(5) NOT NULL default '0',
`type_name` varchar(50) character set utf8 NOT NULL default '',
PRIMARY KEY (`id`)
)  DEFAULT CHARSET=utf8;
~~~

### 查看字符编码
~~~ sql
SHOW VARIABLES LIKE'character_set_%';
SHOW VARIABLES LIKE'collation_%';
~~~

### 数据库设置
~~~ text
# 找到客户端配置[client] 在下面添加
default-character-set=utf8 #默认字符集为utf8
# 在找到[mysqld] 添加
character-set-server=utf8 #默认字符集为utf8
init-connect='SET NAMES utf8'#（设定连接mysql数据库时使用utf8编码，以让mysql数据库为utf8运行）
~~~