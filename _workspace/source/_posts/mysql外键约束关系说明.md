title: mysql外键约束关系说明
author: Lscy
tags:
  - mysql
categories:
  - 编程
date: 2018-05-20 11:01:00
---
### 说明
MySQL有两种常用的引擎类型：MyISAM和InnoDB，目前只有InnoDB引擎类型支持外键约束。
~~~ sql
ALTER TABLE tbl_name
    ADD [CONSTRAINT [symbol]] FOREIGN KEY
    [index_name] (index_col_name, ...)
    REFERENCES tbl_name (index_col_name,...)
    [ON DELETE reference_option]
    [ON UPDATE reference_option]
~~~

### 约束关系
~~~ text
CASCADE：在父表上update/delete记录时，同步update/delete掉子表的匹配记录 
SET NULL：在父表上update/delete记录时，将子表上匹配记录的列设为null (要注意子表的外键列不能为not null)  
NO ACTION：如果子表中有匹配的记录,则不允许对父表对应候选键进行update/delete操作  
RESTRICT：同no action, 都是立即检查外键约束
mysql下NO ACTION == RESTRICT
~~~