---
title: 使用多台电脑维护GitHub代码
tags: [Git,GitHub]
categories: Git
comments: true
---
在实际工作生活中，我们可能不一定仅仅在一台电脑上编码，比如：我们平时在单位电脑1上写代码，提交代码到github账户，而我们也可能会在在家里的电脑2上继续工作，提交代码，这样就是在不同的电脑上提交代码到同一个github账户，同时在每一台电脑上都保持和github账户的一致，该怎么办呢？
<!--more-->
### Step1:首先在电脑2上完成git的安装和配置
具体安装配置与电脑1上的一样，其中用户名和邮箱可以使用电脑1的用户名和邮箱，也可以设置为其他用户名和邮箱。配置邮箱操作如下：
1. 装完成后，开发“Git Bash”，弹出一个git命令行窗口
2. 在弹出的git命令行窗口输入：
```bash
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
```
![gitconfig](/img/gitconfig.jpg)
### Step2:在电脑2上创建SSH Key
1. 打开Shell（Windows下打开Git Bash），输入
```bash
ssh-keygen -t rsa -C "youremail@example.com"
```

2. 然后一路回车，无需设置密码。
3. 然后在用户主目录里找到.ssh目录，里面有id_rsa和id_rsa.pub两个文件，id_rsa是私钥，不能泄露，id_rsa.pub是公钥，可以放心告诉别人.
4. 登陆Github，进入settings,点击SSH Keys.
5. 点击New SSH Key,填写任意Title，在Key文本框粘贴电脑2的id_rsa.pub文件的内容,然后点add Key。(*由于电脑1的SSH Key已经上传，所以可以看到已经有一个SSH Key了，这个SSH key是电脑1的，为了创建电脑2的SSH Key*）
### Step3:将远程库克隆到本地电脑2上
1. 进入项目目录，git bash进入命令行模式
2. 输入：
```bash
git clone git@github.com:kaysonyao/test.git
```

3. 进入该目录，可以看到test文件夹，远程的代码已经被克隆到本地电脑2上了。
这样就可在在电脑2上对代码进行修改、提交等操作了，每次git push将本地修改提交到远程后，远程代码就发生了改变。
### Step4：当在电脑1上工作时，本地代码和远程的代码发生了不一致，为了保持同步，所以需要将远程的代码同步到本地电脑1上
1. 从远程的origin的master主分支下载最新的版本到origin/master分支上
```bash
git fetch origin master
```

2. 然后比较本地的master分支和origin/master分支的差别
```bash
git log -p master..origin/master
```

3. 最后进行合并
```bash
git merge origin/master
```