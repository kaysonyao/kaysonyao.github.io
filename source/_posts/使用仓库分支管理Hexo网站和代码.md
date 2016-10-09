---
title: 使用仓库分支管理Hexo网站和代码
tags: [Hexo,GitHub]
categories: Hexo
comments: true
---
搭建完Hexo后，一直在同一台PC上更新，想到如果换了电脑就不好继续了。最初的做法是建立新的仓库，将代码放到新仓库，每次修改后hexo d 部署到就仓库，然后push代码到新仓库，虽然不用修改配置，但总觉得GitHub上建了2个Repositories不是很爽，所以使用了同一个repositorie的不同分支来部署Hexo和代码。
<!--more-->
##前言
由于hexo在本地已经安装并且网站已部署到GitHub，而且对git不是很熟，我选择保留本地代码删除重建GitHub上repository
### 新建repository
因为我是删除了原本的repository重头开始，所以这边需要新建一个新的，repository名称部署成功过的都知道，如果不是用二级域名访问，就需要yourname.github.io的形式：
![createnew](/img/createnew.jpg)
*建议勾上Readme.md，这样默认就创建了master分支*
### 本地仓库操作
1. 打开gitbash，进入hexo目录
2. 建立git仓库
```bash
git init
```
3. 将项目的所有文件添加到仓库中
```bash
git add .
```
如果想添加某个特定的文件，只需把.换成特定的文件名即可
4. 将add的文件commit到仓库
```bash
git commit -m "注释语句"
```
### 将本地的仓库关联到github上
```bash
git remote add origin git@github.com:kaysonyao/kaysonyao.github.io.git
```
### 创建分支并同步
1. 创建本地hexo分支
```bash
git branch hexo
```
2. 将推到远程分支
```bash
git bran
```