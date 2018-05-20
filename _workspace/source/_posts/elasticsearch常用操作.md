title: elasticsearch常用操作
author: Lscy
tags:
  - 服务组件
categories:
  - 编程
date: 2018-05-20 11:35:00
---
### 使用aggregations，排序必须要开启fielddata
~~~ text
PUT my_index/_mapping/my_type
{
  "properties": {
    "my_field": { 
      "type":     "text",
      "fielddata": true
    }
  }
}
~~~

### 安装，参数设置
~~~ bash
# 内核设置
vm.swappiness=1
vm.max_map_count=262144
# 内存设置
export ES_HEAP_SIZE=8g
# 配置文件
path.data: /home/stat/elasticsearch-6.1.1/data
path.logs: /home/stat/elasticsearch-6.1.1/logs
indices.fielddata.cache.size:  20%
# 外部访问
network.host: 0.0.0.0
# [1]: max file descriptors [4096] for elasticsearch process is too low, increase to at least [65536]
# [2]: max number of threads [1024] for user [stat] is too low, increase to at least [4096]
# [3]: system call filters failed to install; check the logs and fix your configuration or disable system call filters at your own risk
修改 /etc/security/limits.conf
* soft nofile 65536
* hard nofile 131072
* soft nproc 4096
* hard nproc 4096
修改 /etc/security/limits.d/90-nproc.conf
* soft nproc 4096
要在Memory下面修改增加:
bootstrap.memory_lock: false
bootstrap.system_call_filter: false
~~~
<!-- more -->
### 开启fielddata
~~~ text
PUT http://127.0.0.1:9200/_template/template_test
{
    "index_patterns": ["test*"],
    "mappings": {
        "default": {
          "_source": {
            "enabled": true
          },
          "properties": {
          "@timestamp": {
              "type":   "date",
              "format": "epoch_millis"
            },
            "host": { 
              "type":     "text",
              "fielddata": true
            },
            "server": { 
              "type":     "text",
              "fielddata": true
            }
          }
        }
  }
}
~~~

### 不分词的string
~~~ text
"domain": { 
    "type":     "keyword",
    "doc_values": true
}
~~~

### 允许跨域访问
解决Response to preflight request doesn't pass access control check: No 'Access-Control-Allow-Origin' header...
~~~ text
http.cors.enabled: true  
http.cors.allow-origin: "*"
~~~

### 设置副本，字段默认类型，匹配，模版
~~~ text
POST http://127.0.0.1:9200/_template/template_metrics
{
    "index_patterns":[
        "metrics-*"
    ],
    "settings":{
        "number_of_shards":3,
        "number_of_replicas":"1",
        "refresh_interval":"30s"
    },
    "mappings":{
        "_default_":{
            "_all":{
                "enabled":false
            },
            "_source":{
                "enabled":true
            },
            "dynamic_templates":[
                {
                    "template_string":{
                        "match_mapping_type":"string",
                        "mapping":{
                            "type":"keyword",
                            "doc_values":true,
                            "norms":false
                        }
                    }
                }
            ],
            "properties":{
                "@timestamp":{
                    "type":"date",
                    "format":"epoch_millis"
                }
            }
        }
    }
}
~~~