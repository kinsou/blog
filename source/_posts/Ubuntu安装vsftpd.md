title: Ubuntu安装vsftpd
tags:
  - Ubuntu
categories:
  - Ubuntu
date: 2016-05-19 10:14:00
---
## 1、安装
```shell
sudo apt-get update
sudo apt-get install vsftpd
```
## 2、新建用户uftp并设置密码
### 创建用户
```shell
useradd ftpuser -s /sbin/nologin -d /app/ftpuser/
passwd ftpuser
```
### 目录赋权限
```shell
chmod 777 -R /app/ftpuser/html
```