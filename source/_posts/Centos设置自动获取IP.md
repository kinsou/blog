title: Centos设置自动获取IP
tags:
  - Centos
categories:
  - Centos
date: 2013-05-05 11:51:00
---
## 编辑文件：
```shell
vi /etc/sysconfig/network-scripts/ifcfg-eth0
```
## 修改：
```shell
ONBOOT=yes
BOOTPROTO=dhcp
```
## 重启网络:
```shell
service network restart
```