title: Spring多事务绑定
author: ZkName
tags:
  - Spring
  - Java
categories: []
date: 2017-08-16 16:55:00
---
###### 1、maven 使用 spring-data-commons
```xml
		<dependency>
		    <groupId>org.springframework.data</groupId>
		    <artifactId>spring-data-commons</artifactId>
		    <version>1.13.6.RELEASE</version>
		</dependency>
```

###### 2、spring 配置文件
```xml
	<!-- 事务声明 -->
	<bean id="transactionManager1" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
		<property name="dataSource" ref="dataSource1" />
	</bean>
	<!-- 事务声明 -->
	<bean id="transactionManager2" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
		<property name="dataSource" ref="dataSource2" />
	</bean>
    <!-- 配置默认事务 -->
	<tx:annotation-driven transaction-manager="transactionManager1"  proxy-target-class="true" />
    
	<!-- 多事务绑定 -->
	<bean id="chainedTransactionManager" class="org.springframework.data.transaction.ChainedTransactionManager">
		<constructor-arg>
			<array>
				<ref bean="transactionManager1"/>
				<ref bean="transactionManager2"/>
			</array>
		</constructor-arg>
	</bean>

```
###### 3、java 测试可见已经回滚了

```java
	@Transactional(value="chainedTransactionManager",rollbackFor = Exception.class) 
	public void test() {
		//插入数据库
		save(obj1);
		//插入数据库
		save(obj2);
		//抛出异常
		if (true) {
			throw new Exception("error");
		}
	}
```