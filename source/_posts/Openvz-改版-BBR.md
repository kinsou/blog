title: Openvz 改版 BBR
author: ZkName
tags:
  - bbr
  - Ubuntu
categories: []
date: 2017-07-19 17:26:00
---
### github 项目地址

[https://github.com/linhua55/lkl_study](https://github.com/linhua55/lkl_study "https://github.com/linhua55/lkl_study")

### 安装命令：
```shle
curl https://raw.githubusercontent.com/linhua55/lkl_study/master/get-rinetd.sh | bash
```
##### 修改配置文件：vi /etc/rinetd-bbr.conf
```shle
# bindadress bindport connectaddress connectport
0.0.0.0 443 0.0.0.0 443
0.0.0.0 80 0.0.0.0 80
```

### iptables
```shle
iptables -A INPUT -p tcp --destination-port 443 -j DROP
iptables -A INPUT -p tcp --destination-port 80 -j DROP
```

### 查看是否成功 rinetd-bbr 
暂时只能使用top 命令查看cpu占用率
```shle
top - 17:39:34 up 45 min,  2 users,  load average: 0.00, 0.01, 0.00
Tasks:  23 total,   1 running,  22 sleeping,   0 stopped,   0 zombie
%Cpu(s):  0.0 us,  0.0 sy,  0.0 ni,100.0 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
KiB Mem:    524288 total,   131240 used,   393048 free,        0 buffers
KiB Swap:    65536 total,        0 used,    65536 free.    41152 cached Mem

  PID USER      PR  NI    VIRT    RES    SHR S %CPU %MEM     TIME+ COMMAND                                                                                                                                                       
  294 root      20   0  518592  11792   2524 S  1.3  2.2   0:44.73 rinetd-bbr                                                                                                                                                    
    1 root      20   0   37060   3612   2352 S  0.0  0.7   0:00.25 systemd                                                                                                                                                       
    2 root      20   0       0      0      0 S  0.0  0.0   0:00.00 kthreadd/120973                                                                                                                                               
    3 root      20   0       0      0      0 S  0.0  0.0   0:00.00 khelper/120973                                                                                                                                                
   59 root      20   0   41464   1800   1316 S  0.0  0.3   0:00.00 systemd-udevd                                                                                                                                                 
   60 root      20   0   31108   2028   1728 S  0.0  0.4   0:00.09 systemd-journal                                                                                                                                               
  289 systemd+  20   0   26520   1608   1344 S  0.0  0.3   0:00.04 systemd-network                                                                                                                                               
  290 root      20   0   25988   1180    948 S  0.0  0.2   0:00.00 cron                                                                                                                                                          
  299 root      20   0   69872   3344   2604 S  0.0  0.6   0:00.00 sshd                                                                                                                                                                   
  377 root      20   0   56932  11860   1760 S  0.0  2.3   0:00.33 supervisord                                                                                                                                                   
  379 root      20   0   60860  12120   2292 S  0.0  2.3   0:16.00 python                                                                                                                                                        
  386 kcptun    20   0    9420   3900   2908 S  0.0  0.7   0:00.01 server_linux_am                                                                                                                                               
  571 root      20   0   97404   4124   3116 S  0.0  0.8   0:00.11 sshd                                                                                                                                                          
  582 root      20   0   18240   2116   1556 S  0.0  0.4   0:00.00 bash                                                                                                                                                          
  716 root      20   0   97404   4080   3120 S  0.0  0.8   0:00.01 sshd                                                                                                                                                          
  727 root      20   0   18240   2084   1524 S  0.0  0.4   0:00.00 bash                                                                                                                                                          
  738 root      20   0   20000   1604   1080 R  0.0  0.3   0:00.02 top 
  
  ```