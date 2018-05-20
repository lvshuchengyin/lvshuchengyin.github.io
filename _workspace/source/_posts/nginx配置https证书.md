title: nginx配置https证书
author: Lscy
tags:
  - linux
categories:
  - 编程
date: 2018-05-20 10:11:00
---
~~~ text
#upstream mysvr {
#    server 127.0.0.1:8099 weight=1;  
#    server 127.0.0.1:8099 weight=1;
#}
server {
    server_name example.com;
    listen 443 ssl;
    ssl_certificate     /home/stat/example.com/cert/example.com.crt;
    ssl_certificate_key /home/stat/example.com/cert/ca.example.com.key;
    ssl_session_cache    shared:SSL:1m;
    ssl_session_timeout  5m;
    ssl_ciphers  HIGH:!aNULL:!MD5;
    ssl_prefer_server_ciphers  on;
    log_format  example_log '[$time_local] $remote_addr "$request" '
                        '$status $upstream_status $body_bytes_sent $request_time $upstream_response_time '
                        '"$remote_user" "$http_user_agent" "$http_referer"';
    access_log /var/www/example/nginxlog/access.log example_log;
    error_log  /var/www/example/nginxlog/error.log;
    gzip on;
    location ~ ^/static/ {
        root /var/www/example;
    }
    location / {        
        proxy_set_header    Host    $host;
        proxy_set_header    X-REAL-IP   $remote_addr;
        proxy_set_header    X-FORWARDED-FOR $proxy_add_x_forwarded_for;
        proxy_ignore_client_abort on;
        #proxy_pass  http://mysvr;
        proxy_pass http://127.0.0.1:8099;
    }
}
~~~