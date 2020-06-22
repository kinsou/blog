title: ubuntu dnsmasq配置
tags:
  - Ubuntu
  - DNSmasq
categories:
  - Ubuntu
date: 2014-10-14 10:22:00
---
## 简介
#### DNSmasq是一个轻巧的，容易使用的DNS服务工具，它可以应用在内部网和Internet连接的时候的 IP地址NAT转换，也可以用做小型网络的DNS服务。
## 安装
```shell
sudo apt-get install dnsmasq
```
## 配置
```shell
vi /etc/dnsmasq.conf

# Configuration file for dnsmasq.
#
# Format is one option per line, legal options are the same
# as the long options legal on the command line. See
# "/usr/sbin/dnsmasq --help" or "man 8 dnsmasq" for details.

# The following two options make you a better netizen, since they
# tell dnsmasq to filter out queries which the public DNS cannot
# answer, and which load the servers (especially the root servers)
# unnecessarily. If you have a dial-on-demand link they also stop
# these requests from bringing up the link unnecessarily.

# Never forward plain names (without a dot or domain part)
#domain-needed
# Never forward addresses in the non-routed address spaces.
#bogus-priv


# Uncomment this to filter useless windows-originated DNS requests
# which can trigger dial-on-demand links needlessly.
# Note that (amongst other things) this blocks all SRV requests,
# so don't use it if you use eg Kerberos, SIP, XMMP or Google-talk.
# This option only affects forwarding, SRV records originating for
# dnsmasq (via srv-host= lines) are not suppressed by it.
#filterwin2k

# Change this line if you want dns to get its upstream servers from
# somewhere other that /etc/resolv.conf
#resolv-file=
#用于设置上级dns服务器，用于向上级服务器转发查询请求。不设置，默认使用/etc/resolv.conf 如要解析外网的dns，必须设置此项用于向外转发dns请求。

# By  default,  dnsmasq  will  send queries to any of the upstream

...
...
...

# Include a another lot of configuration options.
#conf-file=/etc/dnsmasq.more.conf
conf-dir=/etc/dnsmasq.d
#用于包含配置文件目录

```

#### 在/etc/dnsmasq.d 新建文件配置文件dns-intrant.conf 添加常用的网站用于dns缓存
```shell
address=/a.com/192.168.1.1 

#泛解析
address=/.a.com/192.168.1.1
address=/.a.net/192.168.1.2
address=/.a.cn/192.168.3  
```
## 启动服务
```shell
sudo service dnsmasq restart

#查看服务是否启动
netstat -ntlp|grep 53 
```

