title: LKL一键包 BBR（适用Openvz）
author: ZkName
tags:
  - Ubuntu
  - bbr
  - 搬瓦工
categories: []
date: 2017-04-10 18:17:00
---
### LKL使用前置需求
1. LKL要求ldd的版本至少在2.14，目前我测试下来，如果不想折腾建议直接安装CentOS7，Debian8和Ubuntu16
2. 安装包只使用64bit的系统。
3. 默认的端口转发只转发了9000-9999的端口，如果你不想费心修改，请把ssr等应用的端口设在这个范围
4. 只适用openvz，请他虚拟请参考原帖自己折腾。。

### 安装LKL一键包命令：
```shle
wget --no-check-certificate https://github.com/91yun/uml/raw/master/lkl/install.sh && bash install.sh
```
### 如何判断是否安装成功
```shle
ping 10.0.0.2
```
如果10.0.0.2能ping通说明成功，ping不通说明失败

### 如果修改转发端口
1. 修改/root/lkl/run.sh，查找9000-9999，改成你想要的端口段
2. 修改/root/lkl/haproxy.cfg查找9000-9999，改成你想要的端口段
3. 重启vps

### 91yun论坛转发