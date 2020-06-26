title: ubuntu18.04搭建NTP服务器
author: ZkName
tags:
  - Ubuntu
  - NTP
categories: []
date: 2020-03-20 16:25:00
---

#### 1、安装NTP
```shell
apt-get install ntp
```
#### 2、配置文件/etc/ntp.conf
```shell
vim /etc/ntp.conf
```
##### 2、配置上层server

```shell
#这里常用的选项是prefer - 优先主机， iburst -当服务器不可用时将发包检测
server ntp1.aliyun.com prefer
server ntp2.aliyun.com iburst
server ntp3.aliyun.com iburst
server ntp4.aliyun.com iburst
server ntp5.aliyun.com iburst
```
```shell
#允许这个网段的对时请求
restrict 192.168.0.0 mask 255.255.255.0 nomodify 
```

##### 3、防火墙取消对123端口的限制
```shell
iptables -t filter -A INPUT -p udp --destination-port 123 -j ACCEPT

#或者
sudo ufw allow 123/udp
```

##### 4、ntp 开机启动
```shell
systemctl enable ntp
```

##### 5、查看状态
```shell
watch ntpq -p

Every 2.0s: ntpq -p                                                                                             nacos: Fri Mar 20 17:00:21 2020

     remote           refid      st t when poll reach   delay   offset  jitter
==============================================================================
*120.25.115.20   10.137.53.7      2 u   25   64   37   30.932   -7.778   4.707
+tick.ntp.infoma .GPS.            1 u   21   64   37  280.022  -13.369   3.185
-94.130.49.186 ( 195.13.23.5      3 u   15   64   37  246.228   -6.189  89.097
+ntp1.ams1.nl.le 130.133.1.10     2 u   14   64   35  224.919   -7.378   6.993
+ntp5.flashdance 194.58.202.148   2 u   22   64   37  264.122   -6.842   5.630

```
说明：
```shell
remote: 连接的远程NTP服务器；
refid: 提供时间同步的服务器IP；
st: 远程服务器的层级别（stratum）。由于NTP是层型结构，有顶端的服务器、多层的Relay服务器、再到客户端。所以服务器级别从高到低可以设定为1-16。为了减缓负荷和网络堵塞，原则上应该避免直接连接到级别为1的服务器；
when: 几秒钟前曾经做过时间同步更新的动作；
poll: 本地主机和远程服务器多少时间进行一次同步(单位：s)；
reach: 已经向上层NTP服务器要求更新的次数；
delay: 网络传输过程当中延迟的时间（单位：10^(-6)s，微秒）；
offset: 时间补偿的结果（单位与：10^(-3)s，毫秒）；
jitter: Linux系统时间与BIOS硬件时间的差值（单位：10^(-6)s，微秒）。其绝对值越小，主机和对时服务器的时间就越接近；
*: 远端的服务器已经被确认为主NTP Server，系统时间将由这台机器所提供；
+: 作为辅助的NTP Server，与带有*号的服务器一起为我们提供同步服务. 当`*`号服务器不可用时，它就可以接管；
-: 远程服务器被clustering algorithm认为是不合格的NTP Server；
x: 远程服务器不可用；
```

