title: Cygwin的 vim 退格键 方向键混乱
date: 2014-08-27 10:22:00
tags: Cygwin
---
## Cygwin里面vi的问题只是因为配置文件导致的问题，执行以下命令重新放好配置文件即可解决:
```shell
cp /usr/share/vim/{VIM_VERSION}/vimrc_example.vim ~/.vimrc
```
记得将{VIM_VERSION}替换成你自己所对应的版本，例如vim72。

