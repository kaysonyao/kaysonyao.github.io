---
title: 使用仓库分支管理Hexo网站和代码
tags: [Hexo,GitHub]
categories: Hexo
comments: true
---
搭建完Hexo后，一直在同一台PC上更新，想到如果换了电脑就不好继续了。最初的做法是建立新的仓库，将代码放到新仓库，每次修改后hexo d 部署到就仓库，然后push代码到新仓库，虽然不用修改配置，但总觉得GitHub上建了2个Repositories不是很爽，所以使用了同一个repositorie的不同分支来部署Hexo和代码。
<!--more-->
## 前言
由于hexo在本地已经安装并且网站已部署到GitHub，而且对git不是很熟，我选择保留本地代码删除重建GitHub上repository
## hexo代码分支操作
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
### 将远程分支文件拉下来（避免冲突）
```bash
git pull origin master
```
### 创建分支
创建本地hexo分支
```bash
git branch hexo
```
### 切换至hexo分支
```bash
git checkout hexo
```
### 将本地资源同步推到GitHub的Hexo分支（自己创建）
```bash
git push origin hexo
```
**至此hexo代码已经上传至远程仓库的hexo分支**
## hexo发布
hexo发布和之前没有区别，因为没有切换环境，所以不需要重新安装nodejs、hexo等
仍然可使用 hexo g -d  来部署
**注意** _config.yml 文件依旧需要保持原地址和master分支
```bash
  repository: https://github.com/kaysonyao/kaysonyao.github.io.git
  branch: master
```
## 修改hexo代码后提交
依次执行下面语句：
```bash
git add .
```
```bash
git commit -m "..."
```
```
git push origin hexo
```
## 更换电脑后同步管理
**前提：**需要在GitHub上将hexo分支作为Default分支
**参考资料：**[http://blog.yaock.com/2016/10/09/%E4%BD%BF%E7%94%A8%E5%A4%9A%E5%8F%B0%E7%94%B5%E8%84%91%E7%BB%B4%E6%8A%A4GitHub%E4%BB%A3%E7%A0%81/](http://blog.yaock.com/2016/10/09/%E4%BD%BF%E7%94%A8%E5%A4%9A%E5%8F%B0%E7%94%B5%E8%84%91%E7%BB%B4%E6%8A%A4GitHub%E4%BB%A3%E7%A0%81/ "使用多台电脑维护GitHub代码")
具体操作步骤如下：
1. 在电脑2上完成git的安装和配置
2. 在电脑2上创建SSH Key
3. 在GitHub上添加新建的SSH Key
4. 将远程库克隆到本地电脑2上（默认分支为hexo）
5. 在本地新拷贝的kaysonyao.github.io目录下通过Git bash依次执行下列指令：
```bash
npm install hexo
```
```bash
npm install
```
```bash
npm install hexo-deployer-git
```
**注：** *不需要hexo init这条指令
## 日常修改操作
在本地对博客进行修改后，通过下面的步骤进行管理：
0. 将最新代码同步至本地,执行：
```bash
git pull origin hexo 
```
1. 依次执行下面指令，将改动推送到GitHub（此时当前分支应为hexo）
```bash
git add .
```
```bash
git commit -m "注释语句"
```
```bash
git push origin hexo
```
2. 发布hexo网站到master分支上，执行：
```bash
hexo g -d
```
虽然1、2个过程顺序调转一般不会有问题，不过逻辑上这样的顺序是绝对没问题的
（例如突然死机要重装了，悲催….的情况，调转顺序就有问题了）。
