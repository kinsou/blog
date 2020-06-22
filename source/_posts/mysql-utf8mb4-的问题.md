title: mysql  emoji  utf8mb4 问题
tags:
  - Mysql
categories:
  - Mysql
date: 2016-05-17 14:28:00
---
## 一、前提
1、mysql的版本不能太低，低于5.5.3的版本不支持utf8mb4编码
2、将表中的对应字段，其字符集修改成utf8mb4
3、对于 JDBC 连接，需要使用 MySQL Connector/J 5.1.13（含）以上的版本。
4、JDBC 的连接串中，建议不配置 characterEncoding 选项。
## 二、解决方式
### 第一种通过 set names 命令设置会话字符集
```java
 String query = "set names utf8mb4";
 stat.execute(query);
```
### 第二种如果使用Druid连接池配置文件增加：
```xml
<property name="connectionInitSqls" value="set names utf8mb4;"/>
```
##### 完整配置：
```xml
<bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource" init-method="init" destroy-method="close">
        <property name="driverClassName" value="${jdbc-driver}"/>
        <property name="url" value="${jdbc-url}"/>
        <property name="username" value="${jdbc-user}"/>
        <property name="password" value="${jdbc-password}"/>
        <property name="filters" value="stat"/>
        <property name="maxActive" value="20"/>
        <property name="initialSize" value="1"/>
        <property name="maxWait" value="60000"/>
        <property name="minIdle" value="1"/>
        <property name="timeBetweenEvictionRunsMillis" value="3000"/>
        <property name="minEvictableIdleTimeMillis" value="300000"/>
        <property name="validationQuery" value="SELECT 'x'"/>
        <property name="testWhileIdle" value="true"/>
        <property name="testOnBorrow" value="false"/>
        <property name="testOnReturn" value="false"/>
        <property name="poolPreparedStatements" value="true"/>
        <property name="maxPoolPreparedStatementPerConnectionSize" value="20"/>
        <property name="connectionInitSqls" value="set names utf8mb4;"/>
</bean>
```