title: wechat-javax.net.ssl.SSLException异常
tags:
  - Java
  - Wechat
categories:
  - Java
date: 2015-02-02 18:27:00
---
## 在使用微信公众平台开发模式(JAVA) SDK 发现调用https的异常：
```
/**
 * 微信公众平台开发模式(JAVA) SDK
 * (c) 2012-2013 ____′↘夏悸 <wmails@126.cn>, MIT Licensed
 * http://www.jeasyuicn.com/wechat
 */
```
```java
java.util.concurrent.ExecutionException: java.net.ConnectException: Received fatal alert: bad_record_mac to https://api.weixin.qq.com/cgi-bin/user/info?openid=#&access_token=#
	at com.ning.http.client.providers.netty.NettyResponseFuture.abort(NettyResponseFuture.java:342)
	at com.ning.http.client.providers.netty.NettyConnectListener.operationComplete(NettyConnectListener.java:108)
	at org.jboss.netty.channel.DefaultChannelFuture.notifyListener(DefaultChannelFuture.java:427)
	at org.jboss.netty.channel.DefaultChannelFuture.notifyListeners(DefaultChannelFuture.java:413)
	at org.jboss.netty.channel.DefaultChannelFuture.setFailure(DefaultChannelFuture.java:380)
	at org.jboss.netty.handler.ssl.SslHandler.setHandshakeFailure(SslHandler.java:1566)
	at org.jboss.netty.handler.ssl.SslHandler.unwrap(SslHandler.java:1368)
	at org.jboss.netty.handler.ssl.SslHandler.decode(SslHandler.java:917)
	at org.jboss.netty.handler.codec.frame.FrameDecoder.callDecode(FrameDecoder.java:425)
	at org.jboss.netty.handler.codec.frame.FrameDecoder.messageReceived(FrameDecoder.java:303)
	at org.jboss.netty.channel.SimpleChannelUpstreamHandler.handleUpstream(SimpleChannelUpstreamHandler.java:70)
	at org.jboss.netty.channel.DefaultChannelPipeline.sendUpstream(DefaultChannelPipeline.java:564)
	at org.jboss.netty.channel.DefaultChannelPipeline.sendUpstream(DefaultChannelPipeline.java:559)
	at org.jboss.netty.channel.Channels.fireMessageReceived(Channels.java:268)
	at org.jboss.netty.channel.Channels.fireMessageReceived(Channels.java:255)
	at org.jboss.netty.channel.socket.nio.NioWorker.read(NioWorker.java:88)
	at org.jboss.netty.channel.socket.nio.AbstractNioWorker.process(AbstractNioWorker.java:108)
	at org.jboss.netty.channel.socket.nio.AbstractNioSelector.run(AbstractNioSelector.java:318)
	at org.jboss.netty.channel.socket.nio.AbstractNioWorker.run(AbstractNioWorker.java:89)
	at org.jboss.netty.channel.socket.nio.NioWorker.run(NioWorker.java:178)
	at org.jboss.netty.util.ThreadRenamingRunnable.run(ThreadRenamingRunnable.java:108)
	at org.jboss.netty.util.internal.DeadLockProofWorker$1.run(DeadLockProofWorker.java:42)
	at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1145)
	at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:615)
	at java.lang.Thread.run(Thread.java:744)
Caused by: java.net.ConnectException: Received fatal alert: bad_record_mac to https://api.weixin.qq.com/cgi-bin/user/info?openid=#&access_token=#
	at com.ning.http.client.providers.netty.NettyConnectListener.operationComplete(NettyConnectListener.java:104)
	... 23 more
Caused by: javax.net.ssl.SSLException: Received fatal alert: bad_record_mac
	at sun.security.ssl.Alerts.getSSLException(Alerts.java:208)
	at sun.security.ssl.SSLEngineImpl.fatal(SSLEngineImpl.java:1619)
	at sun.security.ssl.SSLEngineImpl.fatal(SSLEngineImpl.java:1587)
	at sun.security.ssl.SSLEngineImpl.recvAlert(SSLEngineImpl.java:1756)
	at sun.security.ssl.SSLEngineImpl.readRecord(SSLEngineImpl.java:1060)
	at sun.security.ssl.SSLEngineImpl.readNetRecord(SSLEngineImpl.java:884)
	at sun.security.ssl.SSLEngineImpl.unwrap(SSLEngineImpl.java:758)
	at javax.net.ssl.SSLEngine.unwrap(SSLEngine.java:624)
	at org.jboss.netty.handler.ssl.SslHandler.unwrap(SslHandler.java:1282)
	at org.jboss.netty.handler.ssl.SslHandler.decode(SslHandler.java:917)
	at org.jboss.netty.handler.codec.frame.FrameDecoder.callDecode(FrameDecoder.java:425)
	at org.jboss.netty.handler.codec.frame.FrameDecoder.messageReceived(FrameDecoder.java:303)
	at org.jboss.netty.channel.Channels.fireMessageReceived(Channels.java:268)
	at org.jboss.netty.channel.Channels.fireMessageReceived(Channels.java:255)
	at org.jboss.netty.channel.socket.nio.NioWorker.read(NioWorker.java:88)
	at org.jboss.netty.channel.socket.nio.AbstractNioWorker.process(AbstractNioWorker.java:108)
	at org.jboss.netty.channel.socket.nio.AbstractNioSelector.run(AbstractNioSelector.java:318)
	at org.jboss.netty.channel.socket.nio.AbstractNioWorker.run(AbstractNioWorker.java:89)
	at org.jboss.netty.channel.socket.nio.NioWorker.run(NioWorker.java:178)
	... 3 more
```

## 解决方法com.gson.util.HttpKit.java 修改：
### 原内容
```java
        AsyncHttpClient http = new AsyncHttpClient();
        AsyncHttpClient.BoundRequestBuilder builder = http.prepareGet(url);
```

### 修改为：
```java
        AsyncHttpClient http = new AsyncHttpClient(new ApacheAsyncHttpProvider (new AsyncHttpClientConfig.Builder().build()));
        AsyncHttpClient.BoundRequestBuilder builder = http.prepareGet(url);
```