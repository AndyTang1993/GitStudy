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

注：切换分支时，保证当前分支已经没有变动。
如果主分支bug已经改完，开发分支要在这个基础上继续开发，需要同步到开发分支上面，命令行如下：
（1）先切换到开发分支 git checkout name
（2）git rebase 主分支名
（3）此时如果有冲突，需要先解决冲突，然后 git add -u
（4）git rebase --continue 
（5）完成，此时，开发分支就跟主分支没有差别了

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

10、标签管理（tag）
git tag xxx （打一个新标签）
git tag（查看所有标签）
注：git tag xxx commitid（根据commitid打标签）
带说明的标签如下：
例：git tag -a v0.1 -m "说明" 3628164
git show <tagname>（查看标签信息）
git tag -s <tagname> -m "说明"（用PGP签名打标签）

git tag -d <tagname>（删除标签）
git push origin <tagname>（推送某个标签到远程）
git push origin --tags（一次性推送全部尚未推送到远程的本地标签）
git tag -d <tagname>（删除一个本地标签）
git push origin :refs/tags/<tagname>（删除一个远程标签）

11、自定义Git
git config --global color.ui true（Git显示颜色）
忽略特殊文件：https://github.com/github/gitignore
1、忽略操作系统自动生成的文件，比如缩略图等；
2、忽略编译生成的中间文件、可执行文件等，也就是如果一个文件是通过另一个文件自动生成的，那自动生成的文件就没必要放进版本库，比如Java编译产生的.class文件；
3、忽略你自己的带有敏感信息的配置文件，比如存放口令的配置文件。

忽略某些文件时，需要编写.gitignore；
.gitignore文件本身要放到版本库里，并且可以对.gitignore做版本管理！
git add -f xxx（强制添加到git）

12、命令别名
git config --global alias.xx <原名>（简写命令）
git config --global alias.last 'log -1'（显示最后一次提交信息改为last）
git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"（查看log）

Git配置文件都放在.git/config，别名就在[alias]后面，要删除别名，直接把对应的行删掉即可