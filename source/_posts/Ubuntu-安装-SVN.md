title: Ubuntu 安装 SVN 一键脚本
author: ZkName
tags:
  - Ubuntu
  - SVN
  - svn
date: 2018-12-13 12:27:00
---
## SVN安装
```
apt-get install subversion
```
#### 1. 创建svn根目录
```
sudo mkdir /home/svn/

```

#### 2. 使用svn命令创建SVN文件仓库
```
sudo svnadmin create /home/svn/
```
## 配置svn

#### 1. 配置用户名密码
```
vi /home/svn/conf/passwd

[users]
# harry = harryssecret
# sally = sallyssecret
test = test  # 添加用户密码
```

#### 2. 配置分组权限
```
vi /home/svn/conf/authz

[groups]
manager = test

#[repository:/svn]
@manager = rw
```

#### 3. svn全局配置，启用用户名密码，分组等
```
vi /home/svn/conf/svnserve.conf

anon-access = none
auth-access = write
password-db = passwd
authz-db = authz
```

#### 启动svn服务
```
svnserve -d -r /home/svn/
```







