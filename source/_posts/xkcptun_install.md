title: Xkcptun 改版的 kcptun
author: ZkName
tags:
  - kcptun
  - xkcptun 
  - Ubuntu
categories: []
date: 2017-10-18 15:26:00
---
### github 项目地址

[https://github.com/liudf0716/xkcptun](https://github.com/liudf0716/xkcptun "https://github.com/liudf0716/xkcptun")

### 安装：
xkcptun依赖libevent2
安装libevent2库后 (apt-get install libevent-dev)

```shle
git clone https://github.com/liudf0716/xkcptun.git

cd xkcptun

mkdir build && cd build

cmake ..

make
```
build下生成 xkcp_client, xkcp_server, xkcp_spy

##### 注册服务
```shle
mkdir /etc/xkcptun
cp xkcp_server /usr/local/bin/
cp server.json /etc/xkcptun/
cp xkcptun.service /lib/systemd/system/xkcptun.service

systemctl enable xkcptun
systemctl start xkcptun
systemctl status xkcptun
```

### server.json 配置文件例子 

```json
{
  "localinterface": "eth0",
  "localport": 9089,
  "remoteaddr": "127.0.0.1",
  "remoteport": 443,
  "key": "14789632a",
  "crypt": "none",
  "mode": "fast3",
  "mtu": 1350,
  "sndwnd": 4096,
  "rcvwnd": 512,
  "datashard": 10,
  "parityshard": 3,
  "dscp": 0,
  "nocomp": true,
  "acknodelay": false,
  "nodelay": 0,
  "interval": 20,
  "resend": 2,
  "nc": 1,
  "sockbuf": 4194304,
  "keepalive": 10
}
  
  ```