title: Google Chrome 用户数据（User Data）默认目录配置 
author: ZkName
tags:
  - Google
  - Chrome 
categories: []
date: 2019-02-18 12:26:00
---

### Google Chrome 用户数据（User Data）默认目录配置 ：
1. 在你想要存放数据的盘符下创建文件夹，假设为
```cmd
E:\Chrome\User Data
```
2. 开始->附件->命令提示符（右键以管理员身份运行） 

3. 输入
```cmd
CD C:\Users\你的用户名\AppData\Local\Google\Chrome 
```

4. 输入RMDIR /S “User Data”，提示是否删除输入Y 
```cmd
RMDIR /S “ser Data”
```

5. 输入MKLINK /J "User Data" "E:\Chrome\User Data" 
```cmd
MKLINK /J "User Data" "E:\Chrome\User Data" 
```

6. 启动浏览器生效。
