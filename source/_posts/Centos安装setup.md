title: Centos 安装 setup
tags:
  - Centos
categories:
  - Centos
date: 2013-05-08 23:59:00
---
## 安装setuptool
```shell
yum install setuptool
```
## 可以发现执行setup后不全，再安装一个用于系统服务管理
```shell
yum install ntsysv
```
## 再安装个防火墙，以及setup中配套的防火墙设置、网络设置
```shell
yum install iptables
```
## 安装setup中配套的防火墙设置
```shell
yum install system-config-securitylevel-tui
```
## 安装setup中配套的网络设置
```shell
yum install system-config-network-tui
```