---
title: 使用Git上传代码至GitHub
tags: [Git,GitHub]
categories: Git
comments: true
---
将新建的代码上传至github
<!--more-->
### 第一步：建立git仓库
cd到你的本地项目根目录下，执行git命令

```bash
git init
```
### 第二步：将项目的所有文件添加到仓库中
```bash
git add .
```
如果想添加某个特定的文件，只需把.换成特定的文件名即可
### 第三步：将add的文件commit到仓库
```bash
git commit -m "注释语句"
```
### 第四步：去github上创建自己的Repository，创建页面如下图所示： 
![create_repository](/img/create_repository.jpg)

点击下面的Create repository，就会进入到类似下面的一个页面,如下图所示：

![test1_repository](/img/test1_repository.jpg)

点击右侧Clone or download 按钮，下面红色框里的地址就是创建的仓库的地址
### 第五步：将本地的仓库关联到github上
```bash
git remote add origin git@github.com:kaysonyao/test1.git
```
origin后面的链接地址换成你自己的仓库url地址，也就是上面红框中标出来的地址
### 第六步：上传github之前，要先pull一下，执行如下命令：
```bash
git pull origin master
```
敲回车后，会执行输出类似如下页面 

![gitpull](/img/gitpull.jpg)
### 第七步：上传代码到github远程仓库
```bash
git push -u origin master
```
执行完后，如果没有异常，等待执行完就上传成功了，中间可能会让你输入Username和Password，你只要输入github的账号和密码就行了

![gitpush](/img/gitpush.jpg)
![uploadcode](/img/uploadcode.jpg)