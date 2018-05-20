title: 使用let's encrypt配置免费的https证书
author: Lscy
tags:
  - linux
categories:
  - 编程
date: 2018-05-20 10:56:00
---
### 安装
~~~ bash
yum -y install yum-utils
yum-config-manager --enable rhui-REGION-rhel-server-extras rhui-REGION-rhel-server-optional
yum install certbot
~~~

### 关闭nginx
因为standalone需要占用80和443端口

### 生成证书
~~~ bash
certbot certonly --standalone -d example.com -d www.example.com
~~~

### 配置nginx证书
~~~ bash
ssl_certificate    /etc/letsencrypt/live/simpledao.win/fullchain.pem;
ssl_certificate_key    /etc/letsencrypt/live/simpledao.win/privkey.pem;
ssl_trusted_certificate /etc/letsencrypt/live/simpledao.win/chain.pem;
~~~
### 启动nginx

### 更新证书，因为生成的证书只有90天有效期
~~~ bash
# 测试是否能生成
certbot renew --dry-run
# 生成
certbot renew
~~~
注意：由于使用的是standalone模式，需要占用80和443端口，所以需要先关闭nginx才能生成或更新证书，使用webroot模式，则可以不关闭nginx，但需要配置。