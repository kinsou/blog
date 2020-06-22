title: Centos scp 拷贝文件
tags:
  - Centos
categories:
  - Centos
date: 2013-05-10 09:49:00
---
## 复制文件或目录命令
### 复制文件：
#### （1）将本地文件拷贝到远程
scp 文件名 用户名@计算机IP或者计算机名称:远程路径
```shell
scp /root/jdk-6u24-linux-x64.bin  root@192.168.0.65:/root/jdk-6u24-linux-x64.bin
```
#### （2）从远程将文件拷回本地
scp 用户名@计算机IP或者计算机名称:文件名 本地路径
```shell
scp root@192.168.0.65:/root/jdk-6u24-linux-x64.bin /root/jdk-6u24-linux-x64.bin
```

### 复制目录：
#### （1）将本地目录拷贝到远程
scp -r 目录名 用户名@计算机IP或者计算机名称:远程路径
```shell
scp -r /app/jetty  root@192.168.0.65:/app/jetty
```
#### （2）从远程将目录拷回本地
scp -r   用户名@计算机IP或者计算机名称:目录名 本地路径
```shell
scp -r root@192.168.0.65:/app/jetty  /app/jetty
```