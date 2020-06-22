title: linux 常用命令
tags:
  - Ubuntu
  - Linux
categories:
  - Ubuntu
date: 2014-10-16 10:14:00
---
## 简介
#### linux常用命令
### scp
```shell
#文件复制
scp /home/root/music/1.mp3 root@192.168.1.100:/home/root/others/music
scp /home/root/music/1.mp3 root@192.168.1.100:/home/root/others/music/001.mp3
#目录复制
scp -r /home/root/music/ root@192.168.1.100:/home/root/others/
#远程文件复制
scp root@192.168.1.100:/home/root/others/music /home/root/music/1.mp3
#远程目录复制
scp -r root@192.168.1.100:/home/root/others/ /home/root/music/
```
