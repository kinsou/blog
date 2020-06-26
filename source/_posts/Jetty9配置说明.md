title: Jetty9配置说明
author: ZkName
tags:
  - jetty
  - Ubuntu
  - jetty9
categories: []
date: 2019-10-08 10:00:00
---
## Jetty9配置说明
##### 在Jetty的根目录下执行以下命令
```shell
java -jar start.jar --add-to-start=jvm
```
1、 start.ini目录内增加

```shell
--module=deploy,http,jsp,jstl,websocket,ext,resources,console-capture,jvm

```
2、 修改配置文件start.d/jvm.ini

```shell
# --------------------------------------- 
# Module: jvm
# A noop module that creates an ini template useful for
# setting JVM arguments (eg -Xmx )
# --------------------------------------- 
--module=jvm

## JVM Configuration
## If JVM args are include in an ini file then --exec is needed
## to start a new JVM from start.jar with the extra args.
##
## If you wish to avoid an extra JVM running, place JVM args
## on the normal command line and do not use --exec
--exec
-Xmx3072m
-Xmn1024m
# -XX:+UseConcMarkSweepGC
# -XX:ParallelCMSThreads=2
# -XX:+CMSClassUnloadingEnabled
# -XX:+UseCMSCompactAtFullCollection
# -XX:CMSInitiatingOccupancyFraction=80
# -internal:gc
# -XX:+PrintGCDateStamps
# -XX:+PrintGCTimeStamps
# -XX:+PrintGCDetails
# -XX:+PrintTenuringDistribution
# -XX:+PrintCommandLineFlags
# -XX:+DisableExplicitGC
```
3、查询模块已安装模块
```shell
java -jar start.jar --list-config
```