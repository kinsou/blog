title: Ubuntu18.04开机启动脚本
author: ZkName
tags:
  - Ubuntu
categories: []
date: 2020-04-02 15:25:00
---

```shell
vi /lib/systemd/system/rc.local.service

[Unit]
Description=/etc/rc.local Compatibility
ConditionFileIsExecutable=/etc/rc.local
After=network.target

[Service]
Type=forking
ExecStart=/etc/rc.local start
TimeoutSec=0
RemainAfterExit=yes


```

尾部添加内容
```shell
[Unit]
Description=/etc/rc.local Compatibility
ConditionFileIsExecutable=/etc/rc.local
After=network.target

[Service]
Type=forking
ExecStart=/etc/rc.local start
TimeoutSec=0
RemainAfterExit=yes


[Install]  
WantedBy=multi-user.target  
Alias=rc-local.service
```

新建文件
```shell
vi /etc/rc.local 
```

软链
```shell
ln -s /lib/systemd/system/rc.local.service /etc/systemd/system/
```
