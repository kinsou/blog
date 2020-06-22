title: Nginx安装反向代理配置
author: ZkName
tags:
  - Ubuntu
  - Nginx
  - SSL
categories: []
date: 2017-08-07 12:25:00
---
#### 1、安装Nginx
```shell
apt-get update
apt-get install nginx
/etc/init.d/nginx start
```
#### 2、配置反向代理
```shell
vi /etc/nginx/conf.d/domain.conf

server {
        listen 80;
        server_name domain.com;
        location / {
		proxy_set_header Host $host;
		proxy_set_header X-Real-IP $remote_addr;
		proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
		proxy_set_header X-Forwarded-Proto $scheme;
		proxy_pass http://localhost:8080;
        }
}
```
#### 3、配置反向代理加SSL
```shell
vi /etc/nginx/conf.d/domain.conf

server {
        listen 80;
        listen 443 ssl;
        server_name domain.com;
        
        ssl on;
        ssl_certificate /etc/ssl/private/domain.crt;
        ssl_certificate_key /etc/ssl/private/domain.key
        ssl_prefer_server_ciphers on;
        
        location / {
		proxy_set_header Host $host;
		proxy_set_header X-Real-IP $remote_addr;
		proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
		proxy_set_header X-Forwarded-Proto $scheme;
		proxy_pass http://localhost:8080;
        }
}
```