title: cdh添加自定义扩展服务，分发，管理
author: Lscy
tags:
  - 服务组件
categories:
  - 编程
date: 2018-05-20 11:06:00
---
### 参考
https://github.com/cloudera/cm_ext

https://github.com/cloudera/cm_csds

### 生成parcel
~~~ bash
# 需要在目标文件夹内新建meta文件，并在meta中新建文件parcel.json，文件内容需要自己参考资料填写
# 验证文件
java -jar cm_ext/validator/target/validator.jar -p HELLO-1.0/meta/parcel.json
# 验证目录
java -jar cm_ext/validator/target/validator.jar -d HELLO-1.0
# 打包parcel
tar zcvf HELLO-1.0-el6.parcel HELLO-1.0 --owner=root --group=root
# 验证
java -jar cm_ext/validator/target/validator.jar -f HELLO-1.0-el6.parcel
~~~
<!-- more -->
### 对外提供http的parcel服务
~~~ bash
# 生成manifest.json
python cm_ext/make_manifest/make_manifest.py /data/root
# 提供http服务
python -m SimpleHTTPServer 10001
~~~

### 配置cm的parcel
添加上述http地址，即可分发parcel

### 生成CSD
~~~ bash
# 新建目录，内部结构为
├── descriptor
│   └── service.sdl
└── scripts
    └── control.sh
 
# 文件内容需要自己参考资料填写
#验证
java -jar cm_ext/validator/target/validator.jar -s csd/HELLO-1.0/descriptor/service.sdl
# 打包
jar -cvf HELLO-1.0.jar *
# 复制到csd目录
~~~cp HELLO-1.0.jar /opt/cloudera/csd/

### 重启cm服务即可生效

### 示例

HELLO-1.0/meta/parcel.json
~~~ json
{
    "schema_version":1,
    "name":"HELLO",
    "version":"1.0",
    "setActiveSymlink":true,
    "conflicts":"",
    "provides":[
        "hello"
    ],
    "scripts":{
        "defines":"hello_env.sh"
    },
    "packages":[
        {
            "name":"hello",
            "version":"1.0"
        }
    ],
    "components":[
        {
            "name":"hello",
            "version":"1.0",
            "pkg_version":"1.0",
            "pkg_release":"1.0"
        }
    ],
    "users":{},
    "groups":[]
}
~~~
HELLO-1.0/meta/hello_env.sh
~~~ bash
HELLO_DIRNAME=${PARCEL_DIRNAME}
export CDH_HELLO_HOME=$PARCELS_ROOT/$HELLO_DIRNAME
~~~
cat descriptor/service.sdl
~~~ json
{
    "name":"HELLO",
    "label":"Hello",
    "description":"The hello service",
    "version":"1.1",
    "runAs":{
        "user":"root",
        "group":"root"
    },
    "compatibility":{
        "generation":1
    },
    "icon":"images/icon.png",
    "parcel" : {
        "requiredTags" : [ "hello" ],
        "optionalTags" : [ "hello-plugin" ]
    },
    "parameters":[
        {
            "name":"service_var1",
            "label":"Service Var1 Label",
            "description":"Service Var1 Description",
            "configName":"service.var1.config",
            "type":"string",
            "default":"this is a default"
        }
    ],
    "roles":[
        {
            "name":"HELLO_SERVICE",
            "label":"hello service",
            "pluralLabel":"hello services",
            "parameters":[
                {
                    "name":"init_content",
                    "label":"conf1",
                    "description":"conf",
                    "type":"string",
                    "default": "defaultiii"
                }
            ],
            "startRunner":{
                "program":"scripts/control.sh",
                "args":[
                    "start"
                ],
                "environmentVariables":{
                    "PORT": "10002"
                }
            }
        }
    ]
}
~~~
scripts/control.sh
~~~ bash
#!/bin/bash
 
CMD=$1
 
export HELLO_HOME=${HELLO_HOME:-$CDH_HELLO_HOME}
 
case $CMD in
 
  (start)
    echo "Starting Hello123"
    exec python $HELLO_HOME/src/hello.py
    ;;    
 
  (*)
    echo "Don't understand [$CMD]"
    ;;
 
esac
~~~