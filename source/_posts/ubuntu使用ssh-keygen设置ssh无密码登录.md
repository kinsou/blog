title: ubuntu使用ssh-keygen设置ssh无密码登录
tags:
  - Ubuntu
categories:
  - Ubuntu
date: 2014-08-27 17:55:00
---
## 输入时，会提示创建.ssh/id_rsa、id_rsa.pub的文件，其中第一个为密钥，第二个为公钥。过程中会要求输入密码，为了ssh访问过程无须密码，直接回车 。

```shell
root@ubuntu:~# ssh-keygen -t rsa
Generating public/private rsa key pair.
Enter file in which to save the key (/root/.ssh/id_rsa): 
Created directory '/root/.ssh'.
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /root/.ssh/id_rsa.
Your public key has been saved in /root/.ssh/id_rsa.pub.
The key fingerprint is:
84:50:44:e7:22:e1:f0:75:01:f2:c8:e9:45:39:66:70 root@ubuntu
The key's randomart image is:
+--[ RSA 2048]----+
|  . ==Eo+.       |
|   = @==         |
|    Bo=.o        |
|   . o o         |
|    .   S        |
|                 |
|                 |
|                 |
|                 |
+-----------------+
```

## 公钥复制，本机直接复制
```shell
root@ubuntu:~/.ssh# cp id_rsa.pub authorized_keys
```

## 复制密码
```shell
# 192.168.1.11 服务器输入
ssh-copy-id -i ~/.ssh/id_rsa.pub -p22 root@192.168.1.10
# 192.168.1.10 服务器输入
ssh-copy-id -i ~/.ssh/id_rsa.pub -p22 root@192.168.1.11
```

# 登录
```shell
root@ubuntu:~/.ssh# ssh localhost
```



