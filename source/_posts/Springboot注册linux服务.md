title: Springboot注册linux服务
author: ZkName
tags:
  - SpringBoot
  - Spring
categories: []
date: 2017-08-03 16:08:00
---
##### 1、设置jar|war权限
```shell
# 确保jar文件有执行权限
chmod 500 demo.jar
# 创建jar文件到/etc/init.d/的软连接
ln -s /home/demo.jar /etc/init.d/demo.conf配置文件

```
###### demo.conf配置文件
```shell
JAVA_OPTS="-Xms1024m -Xmx2048m"
RUN_ARGS="--server.port=8080 --logging.level=INFO --spring.thymeleaf.cache=true --logging.file=/app/log/demo/demo.log" 
```
##### 2、使用service命令运行应用
```shell
service demo start|stop|restart|status
```

##### 3、开机启动
###### 1.启动
```shell
update-rc.d demo defaults
```
###### 1.关闭启动
```shell
update-rc.d demo disable
```
###### 1.删除启动
```shell
update-rc.d demo remove
```