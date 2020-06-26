title: Ubuntu 安装 nodejs
author: ZkName
tags:
  - nodejs
  - Ubuntu
categories: []
date: 2018-10-30 10:00:00
---
## Ubuntu 安装 nodejs
```shell
#下载
wget https://nodejs.org/dist/v8.12.0/node-v8.12.0-linux-x64.tar.xz
#解压
tar xf  node-v8.12.0-linux-x64.tar.xz -C /usr/local/
#环境变量配置增加
sudo vi /etc/profile

export NODE_HOME=/usr/local/node-v8.12.0-linux-x64
export PATH=$PATH:$NODE_HOME/bin 
export NODE_PATH=$NODE_HOME/lib/node_modules
```