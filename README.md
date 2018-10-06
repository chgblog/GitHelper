初始化存储库：
git init

设置账号：
git config --global user.name "用户名"
git config --global user.emila "邮箱"

添加文件到暂存区：
git add 文件名

#添加所有文件到暂存区：
git add .

暂存区撤销文件：
git reset HEAD -- 文件名

工作区恢复到上一次更改，需要先把暂存区撤销后再执行（注意，只有提交到存储库的文件才有效）：
git checkout -- 文件名

暂存区提交到存储库：
git commit -m "备注"

撤销某次的提交：
git reset 版本编号

撤销上一版本到暂存区，与增加--mixed参数一样：
git reset HEAD~1

版本库指针指向上一版本提交：
git reset --soft HEAD~1

撤销上一版本到暂存区和工作区：
git reset --hard HEAD~1

撤销指定版本到暂存区和工作区（先用git log查到要回滚的版本编号）：
git reset --hard 版本编号

对比指定文件暂存区和工作区的差异：
git diff 文件名

对比指定文件版本库指定版本和工作区的差异：
git diff 版本编号 文件名

对比版本库上一版本和工作区的差异：
git diff HEAD~1 文件名

对比版本库中上次提交和工作区的差异：
git log -p -1

查看指定文件每行代码修改人：
git blame 文件名

删除文件，删除后再提交才会从存储库删除：
git rm 1.js
git commit -m "删除1.js"

克隆远程存储库：
git clone "存储库地址"

连接到远程存储库：
git remote add origin git@github.com:chgblog/GitHelper.git		#使用ssh协议链接，配置ssh key后每次输入key的密码
git remote add origin https://github.com/chgblog/GitHelper.git  #使用https协议链接，每次需要输入账号

推送本地存储库到远程存储库，并建立远程存储库origin与本地存储库master的连接：
git push -u origin master

推送本地存储库test_branch分支到远程存储库test_branch，如果远程没有则建立：
git push -u origin test_branch:test_branch

关联本地与远程存储库后可以直接推送：
git push

获取远程存储库更改到本地存储库：
git pull

查看分支：
git branch

查看分支及当前版本：
git branch -v

查看本地和远程分支:
git branch -a -v

新建分支：
git branch 分支名

切换到指定分支：
git checkout 分支名

新建并切换到新建的分支：
git checkout -b 分支名

删除非当前分支：
git branch -d 分支名

删除一个没有合并到主分支的分支：
git branch -D 分支名

删除远程分支：
git push origin --delete 分支名

合并分支，会把分支commit记录合并过来（注意，这个操作是把目标分支合并到当前分支，所以通常是先切换到master再合并）：
git merge 分支名

合并分支,但不把分支的commit记录合并过来，合并后需要commit
git merge --squash 分支名

查看标签
git tag

添加标签：
git tag 标签名

删除标签：
git tag -d 标签名

推送标签到远程：
git push origin 标签名

查看提交日志：
git log

以简洁的方式查看提交日志：
git log --oneline
git log --graph --oneline

查看所有日志，包括撤销的版本：
git log --all

以简洁的方式查看日志，包括撤销的版本：
git reflog

把当前未添加到暂存区的保存到临时缓存，并恢复当前工作目录为未修改之前：
git stash save "提交到临时缓存备注"

暂存区的内容加载到当前工作目录，如果有冲突，则以后修改的为准：
git stash apply

暂存区和工作区改名或移动：
git mv 旧文件名 新文件名

修改上一次提交的备注及补充新的提交：
git commit -m "备注" --amend

获取远程的更改到本地并建立一个新分支：
git fetch

从远程的origin存储库的master分支下载代码到本地的origin master：
git fetch origin master

合并下载下来的远程的master分支到当前分支，当远程版本树与本地版本树不一样时使用，不会产生多余的历史日志：
git rebase origin/master

rebase遇到冲突后，先解决冲突（修改文件），然后再add、commit，然后继续rebase：
git rebase --continue

终止rebase的操作，分支会回到rebase开始前的状态：
git rebase --abort

master之后到feature分支的commit树放到master树上面：
git rebase --onto master master feature

复制某段更改的commit到当前分支：
git cherry-pick 58a8c8e ca32a6d

查找包含TODO的代码：
git grep TODO

修改3d18a58之后的历史提交，更改哪行对应要修改的提交，pick是不修改：
git rebase -i 3d18a58

系统根据二分法自动切换到（reset）某个版本，确认给版本是否有错后输出git bisect bad/good标记，测试完后显示第一个出错的版本号：
1.启动找错：
git bisect start
2.标记第一个没有错的版本：
git bisect good 版本号
3.标记最后一个出错的版本：
git bisect bad 版本号
4.找到错误后恢复到bisect start之前的状态：
git bisect reset

自动测试，脚本返回0为正确，1（非0）为错误：
git bisect run 脚本/命令/程序

忽略指定文件，忽略的文件不加入版本库：
建立.gitignore文件，里面的文件不加入版本库，可以使用统配符
