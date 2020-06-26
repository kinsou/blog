title: Debian9安装vim和vim无法右键鼠标粘贴解决方法
tags:
  - Debian
categories:
  - Debian
date: 2020-01-08 12:50:00
---


##### 安装
```
apt-get install vim
```
##### 修改vim配置文件
```
vi /usr/share/vim/vim80/defaults.vim
```

70行 set mouse=a 修改为 set mouse-=a

```
if has('mouse')
  set mouse-=a
endif
```



