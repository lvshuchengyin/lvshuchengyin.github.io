title: inode软连接和硬连接说明
author: Lscy
tags:
  - linux
categories:
  - 编程
date: 2018-05-20 11:00:00
---
### 软连接
~~~ bash
ln -s B A
 
# 文件A和文件B的inode号码不一样，只是文件A的内容是文件B的路径，读取文件A时，系统会自动将访问者导向文件B
# 文件A依赖于文件B而存在，如果删除了文件B，打开文件A就会报错
# 文件A指向文件B的文件名，而不是文件B的inode号码，文件B的inode"链接数"不会因此发生变化
~~~

### 硬连接
~~~ bash
ln B A
 
# 源文件与目标文件的inode号码相同，都指向同一个inode
# 这意味着，可以用不同的文件名访问同样的内容；对文件内容进行修改，会影响到所有文件名
# 但是，删除一个文件名，不影响另一个文件名的访问
~~~