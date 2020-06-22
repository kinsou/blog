title: Ubuntu 安装 SSR 一键脚本
author: ZkName
tags:
  - Ubuntu
  - shadowsocks
  - ssr
categories: []
date: 2017-04-19 12:27:00
---
## SSR一键脚本

###### 几个默认配置：
默认加密为： chacha20
默认协议为： auth_sha1_v4
默认混淆为：  tls1.2_ticket_auth

### 一键脚本的安装
```shell
wget -N --no-check-certificate https://raw.githubusercontent.com/91yun/shadowsocks_install/master/shadowsocksR.sh && bash shadowsocksR.sh
```
###### 本脚本安装完成后，已将 ShadowsocksR 自动加入开机自启动。
### 卸载方法：
```shell
bash ./shadowsocksR.sh uninstall
```
### 升级方法：
```shell
cd /usr/local/shadowsocks/shadowsocks
git pull
```
### 使用命令：
启动： /etc/init.d/shadowsocks start
停止： /etc/init.d/shadowsocks stop
重启： /etc/init.d/shadowsocks restart
状态： /etc/init.d/shadowsocks status

配置文件路径： /etc/shadowsocks.json
日志文件路径： /var/log/shadowsocks.log
安装路径： /usr/local/shadowsocks/shadowsoks

### 多用户配置
如果要多个用户一起使用的话，请写入以下配置（ vi /etc/shadowsocks.json ）：

多用户的核心是这个配置，把这个配置替代掉 /etc/shadowsocks.json 的相关密码的配置就行了：
```shell
“port_password”:{
“80”:”password1″,
“443”:”password2″
},
```

###### 完整的多用户配置：
```shell
{
    "server":"0.0.0.0",
    "server_ipv6": "[::]",
    "local_address":"127.0.0.1",
    "local_port":1080,
    "port_password":{
        "80":"password1",
        "443":"password2"
    },
    "timeout":300,
    "method":"aes-256-cfb",
    "protocol": "auth_sha1_compatible",
    "protocol_param": "",
    "obfs": "http_simple_compatible",
    "obfs_param": "",
    "redirect": "",
    "dns_ipv6": false,
    "fast_open": false,
    "workers": 1
}
```

文章来源：https://www.91yun.org/archives/2079


