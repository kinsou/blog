title: hexo+coding 搭建博客
tags:
  - Git
  - Hexo
categories:
  - Hexo
date: 2015-12-17 23:59:00
---
### 1、安装Git
[http://git-for-windows.github.io/](http://git-for-windows.github.io/ "官网")
[https://github.com/git-for-windows/git/releases/download/v2.6.4.windows.1/Git-2.6.4-64-bit.exe](https://github.com/git-for-windows/git/releases/download/v2.6.4.windows.1/Git-2.6.4-64-bit.exe "Git-2.6.4-64-bit 下载")
### 2、安装Node.js
[https://nodejs.org/en/](https://nodejs.org/en/ "官网")
[https://nodejs.org/dist/v5.3.0/node-v5.3.0-x64.msi](https://nodejs.org/dist/v5.3.0/node-v5.3.0-x64.msi "下载")
### 3、安装Hexo框架
```shell
npm install -g hexo
```
### 4、安装Hexo插件
```shell
npm install hexo-generator-sitemap --save
npm install hexo-generator-feed --save
npm install hexo-deployer-git --save
```
### 5、创建个人博客
创建目录，右击后选择git bash，输入：
```shell
hexo init
```
### 6、运行服务器测试
```shell
hexo generate
hexo server
```
本地地址：[http://localhost:4000/](http://localhost:4000/ "http://localhost:4000/")

### 7、编辑_config.yml文件增加
```shell
deploy:
   type: git
   repo: git@git.coding.net:kinsou/blog.git
   message: update
   branch: coding-pages
```
### 8、上传Git
```shell
hexo d -g
```
其他命令：
```shell
hexo n #写文章
hexo g #生成
hexo d #部署 # 可与hexo g合并为 
```