title: eclipse安装插件慢
tags:
  - eclipse
  - java
categories:
  - eclipse
date: 2018-12-28 17:27:00
---

### 1. eclipse安装插件慢使用国内镜像
```
#1.企业贡献： 
搜狐开源镜像站：http://mirrors.sohu.com/ 
网易开源镜像站：http://mirrors.163.com/ 
首都在线科技股份有限公司：http://mirrors.yun-idc.com/ 

#2.大学教学： 
北京交通大学： http://mirror.bjtu.edu.cn (IPv4 only) 
http://mirror6.bjtu.edu.cn (IPv6 only) 
http://debian.bjtu.edu.cn(IPv4+IPv6) 

上海交通大学： 
http://ftp.sjtu.edu.cn/ (IPv4 only) 
http://ftp6.sjtu.edu.cn (IPv6 only) 

清华大学： 
http://mirrors.tuna.tsinghua.edu.cn/ (IPv4+IPv6) 
http://mirrors.6.tuna.tsinghua.edu.cn/ (IPv6 only) 
http://mirrors.4.tuna.tsinghua.edu.cn/ (IPv4 only) 

天津大学：http://mirror.tju.edu.cn/ 
浙江大学：http://mirrors.zju.edu.cn/ 

中国科学技术大学： 
http://mirrors.ustc.edu.cn/ (IPv4+IPv6) 
http://mirrors4.ustc.edu.cn/ 
http://mirrors6.ustc.edu.cn/ 
```

### 2. 安装nginx
```
#nginx.conf

server {  
    listen 80;  
    server_name  download.eclipse.org;  
    #charset koi8-r;  
    #access_log  logs/host.access.log  main;  
    location / {  
        proxy_pass https://mirrors.ustc.edu.cn/eclipse/;  
    }
}
```

### 3. 修改host文件 
```
127.0.0.1  download.eclipse.org  
```
