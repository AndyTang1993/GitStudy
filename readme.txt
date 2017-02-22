Git命令：
 1、创建版本库
 $ mkdir learngit
 $ cd learngit
 $ pwd（用于显示当前库目录）
 git init（把这个目录变成Git可以管理的仓库）
 ls -ah（查看隐藏文件）

2、Git库中的文件修改与上传
git add（加入暂存区）
git commit xxx -m "注释"（上传到库中）
git status（随时掌握工作区的状态：是否有变化）
git diff（查看具体修改了什么内容）

3、回退版本
注：Git必须知道当前版本是哪个版本，在Git中，用HEAD表示当前版本，也就是最新的提交，上一个版本就是HEAD^，上上一个版本就是HEAD^^，当然往上100个版本写100个^比较容易数不过来，所以写成HEAD~100

git log（查看提交历史）
git reset --hard HEAD^ 或 版本号（回退到上个版本，有几个^就回退几个版本）
git reflog（用来查看每一次命令，找版本的HEAD时会用到）
cat 文件名（显示指向版本的内容）

4、撤销修改
git checkout -- file（丢弃工作区的修改）

注：git checkout -- file命令中的--很重要，没有--，就变成了“切换到另一个分支”的命令

5、删除
git rm（删除，之后再commit）
误删可以通过git checkout -- file撤销

6、远程仓库
ssh-keygen -t rsa -C "youremail@example.com"（创建SSH KEY）
GitHup网站建远程库
git remote add origin SSH地址（通过SSH关联本地与远程库）
git push -u origin master（第一次推送master分支的所有内容）
git push origin master（把本地master分支的最新修改推送至GitHup）

git clone SSH地址（本地文件夹下，clone GitHup远程库中的项目）

7、分支管理
$ git branch xxx （创建分支）
$ git checkout xxx（切换到分支）
简写：git checkout -b xxx（创建并切换）

git branch（查看当前分支,带*）
git merge（用于合并指定分支到当前分支。）
注：Fast-forward快进模式
git branch -d xxx（删除分支）

注：分支同时有内容修改会冲突。
git status能查看冲突，先手动解决冲突，再提交
git log --graph 或git log --graph --pretty=oneline --abbrev-commit（看到分支合并图）

git merge --no-ff -m "注释" xxx
注：合并分支时，加上--no-ff参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而fast forward合并就看不出来曾经做过合并。

8、bug分支和Feature分支（新功能分支）
情景：正在分支上开发，需要紧急解决一个bug，在主分支或开发分支上创建新的bug分支。
git stash（当前开发的进度保留，并隐藏）
git stash list（查看之前被隐藏的工作区）

git stash apply恢复，stash内容并不删除，用git stash drop来删除；
git stash pop，恢复的同时把stash内容也删了：
git stash apply stash@{0}（多次stash，用编号选择恢复）

9、多人协作
git remote -v（查看远程库的信息：显示推送和提取权限）
模式：
1、首先，可以试图用git push origin branch-name推送自己的修改；

2、如果推送失败，则因为远程分支比你的本地更新，需要先用git pull试图合并；

3、如果合并有冲突，则解决冲突，并在本地提交；

4、没有冲突或者解决掉冲突后，再用git push origin branch-name推送就能成功！

5、如果git pull提示“no tracking information”，则说明本地分支和远程分支的链接关系没有创建，用命令git branch --set-upstream branch-name origin/branch-name。

