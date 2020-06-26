title: Eclipse使用Maven插件异常
tags:
  - Eclipse
  - Maven
categories:
  - Eclipse
date: 2015-12-28 10:35:00
---
1. eclipse中使用maven插件的时候，运行run as maven build的时候报错：
```
-Dmaven.multiModuleProjectDirectory system propery is not set. Check $M2_HOME environment variable and mvn script match.
```
可以设一个环境变量M2_HOME指向你的maven安装目录
M2_HOME=H:\Java\tools\apache-maven-3.3.9
然后在Window->Preference->Java->Installed JREs->Edit
在Default VM arguments中设置
```
-Dmaven.multiModuleProjectDirectory=$M2_HOME
```
![eclipse jdk配置](/img/20151228100517.png)