---
title: Git学习
date: 2019-06-13 13:12:56
tags:
---
## 安装git

[root@localhost ~/testdir]#yum install -y git

## 创建仓库repository
版本库又名仓库，英文名repository，你可以简单理解成一个目录，这个目录里面的所有文件都可以被Git管理起来，每个文件的修改、删除，Git都能跟踪，以便任何时刻都可以追踪历史，或者在将来某个时刻可以“还原”。
先创建一个空目录
[root@localhost ~/testdir]#mkdir testdir

初始化目录，变成仓库
[root@localhost ~/testdir]#git init /root/testdir/

初始化完成后可以看到相应目录下生成.git目录。这个目录是Git来跟踪管理版本库的，没事千万不要手动修改这个目录里面的文件。
[root@localhost ~/testdir]#ls -a
.  ..  .git

## 把工作区文件添加到暂存区
创建一个测试文件
[root@localhost ~/testdir]#vim readme
this is a test file
control by git

查看工作区状态
[root@localhost ~/testdir]#git status
 On branch master

 Initial commit

 Untracked files:
   (use "git add <file>..." to include in what will be committed)

	readme						#未追踪文件
nothing added to commit but untracked files present (use "git add" to track)			  

添加工作区文件到暂存区
[root@localhost ~/testdir]#git add readme

[root@localhost ~/testdir]#git status
 On branch master

 Initial commit

 Changes to be committed:
   (use "git rm --cached <file>..." to unstage)					#可以从暂存区删除文件

	new file:   readme


从暂存区删除文件
[root@localhost ~/testdir]#git rm -f readme					#-f：删除暂存区和工作区的中的文件，彻底删除

[root@localhost ~/testdir]#git rm --cache readme				#--cache：删除暂存区的文件

## 提交文件

[root@localhost ~/testdir]#git commit -m "test file"				#-m后面输入的是本次提交的说明。不能少
[master (root-commit) e936f52] test file
 Committer: root <root@localhost.localdomain>
Your name and email address were configured automatically based
on your username and hostname. Please check that they are accurate.			因为没有自己创建用户和邮箱，git使用了默认配置
You can suppress this message by setting them explicitly:				

    git config --global user.name "Your Name"
    git config --global user.email you@example.com

After doing this, you may fix the identity used for this commit with:

    git commit --amend --reset-author

 1 file changed, 2 insertions(+)
 create mode 100644 readme

创建用户
[root@localhost ~/testdir]#git config --global user.name kej				#创建用户

[root@localhost ~/testdir]#git config --global user.email kej@www.kej.com				#创建邮箱

重新提交
[root@localhost ~/testdir]#git commit --amend --reset-author -m "test file"
[master 45bac50] test file
 1 file changed, 2 insertions(+)				#提示一个文件改动(readme)。插入了两行内容(readme有两行内容)
 create mode 100644 readme

查看提交日志

    [root@localhost ~/testdir]#git log
commit 45bac5002fc85d77e8eceda34781805c0cb09798					
Author: kej <kej@www.kej.com>
Date:   Sun Jun 2 15:35:28 2019 +0800

commit可以一次提交很多文件，所以你可以多次add不同的文件

## 版本回退
现在readme文件已经被追踪。修改readme
[root@localhost ~/testdir]#vim readme 
this is a test file
controled by git
the third line

查看工作区状态
[root@localhost ~/testdir]#git status
 On branch master
 Changes not staged for commit:
   (use "git add <file>..." to update what will be committed)
   (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   readme					#readme文件发生改变

no changes added to commit (use "git add" and/or "git commit -a")

查看工作区该文件与版本库中当前分支上该文件之间的差异
[root@localhost ~/testdir]#git diff readme
diff --git a/readme b/readme
index 1d206bd..11d0dbd 100644
--- a/readme
+++ b/readme
@@ -1,2 +1,3 @@
 this is a test file
 controled by git 
+the third line						#提示新增加了一行

把文件增加到暂存区
[root@localhost ~/testdir]#git add readme

提交
[root@localhost ~/testdir]#git commit -m "add third line" readme
[master 032c62c] add third line
 1 file changed, 1 insertion(+)

查看工作区状态
[root@localhost ~/testdir]#git status
# On branch master
nothing to commit, working directory clean

查看提交日志
[root@localhost ~/testdir]#git log
commit 032c62c487d1764293923d16d9477dbc113c1414				
Author: kej <kej@www.kej.com>
Date:   Sun Jun 2 15:58:33 2019 +0800

    add third line

commit 45bac5002fc85d77e8eceda34781805c0cb09798
Author: kej <kej@www.kej.com>
Date:   Sun Jun 2 15:35:28 2019 +0800

    test file

要回退到上个版本，Git必须知道当前版本是哪个版本，在Git中，用HEAD表示当前版本。
也就是最新提交的commit 032c62c487d1764293923d16d9477dbc113c1414。上一个版本就是HEAD^，
上上一个版本就是HEAD^^，当然往上100个版本写100个^比较容易数不过来，所以写成HEAD~100。

[root@localhost ~/testdir]#git reset --hard HEAD^						#hard|mix|soft三种回退方式；默认mix
HEAD is now at 45bac50 test file

最新版本已经看不到了
[root@localhost ~/testdir]#git log
commit 45bac5002fc85d77e8eceda34781805c0cb09798
Author: kej <kej@www.kej.com>
Date:   Sun Jun 2 15:35:28 2019 +0800

    test file

已经还原到第一个版本
[root@localhost ~/testdir]#cat readme 
this is a test file
controled by git 

此时还可以回到第二个版本，只要上面的命令行窗口还没有被关掉，找到第二个版本的commit id。commit id号
不用写全，一般前6位就行了。
每当你觉得文件修改到一定程度的时候，就可以“保存一个快照”，这个快照在Git中被称为commit。
一旦你把文件改乱了，或者误删了文件，还可以从最近的一个commit恢复，然后继续工作.

[root@localhost ~/testdir]#git reset --hard 032c62
HEAD is now at 032c62c add third line

[root@localhost ~/testdir]#cat readme 
this is a test file
controled by git 
the third line

Git提供了一个命令git reflog用来记录你的每一次命令
[root@localhost ~/testdir]#git reflog
032c62c HEAD@{0}: reset: moving to 032c62
45bac50 HEAD@{1}: reset: moving to HEAD^
032c62c HEAD@{2}: commit: add third line
45bac50 HEAD@{3}: commit (amend): test file
d764af8 HEAD@{4}: commit (amend): test file
c7cf4f9 HEAD@{5}: commit (amend): test file
e936f52 HEAD@{6}: commit (initial): test file

Git跟踪并管理的是修改，而非文件。每次修改完成后都要git add把工作区中被修改的文件放到暂存区，然后在git commit

## 撤销修改

丢弃工作区中的修改
git checkout -- file			#--很重要。没有--表示切换分支

丢弃暂存区中的修改
git reset HEAD <file>，然后git checkout -- file

生成一个新的文件
[root@localhost ~/testdir]#vim test
this is a test file

[root@localhost ~/testdir]#git add test 

[root@localhost ~/testdir]#git commit -m "test file"
[master 5175295] test file
 1 file changed, 1 insertion(+)
 create mode 100644 test

删除工作区中的test
[root@localhost ~/testdir]#rm -rf test 

这是工作区与版本库中文件不一样
[root@localhost ~/testdir]#git status
 On branch master
 Changes not staged for commit:
   (use "git add/rm <file>..." to update what will be committed)
   (use "git checkout -- <file>..." to discard changes in working directory)

	deleted:    test

no changes added to commit (use "git add" and/or "git commit -a")

现在有两个选择
确实要从版本库中删除文件
[root@localhost ~/testdir]#git rm test
rm 'test'

[root@localhost ~/testdir]#git commit -m "remove test file"
[master 0e53a68] remove test file
 1 file changed, 1 deletion(-)
 delete mode 100644 test

误删除了工作区中的文件，要从版本库中恢复
[root@localhost ~/testdir]#git checkout -- test				#git checkout其实是用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以“一键还原”。

## 添加远程库

要关联一个远程库，使用命令git remote add origin git@server-name:path/repo-name.git；
[root@localhost ~/testdir]#git remote add origin git@github.com:kejlinux/learngit.git					#origin：仓库名字

关联后，使用命令git push -u origin master第一次推送master分支的所有内容；

此后，每次本地提交后，只要有必要，就可以使用命令git push origin master推送最新修改；


## 从远程克隆到本地
要克隆一个仓库，首先必须知道仓库的地址，然后使用git clone命令克隆。

Git支持多种协议，包括https，但通过ssh支持的原生git协议速度最快。

## 分支管理

创建一个分支，并切换到分支
[root@localhost ~/testdir]#git checkout -b dev		#checkout -b表示创建分支并切换到分支
Switched to a new branch 'slave'

相当于
[root@localhost ~/testdir]#git branch dev			#创建新分支

[root@localhost ~/testdir]#git checkout dev			#切换分支

查看当前在哪个分支上
[root@localhost ~/testdir]#git branch
* dev					#*表示当前分支
  master
  slave

修改dev分支上的文件
[root@localhost ~/testdir]#vim test 
this is a test file
this is second line

放入暂存区然后提交
[root@localhost ~/testdir]#git add test 
[root@localhost ~/testdir]#git commit -m "branch test"
[dev ec41110] branch test
 1 file changed, 1 insertion(+)

切换到master分区上查看文件
[root@localhost ~/testdir]#git checkout master
Switched to branch 'master'

发现刚才添加的内容不见了。这是因为添加的内容在dev分支上
[root@localhost ~/testdir]#cat test 
this is a test file

把dev分支合并到master分支上
[root@localhost ~/testdir]#git merge dev
Updating 5175295..ec41110
Fast-forward				#这次合并是“快进模式”，也就是直接把master指向dev的当前提交。
 test | 1 +
 1 file changed, 1 insertion(+)

查看master分支上的test文件，发现内容和dev分支上的test一样
[root@localhost ~/testdir]#cat test 
this is a test file
this is second line

合并完成后可以删除dev分支
[root@localhost ~/testdir]#git branch -d dev
Deleted branch dev (was ec41110).

[root@localhost ~/testdir]#git branch
* master
  slave


## 解决合并冲突

切换到slave分支上
[root@localhost ~/testdir]#git checkout slave
Switched to branch 'slave'

[root@localhost ~/testdir]#vim test 
this is a test file
branch slave test

[root@localhost ~/testdir]#git add test 
[root@localhost ~/testdir]#git commit -m "branch slave test" test 

切换到master分支
[root@localhost ~/testdir]#git checkout master
Switched to branch 'master'
Your branch is ahead of 'origin/master' by 1 commit.				#这是因为有远程仓库。目前仓库和远程仓库内容不相同。
  (use "git push" to publish your local commits)

[root@localhost ~/testdir]#vim test 
this is a test file
this is second line
this is third line

[root@localhost ~/testdir]#git add test 
[root@localhost ~/testdir]#git commit -m "third line on master" test 

合并分支
[root@localhost ~/testdir]#git merge slave
Auto-merging test
CONFLICT (content): Merge conflict in test
Automatic merge failed; fix conflicts and then commit the result.				#发现两个分支有冲突，需要解决冲突

现在查看test文件，发现git把需要更改的地方标出来了
[root@localhost ~/testdir]#cat test 
this is a test file
<<<<<<< HEAD
this is second line
this is third line

=======
branch slave test
>>>>>>> slave

修改test文件，然后提交
[root@localhost ~/testdir]#git commit -m "conflict fixed"
[master c4d798e] conflict fixed
提交完成后不需要合并了。因为修改文件的操作相当于把slave分支上的内容整合到master分支上了

如果尝试合并
[root@localhost ~/testdir]#git merge slave
Already up-to-date.				#提示已经更新过数据了

此时可以删除分支了

## git stash

当正在dev分支上进行工作时，需要临时处理另一个分支slave的工作。这时dev分支上能看到dev分支上未完成的工作
[root@localhost ~/testdir]#git branch
* dev
  master
  slave

[root@localhost ~/testdir]#vim test 
this is a test file
this is second line
this is third line
branch slave test
branch on dev
branch on dev
stash test

[root@localhost ~/testdir]#git add test				#无论是否放在暂存区，在别的分区上都可以看到修改后的内容

[root@localhost ~/testdir]#git status
 On branch dev
 Changes to be committed:
   (use "git reset HEAD <file>..." to unstage)

	modified:   test


[root@localhost ~/testdir]#git checkout slave
M	test
Switched to branch 'slave'

[root@localhost ~/testdir]#git status
 On branch slave
 Changes to be committed:
   (use "git reset HEAD <file>..." to unstage)

	modified:   test


可以把当前分支上的工作保存起来。这样在别的分支上就看不到了
[root@localhost ~/testdir]#git branch
  dev
  master
* slave

[root@localhost ~/testdir]#vim test 
this is a test file
this is second line
this is third line
branch slave test
branch on dev
branch on dev
stash on slave

[root@localhost ~/testdir]#git stash
Saved working directory and index state WIP on slave: 98c9973 second dev
HEAD is now at 98c9973 second dev

查看保存的内容
[root@localhost ~/testdir]#git stash list
stash@{0}: WIP on slave: 98c9973 second dev

切换到别分支上，并不能看到slave分支上的改动
[root@localhost ~/testdir]#git checkout master
Switched to branch 'master'

[root@localhost ~/testdir]#git status
 On branch master
 Your branch is ahead of 'origin/master' by 3 commits.
   (use "git push" to publish your local commits)

nothing to commit, working directory clean

恢复保存的内容
[root@localhost ~/testdir]#git stash apply					#这样恢复不会删除保存的内容
 On branch slave
 Changes not staged for commit:
   (use "git add <file>..." to update what will be committed)
   (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   test

no changes added to commit (use "git add" and/or "git commit -a")

[root@localhost ~/testdir]#git stash list
stash@{0}: WIP on slave: 98c9973 second dev					#保存的内容还在

需要手动删除stash保存的内容
[root@localhost ~/testdir]#git stash drop stash@{0}
Dropped stash@{0} (834ad4d84d47c027e8ccd5c0729f0bac24df4900)

可以在恢复的同时把stash内容删除
[root@localhost ~/testdir]#git stash pop

可以多次stash。选择性恢复
[root@localhost ~/testdir]#git stash apply stash@{0}


## 多人协同

首先，可以试图用git push origin <branch-name>推送自己的修改；

如果推送失败，则因为远程分支比你的本地更新，需要先用git pull试图合并；

如果合并有冲突，则解决冲突，并在本地提交；

没有冲突或者解决掉冲突后，再用git push origin <branch-name>推送就能成功！

如果git pull提示no tracking information，则说明本地分支和远程分支的链接关系没有创建，用命令git branch --set-upstream-to <branch-name> origin/<branch-name>。

从远程克隆分支
git clone -b 分支 仓库路径
[root@localhost ~/kej/kej]#git clone -b slave  git@github.com:kejlinux/kej.git

--------------------- 
