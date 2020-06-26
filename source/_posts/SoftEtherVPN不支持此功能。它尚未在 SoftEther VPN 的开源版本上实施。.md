title: SoftEtherVPN 不支持此功能。它尚未在 SoftEther VPN 的开源版本上实施。
tags:
  - VPM
categories:
  - SoftEtherVPN
date: 2019-12-19 12:50:00
---


##### 静态路由表下发功能无法使用：

不支持此功能。它尚未在 SoftEther VPN 的开源版本上实施。
```
源码
src\Cedar\server.c
删除 SiIsEnterpriseFunctionsRestrictedOnOpenSource 方法内容

if (StrCmpi(region, "JP") == 0 || StrCmpi(region, "CN") == 0)
{
		ret = true;
}

重新编译
```

##### 我编译好的地址

链接: <https://pan.baidu.com/s/195glDSOX7TEn6HhvwHH_Ow>
提取码: 4pnu

