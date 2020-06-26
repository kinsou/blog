title: 安装Hadoop2.5.0
tags:
  - Hadoop
categories:
  - Java
date: 2014-08-27 18:27:00
---
## 安装Hadoop，单机模式。

### 1、免密码ssh设置：
[免密码ssh设置](/2014/08/27/ubuntu使用ssh-keygen设置ssh无密码登录/ "免密码ssh设置")

### 2、JDK安装配置：
[JDK安装配置](/2014/08/27/ubuntu%20安装%20jdk/ "JDK安装配置")

### 3、我们把下载好的hadoop-2.5.0.tar.gz解压形成/usr/local/hadoop-2.5.0/并配置环境变量，同JAVA_HOME类似，在/etc/profile文件中添加如下配置：
```shell
#set hadoop environment
export HADOOP_HOME=/usr/local/hadoop-2.5.0/
export PATH=$PATH:$HADOOP_HOME/bin
export PATH=$PATH:$HADOOP_HOME/sbin
```

### 4、修改配置文件

修改的文件都在/usr/local/hadoop-2.5.0/etc/hadoop下：

core-site.xml、hdfs-site.xml、yarn-site.xml 、mapred-site.xml。

配置文件的添加和修改都在<configuration></configuration> 中

#### core-site.xml
```xml
<property>
  <name>fs.defaultFS</name>
  <value>hdfs://localhost:9000</value>
</property>

<property>
  <name>hadoop.tmp.dir</name>
  <value>/data/hadoop/hadoop_tmp</value>
</property>
```
添加hdfs的指定URL路径，由于是伪分布模式，所以配置的是本机IP ，可为真实ip、localhost。

#### hdfs-site.xml
```xml
<property>
  <name>dfs.namenode.name.dir</name>
  <value>/data/hadoop/namenode</value>
</property>

<property>
  <name>dfs.datanode.data.dir</name>
  <value>/data/hadoop/datanode</value>
</property>

<property>
  <name>dfs.replication</name>
  <value>1</value>
</property>
```
主要是对namenode 和 datanode 存储路径的设置。为了便于管理，最好配置一下。

#### mapred-site.xml
```xml
<property>
  <name>mapreduce.framework.name</name>
  <value>yarn</value>
</property>
```
hadoop2.0有了yarn，所以原来的mapred配置都转向yarn-site.xml文件中了，这里也就指定yarn。

#### yarn-site.xml 

为了简单，快速做测试，使用默认的即可。

### 5、启动hadoop

启动的文件都是 sbin下，bin下的都是命令。

使用命令cd $HADOOP_HOME切换到该安装目录下

首先格式化 namenode
```shell
bin/hdfs namenode -format
```
确定不报错，且出现
```shell
14/08/27 18:19:49 INFO util.GSet: capacity      = 2^15 = 32768 entries
14/08/27 18:19:49 INFO namenode.NNConf: ACLs enabled? false
14/08/27 18:19:49 INFO namenode.NNConf: XAttrs enabled? true
14/08/27 18:19:49 INFO namenode.NNConf: Maximum size of an xattr: 16384
14/08/27 18:19:49 INFO namenode.FSImage: Allocated new BlockPoolId: BP-409433172-127.0.1.1-1409134789102
14/08/27 18:19:49 INFO common.Storage: Storage directory /data/hadoop/namenode has been successfully formatted.
14/08/27 18:19:49 INFO namenode.NNStorageRetentionManager: Going to retain 1 images with txid >= 0
14/08/27 18:19:49 INFO util.ExitUtil: Exiting with status 0
14/08/27 18:19:49 INFO namenode.NameNode: SHUTDOWN_MSG: 
/************************************************************
SHUTDOWN_MSG: Shutting down NameNode at ubuntu/127.0.1.1
************************************************************/
```
启动namenode
```shell
root@ubuntu:/usr/local/hadoop-2.5.0/sbin# ./hadoop-daemon.sh start namenode
starting namenode, logging to /usr/local/hadoop-2.5.0/logs/hadoop-root-namenode-ubuntu.out
root@ubuntu:/usr/local/hadoop-2.5.0/sbin# ./hadoop-daemon.sh start datanode
starting datanode, logging to /usr/local/hadoop-2.5.0/logs/hadoop-root-datanode-ubuntu.out
root@ubuntu:/usr/local/hadoop-2.5.0/sbin# jps
8865 NameNode
9009 Jps
8945 DataNode
```
启动成功可以使用sbin/hadoop-daemon.sh stop datanode（或namenode）来关闭。

启动Manage管理
```shell
root@ubuntu:/usr/local/hadoop-2.5.0/sbin# ./yarn-daemon.sh start resourcemanager
starting resourcemanager, logging to /usr/local/hadoop-2.5.0/logs/yarn-root-resourcemanager-ubuntu.out
root@ubuntu:/usr/local/hadoop-2.5.0/sbin# ./yarn-daemon.sh start nodemanager
starting nodemanager, logging to /usr/local/hadoop-2.5.0/logs/yarn-root-nodemanager-ubuntu.out
root@ubuntu:/usr/local/hadoop-2.5.0/sbin# jps
8865 NameNode
8945 DataNode
9362 Jps
9275 NodeManager
9035 ResourceManager
```

证明启动成功 同时也可以使用yarn-daemon.sh stop resourcemanager（nodemanager）来关闭。

如果没有单独配置yarn-site.xml中的yarn.resourcemanager.webapp.address，默认的端口8088 访问

http://127.0.0.1:8088/  可以访问hadoop管理页面

如果没有单独配置 hdfs-site.xml中的dfs.namenode.http-address,默认端口50070

http://127.0.0.1:50070 可以访问namenode节点信息。
