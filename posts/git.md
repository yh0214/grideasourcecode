---
title: 'Git'
date: 2019-08-27 08:31:42
tags: []
published: true
hideInList: false
feature: 
---
**Git配置**
Git安装完成后需要配置个人的用户名称和邮件地址
```
git config --global user.name "yanghang"
git config --global user.email yanghang0214@qq.com
```
查看配置信息
```
git config --list
```
**Git工作区、暂存区和版本库**
* 工作区：就是你在电脑里能看到的目录。
* 暂存区：英文叫stage, 或index。一般存放在 ".git目录下" 下的index文件（.git/index）中，所以我们把暂存区有时也叫作索引（index）。
* 版本库：工作区有一个隐藏目录.git，这个不算工作区，而是Git的版本库。
**Git创建仓库**
初始化Git仓库
```
git init
```
使用git clone从现有Git仓库中拷贝项目（类似svn checkout）
克隆仓库的命名格式为：
```
git clone <repo>
```
如果需要克隆到指定目录，可以使用：
```
git clone <repo> <directory>
```
将文件添加到缓存，例如添加两个文件：
```
git add README hello.php 
```
新项目中添加所有文件很普遍，可以使用git add .
查看文件是否添加成功：
```
git status
git status -s
```
将缓存区内容添加到仓库中：
```
git commit -m '第一次版本提交'
```
查看文件修改了哪些内容：
```
git diff readme.txt 
```
查看git提交修改的日志：
```
git log
```
Git版本回退，在Git中用HEAD表示当前版本，上个版本是HEAD^,上上个版本是HEAD^^，往上100个写成HEAD~100：
```
git reset --hard HEAD^
```
要重返未来需要用git reflog查看命令历史
Git添加远程仓库
第一步：创建SSH Key，使用自己的邮件地址，一路回车使用默认值。
```
ssh-keygen -t rsa -C "youremail@example.com"
```
如果一切顺利的话，可以在**用户主目录**里找到.ssh目录，里面有id_rsa和id_rsa.pub两个文件，这两个就是SSH Key的秘钥对，id_rsa是私钥，不能泄露出去，id_rsa.pub是公钥，可以放心地告诉任何人。
第二步：登陆GitHub，打开“Account settings”，“SSH Keys”页面：然后，点“Add SSH Key”，填上任意Title，在Key文本框里粘贴id_rsa.pub文件的内容，点“Add Key”，你就应该看到已经添加的Key。
关联远程仓库：
```
git remote add origin git@github.com:yh0214/gridea.source.code.git
```
远程库的名字就是origin，这是Git默认的叫法，也可以改成别的























