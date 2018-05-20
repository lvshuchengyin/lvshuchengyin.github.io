title: mongodb常用操作
author: Lscy
tags:
  - 服务组件
categories:
  - 编程
date: 2018-05-20 11:34:00
---
### 备份,恢复
~~~ bash
mongodump -h127.0.0.1:27017 -o ./dump
mongorestore -h 127.0.0.1:27017 ./dump
 
# 可以导出json或csv
mongoexport   -h 127.0.0.1 --db tb_page --collection tb_page --type json -o tb_page.json
mongoimport -h 127.0.0.1 --db tb_page --collection tb_page --type json --mode upsert --file tb_page.json
~~~

### 更新
~~~ bash
db.users.update({"_id": "id1"}, {"$set": {"groups": []}})
~~~

### 插入
~~~ bash
db.products.insert( { item: "card", qty: 15 } )
~~~
<!-- more -->
### 列表元素追加
~~~ bash
# 追加单个元素
db.inventory.update(
   { _id: 1 },
   { $addToSet: { tags: "camera"  } })
 
# 追加多个元素
db.inventory.update(
   { _id: 2 },
   { $addToSet: { tags: { $each: [ "camera", "electronics", "accessories" ] } } }
 )
 ~~~