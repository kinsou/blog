title: Centos配置nfs
tags:
  - Centos
categories:
  - Centos
date: 2013-05-13 09:43:00
---
## 1、配置：
### 服务端：
```shell
#vi /etc/exports 
增加例如：
/opt/storage　192.168.0.*(rw)　　 (IP)就是客户端允许访问ip地址(rw) 权限
```
### 客户端：
```shell
#mount -t nfs 192.168.1.152:/opt/storage/  /152  （/152）为共享本地映射
#showmount –export 192.168.1.152   查看NFS所发布的目录
权限配置：
#chown -R user /152
```
## 2、启动命令：
```shell
#service portmap start
#service nfslock start
#service nfs start
```
## 3、卸载共享：
```shell
#umount -l /152  （/152）为共享本地映射
```
##4、端口：
```shell
1. portmap 端口 111 udp/tcp；
2. nfsd 端口 2049 udp/tcp；
```
## 5、开机启动配置：
```shell
vi /etc/auto.nas 在文件中添加一行:
/152 -rw,rsize=32768,wsize=32768,soft,intr 192.168.1.152:/opt/storage
vi /etc/auto.master,添加一行:
/nas /etc/auto.nas –timeout=0
```
注 意：–timeout=0表明一旦挂载就不会自动被卸载（umount）。也可以指定一个别的正数，比如600，那么如果600秒之内没有使用nfs就 会自动被卸载。如果没有–timeout参数部分，则默认为600秒（10分钟），这个参数在/etc/sysconfig/autofs文件中可以用 TIMEOUT项指定。
------------------------------------------------------------

将autofs服务设置为开机自启动
先使用chkconfig –list autofs检查一下autofs服务是否已经设置为自启动了。
```shell
[root@~]# chkconfig –list autofs
autofs     0:off   1:off   2:off   3:on    4:on    5:on    6:off
```
如果你发现输出中全部为off，使用chkconfig autofs on设置为开机自启动。
```shell
[root@~]# chkconfig autofs on
```
注：autofs实际上是使用automount命令来处理的。