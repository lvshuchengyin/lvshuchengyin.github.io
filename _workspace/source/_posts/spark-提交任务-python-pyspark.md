title: spark 提交任务 python pyspark
author: Lscy
tags:
  - python
  - 服务组件
categories:
  - 编程
date: 2018-05-20 11:27:00
---
### spark-submit
~~~ bash
spark-submit --master yarn --deploy-mode cluster --queue q1 --num-executors 1 scripy.py
~~~

### pyspark
~~~ python
def process(rows):
    content = ""
    for row in rows:
        content += b64encode(row.url)
    return [content]
     
conf = SparkConf().setAppName('PoliceHive2Xml')
spark_context = SparkContext(conf=conf)
hive_context = HiveContext(spark_context)
sql = "select * from table where dayno=20170807 limit 1000"
data_frame = hive_context.sql(sql)
hdfs_filepath = get_hdfs_filepath(table_name, zip_file_name)
data_frame.mapPartitions(process).saveAsTextFile(hdfs_filepath)
~~~