title: tomcat memcached-session-manager使用spring security序列化问题
tags:
  - Tomcat
  - Java
categories:
  - Java
date: 2013-05-09 10:40:00
---
## tomcat异常：
```java
警告: Could not load session with id 2CD7BCC8414A6DF09EF97E07FBCDABD3-n2 from memcached.
com.esotericsoftware.kryo.SerializationException: Unable to deserialize object of type: java.util.concurrent.ConcurrentHashMap
	at com.esotericsoftware.kryo.Kryo.readObject(Kryo.java:593)
	at com.esotericsoftware.kryo.ObjectBuffer.readObject(ObjectBuffer.java:213)
	at de.javakaffee.web.msm.serializer.kryo.KryoTranscoder.deserializeAttributes(KryoTranscoder.java:261)
	at de.javakaffee.web.msm.TranscoderService.deserializeAttributes(TranscoderService.java:169)
	at de.javakaffee.web.msm.TranscoderService.deserialize(TranscoderService.java:126)
	at de.javakaffee.web.msm.MemcachedSessionService.loadFromMemcached(MemcachedSessionService.java:1119)
	at de.javakaffee.web.msm.MemcachedSessionService.findSession(MemcachedSessionService.java:597)
	at de.javakaffee.web.msm.MemcachedBackupSessionManager.findSession(MemcachedBackupSessionManager.java:216)
	at org.apache.catalina.connector.Request.doGetSession(Request.java:2419)
	at org.apache.catalina.connector.Request.getSession(Request.java:2157)
	at org.apache.catalina.connector.RequestFacade.getSession(RequestFacade.java:833)
	at org.apache.catalina.connector.RequestFacade.getSession(RequestFacade.java:844)
	at org.apache.jasper.runtime.PageContextImpl._initialize(PageContextImpl.java:146)
	at org.apache.jasper.runtime.PageContextImpl.initialize(PageContextImpl.java:124)
	at org.apache.jasper.runtime.JspFactoryImpl.internalGetPageContext(JspFactoryImpl.java:107)
	at org.apache.jasper.runtime.JspFactoryImpl.getPageContext(JspFactoryImpl.java:63)
	at org.apache.jsp.login_jsp._jspService(login_jsp.java:61)
	at org.apache.jasper.runtime.HttpJspBase.service(HttpJspBase.java:70)
	at javax.servlet.http.HttpServlet.service(HttpServlet.java:717)
	at org.apache.jasper.servlet.JspServletWrapper.service(JspServletWrapper.java:388)
	at org.apache.jasper.servlet.JspServlet.serviceJspFile(JspServlet.java:313)
	at org.apache.jasper.servlet.JspServlet.service(JspServlet.java:260)
	at javax.servlet.http.HttpServlet.service(HttpServlet.java:717)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:290)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:206)
	at org.springframework.web.filter.CharacterEncodingFilter.doFilterInternal(CharacterEncodingFilter.java:88)
	at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:76)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:235)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:206)
	at com.autoradio.mz.util.filter.AddHttpHeaderFilter.doFilter(AddHttpHeaderFilter.java:29)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:235)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:206)
	at org.apache.catalina.core.StandardWrapperValve.invoke(StandardWrapperValve.java:233)
	at org.apache.catalina.core.StandardContextValve.invoke(StandardContextValve.java:191)
	at de.javakaffee.web.msm.RequestTrackingContextValve.invoke(RequestTrackingContextValve.java:99)
	at org.apache.catalina.core.StandardHostValve.invoke(StandardHostValve.java:127)
	at de.javakaffee.web.msm.RequestTrackingHostValve.invoke(RequestTrackingHostValve.java:165)
	at org.apache.catalina.valves.ErrorReportValve.invoke(ErrorReportValve.java:102)
	at org.apache.catalina.core.StandardEngineValve.invoke(StandardEngineValve.java:109)
	at org.apache.catalina.connector.CoyoteAdapter.service(CoyoteAdapter.java:293)
	at org.apache.coyote.http11.Http11Processor.process(Http11Processor.java:859)
	at org.apache.coyote.http11.Http11Protocol$Http11ConnectionHandler.process(Http11Protocol.java:602)
	at org.apache.tomcat.util.net.JIoEndpoint$Worker.run(JIoEndpoint.java:489)
	at java.lang.Thread.run(Thread.java:662)
Caused by: com.esotericsoftware.kryo.SerializationException: Unable to deserialize object of type: org.springframework.security.core.context.SecurityContextImpl
	at com.esotericsoftware.kryo.Kryo.readClassAndObject(Kryo.java:571)
	at com.esotericsoftware.kryo.serialize.MapSerializer.readObjectData(MapSerializer.java:129)
	at com.esotericsoftware.kryo.Serializer.readObject(Serializer.java:61)
	at com.esotericsoftware.kryo.Kryo.readObject(Kryo.java:589)
	... 43 more
Caused by: com.esotericsoftware.kryo.SerializationException: Serialization trace:
authorities (com.autoradio.mz.security.springsecurity.LoginUser)
principal (org.springframework.security.authentication.UsernamePasswordAuthenticationToken)
authentication (org.springframework.security.core.context.SecurityContextImpl)
	at com.esotericsoftware.kryo.serialize.FieldSerializer.readObjectData(FieldSerializer.java:238)
	at com.esotericsoftware.kryo.serialize.ReferenceFieldSerializer.readObjectData(ReferenceFieldSerializer.java:81)
	at com.esotericsoftware.kryo.serialize.FieldSerializer.readObjectData(FieldSerializer.java:220)
	at com.esotericsoftware.kryo.serialize.ReferenceFieldSerializer.readObjectData(ReferenceFieldSerializer.java:81)
	at com.esotericsoftware.kryo.serialize.FieldSerializer.readObjectData(FieldSerializer.java:220)
	at com.esotericsoftware.kryo.serialize.ReferenceFieldSerializer.readObjectData(ReferenceFieldSerializer.java:81)
	at com.esotericsoftware.kryo.Kryo.readClassAndObject(Kryo.java:566)
	... 46 more
Caused by: java.lang.ClassCastException: org.springframework.security.core.authority.SimpleGrantedAuthority cannot be cast to java.lang.Comparable
	at java.util.TreeMap.put(TreeMap.java:542)
	at java.util.TreeSet.add(TreeSet.java:238)
	at com.esotericsoftware.kryo.serialize.CollectionSerializer.readObjectData(CollectionSerializer.java:113)
	at com.esotericsoftware.kryo.Kryo.readClassAndObject(Kryo.java:566)
	at de.javakaffee.kryoserializers.UnmodifiableCollectionsSerializer.readObjectData(UnmodifiableCollectionsSerializer.java:84)
	at com.esotericsoftware.kryo.serialize.FieldSerializer.readObjectData(FieldSerializer.java:220)
	... 52 more
```
-----------------------------------------------------
发现 SimpleGrantedAuthority 转换类型错误；


## 解决
可以使用自定义序列化对象沿用java自身的序列化实现：

```java
import com.esotericsoftware.kryo.Kryo;
import com.esotericsoftware.kryo.serialize.SerializableSerializer;
import de.javakaffee.web.msm.serializer.kryo.KryoCustomization;

public class CustomKryoRegistration implements KryoCustomization {
	public void customize(Kryo kryo) {
	    kryo.register(org.springframework.security.core.userdetails.User.class, new SerializableSerializer());
	}
}
```
## XML customConverter添加 CustomKryoRegistration类：
```xml
    <Manager className="de.javakaffee.web.msm.MemcachedBackupSessionManager" sticky="false" memcachedNodes="n1:192.168.0.124:11211 n2:192.168.0.123:11211" lockingMode="uriPattern:/path1|/path2" requestUriIgnorePattern=".*\.(png|gif|jpg|css|js|ico)$" sessionBackupAsync="false" transcoderFactoryClass="de.javakaffee.web.msm.serializer.kryo.KryoTranscoderFactory" customConverter="CustomKryoRegistration" />
```

## 高效序列化实现请自行编写继承对象：
```java
com.esotericsoftware.kryo.Serializer.java
```
