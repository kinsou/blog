title: Ubuntu下安装Shadowsocks
tags:
  - Ubuntu
categories:
  - Ubuntu
date: 2015-12-17 11:54:00
---
1. 更新列表：
```shell
sudo apt-get update
```
2. 确认Ubuntu机器上Python的版本号（需要不小于 2.6）：
```shell
sudo apt-get update
```
3. 安装 python-pip和 shadowsocks：
```shell
apt-get install python-gevent python-pip python-m2crypto
pip install shadowsocks
```
4. 找到shadowsocks配置文件所在文件夹，一般为：
```shell
/etc/shadowsocks/

或者通过以下命令完全搜索（可以使用通配符）
find / -name shadowsocks
```
5. 修改配置文件夹下面的 config.json 文件（如果不存在则创建一个），该文件为json格式，具体如下：
```
单用户配置：
{
        "timeout":600,
        "method":"aes-256-cfb",
        "local_port":1080,
        "server":"0.0.0.0",
 
        "server_port":8388,
        "password":"passwd"
}
 
多用户配置（通过配置多个端口来实现）：
{
        "timeout":600,
        "method":"aes-256-cfb"
        "local_port":1080,
        "server":"0.0.0.0",
 
        "port_password": 
        {
                "8388":"passwd1",
                "8391":"passwd2"
        },
        "_comment":
        {
                "8388":"user1",
                "8391":"user1"
        }
}
 
每项配置含义如下：
timeout：         超时时间
method：          加密方式
local_port：      本地代理服务监听端口（用于当前机器的程序使用）
server：          作为代理服务器监听的IP（全0表示监听所有IP）
server_port：     作为代理服务器监听的端口（作为服务器用于其他机器使用）
password：        作为代理服务器提供服务时用于验证的密码
port_password：   为每个不同端口设置不同的验证密码（适用于多用户时）
_comment：        为每个不同端口设置说明文本（例如备注每个端口的使用者）
```
6. 开机自动启动：

```shell
/usr/local/bin/ssserver -c /etc/shadowsocks/config.json -d start
```