# Learn how to use git under the instruction of Micheal Liao

## 1 Step.
初始化一个Git仓库，使用git init命令。

添加文件到Git仓库，分两步：

使用命令git add <file>，注意，可反复多次使用，添加多个文件；
使用命令git commit -m <message>，完成。

***
we should create a id in the github website.
***
# 3 时光机任意穿梭
## -->版本回退
HEAD指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令***git reset --hard commit_id***。

穿梭前，用***git log***可以查看提交历史，以便确定要回退到哪个版本。

要重返未来，用***git reflog***查看命令历史，以便确定要回到未来的哪个版本。

## -->工作区和缓存区
工作区Working area
is the directory we can see 

版本库Repository
就是工作区中的隐藏文件夹.git

在工作区增加一个lincense.txt文件
输入git status查看状态
```
ryan@ryan-VirtualBox:~/git/gitlearn$ git status
位于分支 master
尚未暂存以备提交的变更：
  （使用 "git add <文件>..." 更新要提交的内容）
  （使用 "git restore <文件>..." 丢弃工作区的改动）
        修改：     git_learn.md
        修改：     readme.txt

未跟踪的文件:
  （使用 "git add <文件>..." 以包含要提交的内容）
        license.txt
```
两次使用命令git add，增加readme.txt 和 license.txt后。
![](../gitlearn/pic/0.jpeg)

git add命令实际上就是把要提交的所有修改放到暂存区（Stage），然后，执行git commit就可以一次性把暂存区的所有修改提交到分支。

```
ryan@ryan-VirtualBox:~/git/gitlearn$ git add readme.txt
ryan@ryan-VirtualBox:~/git/gitlearn$ git add license.txt 
ryan@ryan-VirtualBox:~/git/gitlearn$ git status
位于分支 master
要提交的变更：
  （使用 "git restore --staged <文件>..." 以取消暂存）
        新文件：   license.txt
        修改：     readme.txt

尚未暂存以备提交的变更：
  （使用 "git add <文件>..." 更新要提交的内容）
  （使用 "git restore <文件>..." 丢弃工作区的改动）
        修改：     git_learn.md

未跟踪的文件:
  （使用 "git add <文件>..." 以包含要提交的内容）
        pic/
```

而使用git commit命令后就是将暂存区的修改提交到分支
如：
```
git commit -m "understand how stage works"
```
如果提交完后没有其他更改，则暂存区就干净了
![](pic/1.jpeg)
## 管理修改
每次修改，如果不用git add到暂存区，那就不会加入到commit中

## 撤销修改
分几种情况
### 1,文件只是保存
比如编辑了readme.txt并保存。
用git status查看有修改。
用git restore 可以恢复到编辑前的状态。
```
ryan@ryan-VirtualBox:~/git/gitlearn$ git status
位于分支 master
尚未暂存以备提交的变更：
  （使用 "git add <文件>..." 更新要提交的内容）
  （使用 "git restore <文件>..." 丢弃工作区的改动）
        修改：     git_learn.md
        修改：     readme.txt
修改尚未加入提交（使用 "git add" 和/或 "git commit -a"）
```
```
ryan@ryan-VirtualBox:~/git/gitlearn$ git restore readme.txt
ryan@ryan-VirtualBox:~/git/gitlearn$ git status
位于分支 master
尚未暂存以备提交的变更：
  （使用 "git add <文件>..." 更新要提交的内容）
  （使用 "git restore <文件>..." 丢弃工作区的改动）
        修改：     git_learn.md

修改尚未加入提交（使用 "git add" 和/或 "git commit -a"）
```
### 2，放弃已经使用git add，即在暂存区的
```
ryan@ryan-VirtualBox:~/git/gitlearn$ git status
位于分支 master
要提交的变更：
  （使用 "git restore --staged <文件>..." 以取消暂存）
        修改：     readme.txt
```
相当于把文件放回到工作区
再git restore <file>就可以了
### 3,放弃已经commit的
需要使用前面的方法
git reset --hard <id>

## 删除文件
命令git rm用于删除一个文件。如果一个文件已经被提交到版本库，那么你永远不用担心误删，但是要小心，你只能恢复文件到最新版本，你会丢失最近一次提交后你修改的内容。

# 远程仓库
已经建好github账户
在不同的电脑上都需要有不同的公钥
1、检查/home/ryan/.ssh/目录中是否有id_rsa和id_rsa.pub这两个文件。如果没有。则运行
```
ryan@ryan-VirtualBox:~/.ssh$ ssh-keygen -t rsa -C "rainthm@139.com"
```
如果一切顺利的话，可以在用户主目录里找到.ssh目录，里面有id_rsa和id_rsa.pub两个文件，这两个就是SSH Key的秘钥对，id_rsa是私钥，不能泄露出去，id_rsa.pub是公钥，可以放心地告诉任何人。

（2）登录GitHub，打开“Account settings”，“SSH Keys”页面：

然后，点“Add SSH Key”，填上任意Title，在Key文本框里粘贴id_rsa.pub文件的内容：

## 建立远程仓库
在web上操作

## 将本地添加到远程库
```
ryan@ryan-VirtualBox:~/git/gitlearn$ git push -u origin main
枚举对象中: 37, 完成.
对象计数中: 100% (37/37), 完成.
压缩对象中: 100% (32/32), 完成.
写入对象中: 100% (37/37), 27.23 KiB | 3.89 MiB/s, 完成.
总共 37（差异 11），复用 0（差异 0），包复用 0
remote: Resolving deltas: 100% (11/11), done.
To github.com:rainthm/git_learn
 * [new branch]      main -> main
分支 'main' 设置为跟踪来自 'origin' 的远程分支 'main'。
```
开始没有添加公钥，出现了的错误 
```
ryan@ryan-VirtualBox:~/git/gitlearn$ git push -u origin main
git@github.com: Permission denied (publickey).
fatal: 无法读取远程仓库。

请确认您有正确的访问权限并且仓库存在。
```
## 删除远程库
删除远程库，可以用git remote rm <name>命令。使用前，建议先用git remote -v查看远程库信息：

删除其实是解绑。
后面再关联上就可以了

---
要关联一个远程库，使用命令git remote add origin git@server-name:path/repo-name.git；

关联一个远程库时必须给远程库指定一个名字，origin是默认习惯命名；

关联后，使用命令git push -u origin main第一次推送main分支的所有内容；

此后，每次本地提交后，只要有必要，就可以使用命令git push o推送最新修改；

---

