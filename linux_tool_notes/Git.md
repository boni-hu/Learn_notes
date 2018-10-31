1.git clone 后的文件权限问题：需要重新添加仓库吗

2.git 管理自己的代码？

3.代码更新问题？

### git 版本操作状态查询

#### git 的一些状态查询：

```git
git diff : difference 查看具体内容修改和不同

git status： 查看仓库状态

git log：记录提交历史记录，每一次commit时候的注释就显得有用了起来（版本库的状态）

git  log --pretty==oneline

git relog :用来记录每一次的命令

git diff HEAD -- readme.txt ：查看工作区和版本库里最新版本的区别

git remote:查看远程库的信息状态（git remote -v）
```

#### 版本回退：

```
git reset --hard HEAD^ ：回退到上一版本

git reset --hard HEAD^^ :回退到上上版本

git reset --hard HEAD～100 :退回到往上100个版本

git reset --hard 1094ad(版本号，没必要写全)：会退到指定版本

reset命令都是已经提交到暂存区想进行修改，执行了add ，commit

git checkout -- file ：可以丢弃工作区的修改（还没有add，commit 修改还没在暂存区，只是在工作区）

git rm 用于删除一个文件
```

### 远程仓库

本地到远程：

```
git remote add origin git@github.com:user/learngit.git ：把本地仓库的内容关联到远程仓库

git push -u origin master（第一次推送加上了-u参数）
```

远程到本地：

```
git clone url
```

### 分支管理

```
查看分支：git branch

创建分支：git branch <name>

切换分支：git checkout <name>

创建+切换分支：git checkout -b <name>

合并某分支到当前分支：git merge <name>

删除分支：git branch -d <name>

```

##### bug 分支：`git stash 一下`

一，保存工作现场 ：git stash

二，创建修改bug的临时分支：git checkout -b issue-101

三，修改完成后回到当前分支，并完成合并：

git checkout master

git merge  --no-ff -m "merged bug fix 101" issue-101

四，回到dev分支继续

git checkout dev

(工作区是干净的)

git  stash list

恢复：git stash apply

删除stash内容：git stash drop

恢复+删除：git stash pop

 `开发新的功能最好创建一个新的分支`

#### 多人协作

```
1.首先，可以试图用git push origin <branch-name>推送自己的修改；

2.如果推送失败，则因为远程分支比你的本地更新，需要先用git pull试图合并；

3.如果合并有冲突，则解决冲突，并在本地提交；

4.没有冲突或者解决掉冲突后，再用git push origin <branch-name>推送就能成功！

5.如果git pull提示no tracking information，则说明本地分支和远程分支的链接关系没有创建，用命令git branch --set-upstream-to <branch-name> origin/<branch-name>。
```

### 标签

git tag v1.0 添加标签

git tag 查看所有标签

git show 查看标签信息

git tag -d v1.0 删除标签


## some tips
1. 报错1：使用 ssh keys时按照git的教程generate了ssh但是clone的时候仍然报错可以输入
```
eval "$(ssh-agent -s)"
ssh -add
```
关于ssh-keys难以解决的问题，一般直接删除重新添加新的sshkeys
2. 报错2：
```
git push origin master
To git@github.com:boni-hu/SummerCamp2018Homework.git
 ! [rejected]        master -> master (fetch first)
error: failed to push some refs to 'git@github.com:boni-hu/SummerCamp2018Homework.git'
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for 
details.
```
解决：该命令用于合并本地和远程仓库的内容，可能是本地删除了某些东西造成了出错
```
git pull --rebase origin master

```

