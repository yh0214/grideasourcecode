---
title: 'Git'
date: 2019-08-27 08:31:42
tags: []
published: true
hideInList: false
feature: 
---
# Git配置
Git安装完成后需要配置个人的用户名称和邮件地址
```
git config --global user.name "yanghang"
git config --global user.email yanghang0214@qq.com
```
查看配置信息
```
git config --list
```
# Git创建仓库
初始化Git仓库
```
git init
```
将文件添加到缓存，例如添加两个文件：
```
git add <file1> <file2> 
```
或者添加所有文件，可以使用
```
git add .
```
查看文件是否添加成功：
```
git status
git status -s
```
将缓存区内容添加到仓库中：
```
git commit -m '本次提交的说明'
```
查看文件修改了哪些内容：
```
git diff readme.txt 
```
查看git提交修改的日志：
```
git log
```
Git版本回退，在Git中用HEAD表示当前版本，上个版本是HEAD\^,上上个版本是HEAD\^^，往上100个写成HEAD\~100：
```
git reset --hard HEAD^
```
要重返未来需要查看命令历史
```
git reflog
```
# Git添加远程仓库
**创建SSH Key**
使用自己的邮件地址，一路回车使用默认值。完成后可以在**用户主目录**里找到.ssh目录，里面有id_rsa和id_rsa.pub两个文件，id_rsa是私钥，id_rsa.pub是公钥。
```
ssh-keygen -t rsa -C "youremail@example.com"
```
**在GitHub添加key**
登陆GitHub，打开“Account settings”，“SSH Keys”页面，点“Add SSH Key”，填上任意Title，在Key文本框里粘贴**id_rsa.pub**文件的内容，点“Add Key”，你就应该看到已经添加的Key。
**关联远程仓库**
远程库的名字就是origin，这是Git默认的叫法，也可以改成别的
```
git remote add origin git@github.com:yh0214/grideasourcecode.git
```
**本地推送至远程库**
首先添加内容到缓存：git add <file1>，然后由缓存添加内容到仓库：git commit -m '本次提交的说明'；使用命令git push -u origin master第一次推送master分支的所有内容；此后，每次本地提交后，可以使用命令git push origin master推送最新修改
```
git push -u origin master
git push origin master
```
**从远程库克隆至本地**
```
git clone git@github.com:yh0214/grideasourcecode.git
```
**删除github上文件**
```
git rm -r --cached 文件夹名称
git commit -m 'delete 文件夹名称 dir'
git push -u origin master
```
























