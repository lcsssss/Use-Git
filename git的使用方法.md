# git的使用
## 安装git
- git官网：[https://gitforwindows.org/](https://gitforwindows.org/)
## 创建代码仓库
- 配置身份
```git
git config --global uer.name "lcs"
git config --global uer.email "1410613169@qq.com"
```
- 查看是否配置成功
```git
git config --global uer.name 
git config --global uer.email
```
- 在项目的根目录下右键点击Git Bash Here
```git
git init
```
- 查看目录
```git
ls -al
```
## 添加 & 提交文件
- 添加build.gradle文件
```git
git add build.gradle  
```
- 添加app目录下的所有文件
```git
git add app
# git add .
```
- 提交
```git
git commit -m "First commit"
```
##　忽略文件
.gitignore记录排除在版本控制之外的文件，Android会自动创建：一个在根目录，一个在app模块下
##　查看修改内容
- 查看哪一个文件被修改了
```git
git status
```
- 查看更改内容
```git
git diff #可以加上路径
```
> \+
> +first change
> +seconde change  

加号表示增加内容，减号表示删除内容
## 撤销未提交的修改
- 只要代码还未提交，所修改的内容都可以撤销，只适用于没有执行add命令的文件
```git
git checkout Test.cpp
```
- 执行add命令的文件后的，取消添加
```git 
git reset HEAD Test.cpp
```
### 查看提交记录
```git
git log
```
结果：
```
Author: lcs <1410613169@qq.com>
Date:   Wed May 26 18:34:38 2021 +0800

    First commit
```
查看最后一次提交
```git
git log -1
```
### 分支的用法
多版本发布时使用
- 查看当前版本库中有哪些分支
```git
git branch 
```
- 创建分支
```git
git branch version1.0
```
```
$ git branch
* master
  version1.0
```
\*说明代码还在master分支上  
- 切换到version1.0分支
```git 
git checkout version1.0
```
结果：
> $ git branch
>  master
> \* version1.0
- 合并分支
```git
git checkout master
git merge version1.0
```
结果：
> $ git merge version1.0
> Already up to date.
## 与远程版本库协作
比如有一个远程版本库的Git地址是：[https://github.com/h-Tony/Use-Git.git](https://github.com/h-Tony/Use-Git.git)，可以使用如下命令将代码下载到本地：
```git
git clone https://github.com/h-Tony/Use-Git.git
``` 
- 同步到远程版本库上
```git 
git push origin master
```
> origin部分指定的是远程版本库的Git地址，master指定的是同步到哪一个分支，上述代码将本地代码同步到远程版本库地址。
- 将远程版本库的上的代码同步到本地
```git 
git fetch origin master
```
- 接下来的代码会存放到origin/master分支上，可以通过
```git 
git diff origin/master
```
查看远版本库修改的内容
- 合并origin/master到主分支上
```git
git merge origin/master
```
- pull相当于fetch命令和merge命令一直执行
##　将代码托管到Github上
- 打开终端界面切换到某一工程目录下，输入
```git
git clone https://github.com/h-Tony/Use-Git.git
```
将Use目录中的文件全部复制到上一层目录中

---
## 可能会遇到的问题
>The authenticity of host 'github.com (52.74.223.119)' can't be established.
RSA key fingerprint is SHA256:nThbg6kXUpJWGl7E1IGOCspRomTxdCARLviKw6E5SY8.
This key is not known by any other names
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added 'github.com' (RSA) to the list of known hosts.
git@github.com: Permission denied (publickey).
fatal: Could not read from remote repository.

Permission denied (publickey) 没有权限的publickey ，出现这错误一般是- 以下两种原因
> 客户端与服务端未生成 ssh key
> 客户端与服务端的ssh key不匹配
- 客户端生成ssh key
1. 在cmd里面输入
> ssh-keygen -t rsa -C "xxxxxxxx@qq.com"
ssh-keygen -t rsa -C "youremail@example.com"

xxxxxx@qq.com改为自己的邮箱即可，途中会让你输入密码啥的，不需要管，一路回车即可，会生成你的ssh key。（如果重新生成的话会覆盖之前的ssh key。）
2. 打开id_rsa.pub文件,并且复制内容
3. 在github上打开箭头处,点击Setting
4. 点击SSH and GPG keys
5. 打开你刚刚生成的id_rsa.pub，将里面的内容复制，进入你的github账号，在settings下，SSH and GPG keys下new SSH key，然后将id_rsa.pub里的内容复制到Key中，完成后Add SSH Key.
6. 用idea再次提交文件到 github上,显示提交成功