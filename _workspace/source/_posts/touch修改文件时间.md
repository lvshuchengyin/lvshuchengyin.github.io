title: touch修改文件时间
author: Lscy
tags:
  - linux
categories:
  - 编程
date: 2018-05-20 11:04:00
---
### touch命令
~~~ bash
touch -a -m -t 201512180130.09 fileName.ext
 
-a = accessed
-m = modified
-t = timestamp - use [[CC]YY]MMDDhhmm[.ss] time format
-c, --no-create        do not create any files
~~~

### 文件时间说明
* a访问时间，读一次这个文件的内容，这个时间就会更新。比如对这个文件运用 more、cat等命令。ls、stat命令都不会修改文件的访问时间。
* m修改时间，修改时间是文件内容最后一次被修改时间。比如：vi后保存文件。ls -l列出的时间就是这个时间。
* c状态改动时间。是该文件的i节点最后一次被修改的时间，通过chmod、chown命令修改一次文件属性，这个时间就会更新。
