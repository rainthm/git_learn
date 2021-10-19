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
