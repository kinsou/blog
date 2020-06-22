title: Ubuntu安装JDK
tags:
  - Ubuntu
  - JDK
categories:
  - Ubuntu
date: 2016-03-10 17:27:00
---
## 一.jdk1.8安装
### 1. 从网站上下载jdk1.8包(jdk-8u73-linux-x64.tar.gz )

### 2.解压到 /usr/java/目录下，
解压安装到：
```shell
tar zxvf jdk-8u73-linux-x64.tar.gz  -C /usr/java/

ln -s /usr/java/jdk1.8.0_73  /usr/java/jdk
```

### 3.环境变量配置：
 (/etc/profile文件中添加：)
```shell
 vi  /etc/profile
 JAVA_HOME=/usr/java/jdk
 PATH=$PATH:$JAVA_HOME/bin:$JAVA_HOME/jre/bin
 CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
 export JAVA_HOME PATH CLASSPATH
 ```
 添加完毕保存退出
```shell
 source /etc/profile
```
```shell
 sudo update-alternatives --install /usr/bin/java java /usr/java/jdk/bin/java 300
 sudo update-alternatives --install /usr/bin/javac javac /usr/java/jdk/bin/javac 300
 sudo update-alternatives  --install  /usr/bin/jar jar /usr/java/jdk/bin/jar 300
 sudo update-alternatives  --install  /usr/bin/javah javah /usr/java/jdk/bin/javah 300
 sudo update-alternatives  --install  /usr/bin/javap javap /usr/java/jdk/bin/javap 300
```
```shell
 java -version
```
显示 
 java version "1.8.0_73"
 Java(TM) SE Runtime Environment (build 1.8.0_73-b02)
 Java HotSpot(TM) 64-Bit Server VM (build 25.73-b02, mixed mode)