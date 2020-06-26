title: Ubuntu安装 pip 配置服务器端 shadowsocks
author: ZkName
tags:
  - shadowsocks
  - Ubuntu
categories: []
date: 2017-04-10 12:12:00
---
## Ubuntu 安装 pip 配置服务器端 shadowsocks

#### 1、安装 pip
```shell
#更新源
apt-get update
apt-get upgrade
#安装
apt-get install python-pip
```
#### 2、安装 shadowsocks

###### 1.安装最新版：
```shell
pip install https://github.com/shadowsocks/shadowsocks/archive/master.zip
```
###### 2.配置编辑文件： vi /etc/shadowsocks.json
```shell
{
    "server":"0.0.0.0",
    "server_port":8388,
    "password":"xxx",
    "timeout":60,
    "method":"rc4-md5",
    "workers": 4,
    "fast_open": true
}
```
###### 3.开机启动 编辑文件 vi /etc/rc.local 增加：
```shell
nohup ssserver -c /etc/shadowsocks.json > log &
iptables -I INPUT -4 -p tcp -m tcp --dport 8388 -j ACCEPT
```
#### 3、安装 supervisor 
```shell
#安装
apt-get install supervisor
```
###### 1.编辑文件：vi /etc/supervisor/conf.d/s-server.conf
```shell
[program:ssserver]
command=/usr/local/bin/ssserver -c /etc/shadowsocks.json
directory=/tmp
user=root
autostart=true
autorestart=true
stdout_logfile=/dev/null
stderr_logfile=/dev/null
```
###### 2.重新加载配置文件：
```shell
sudo supervisorctl reload
```