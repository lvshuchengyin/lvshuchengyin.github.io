title: hbase操作
author: Lscy
tags:
  - 服务组件
categories:
  - 编程
date: 2018-09-17 09:32:00
---
### 建表
~~~ bash
create 'table1', {
        NAME => 'card', 
        DATA_BLOCK_ENCODING => 'NONE', 
        BLOOMFILTER => 'ROWCOL', 
        REPLICATION_SCOPE => '1', 
        COMPRESSION => 'SNAPPY', 
        VERSIONS => '1', 
        MIN_VERSIONS => '0', 
        KEEP_DELETED_CELLS => 'false', 
        BLOCKSIZE => '65536', 
        IN_MEMORY => 'false', 
        BLOCKCACHE => 'false'
}
~~~
### 数据操作
~~~ bash
put 'table1', 'rowkey1', 'card:col3', 'value3'
get 'table1', 'rowkey1', {COLUMN => ['card:col1', 'card:col2']}
scan 'table1'
~~~
### java
~~~ java
public void test() {
        logger.info("test");

        Configuration conf = HBaseConfiguration.create();
        conf.set("hbase.master", "172.17.161.5:60000");
        conf.set("hbase.zookeeper.property.clientport", "2181");
        conf.set("hbase.zookeeper.quorum", "172.17.161.5");
        conf.set("zookeeper.znode.parent", "/hbase-rpt");

        try {
            Connection connection = ConnectionFactory.createConnection(conf);
            Admin admin = connection.getAdmin();

            TableName[] names = admin.listTableNames();
            for (TableName tableName : names) {
                logger.info("Table Name is : " + tableName.getNameAsString());
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
~~~