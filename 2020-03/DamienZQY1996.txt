Git is a version control system.
Git is free software.


初始化一个Git仓库，使用‘git init’命令。
添加文件到Git仓库，分两步：
1.使用‘git add <file>’命令,将文件修改添加到暂存区。注意，可反复多次使用，添加多个文件；
2.使用命令‘git commit -m <messages>’，将暂存区的所有内容提交到master分支版本库。


随时掌握工作区的状态，使用‘git status’命令。
如果‘git status’告诉你有文件被修改过，用‘git diff’可以查看修改内容。


使用‘cat’命令查看文件内容。
使用‘git log’命令显示从最近到最远的提交日志，如果嫌输出信息太多，加上‘--pretty=oneline’参数。
HEAD指向的版本就是当前版本，因此，Git允许在版本的历史之间穿梭，使用命令‘git reset --hard commit_id’。
重新回到最近版本，用‘git reflog’命令查看历史，以便确定回到最近的哪个版本。


git跟踪并管理的是修改，并非文件。
每次修改需要用‘git add’命令将修改放入暂存区，最后统一用‘git commit’命令加入版本库。


场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令‘git checkout -- <file>’。
场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步：
1.用‘git restore --staged <fi1e>‘，回到了场景1；
2.按场景1操作。


场景1：将版本库中的文件删除，用命令’git rm‘和’git commit‘。
场景2：仅删除工作区中文件，用命令’rm‘；恢复删除文件到最新版本：’git checkout -- <file>‘。注意：从来没有被添加到版本库就被删除的文件，是无法恢复的。


关联远程库，使用命令‘git remote add origin git@server-name:path/repo-name.git’。
关联后，使用命令‘git push -u origin master’第一次推送master分支的所有内容。
此后，每次本地提交后，只要有必要，就可以使用命令‘git push origin master’推送最新修改。


克隆远程库，首先必须知道仓库的地址，然后使用命令‘git clone’克隆。
git支持多种协议，默认的‘git://’使用ssh，但也可以使用‘https://’等其他协议。
使用‘https://’除了速度慢，还有最大的麻烦是每次推送都必须输入口令，但是在某些只开放http端口的公司内部就无法使用ssh协议而只能用https。


查看分支：‘git branch’
创建分支：‘git branch <name>’
切换分支：‘git switch <name>’（推荐）或‘git checkout <name>’
创建+切换分支：‘git switch -c <name>’（推荐）或‘git checkout -b <name>’
合并某分支到当前分支：‘git merge <name>’
删除分支：‘git branch -d <name>’


当git无法自动合并分支时，就必须首先解决冲突。解决冲突后，再提交，合并完成。
解决冲突就是把git合并失败的文件手动编辑为我们希望的内容，再提交。
用git log --graph命令可以看到分支合并图。


实际开发中，我们应该按照如下基本原则进行分支管理：
1.master分支应该时非常稳定的，也就是仅用来发布新版本，平时不在上面干活；
2.干活都在dev分支上，到比如1.0版本发布时，再把dev分支合并到master上，在master分支发布1.0版本；
3.团队每个人都在dev分支上干活，每个人都有自己的分支，时不时地往dev分支上合并。


合并分支时，加上‘--no-ff’参数就可以用普通模式合并，合并后的历史有分支。


修复bug时，我们会通过创建新的bug分支进行修复，然后合并，最后删除。
当手头工作没有完成时，先把工作现场‘git stash’一下，然后去修复bug，修复后，再‘git stash pop’，回到工作现场。
在master分支上修复的bug，想要合并到当前dev分支，可以用‘git cherry-pick <commit>’命令，把bug提交的修改“复制”到当前分支，避免重复劳动。


开发一个新feature，最好新建一个分支。
如果要丢弃一个没有被合并过的分支，可以通过‘git branch -D <name>’强行删除。


多人协作的工作模式：
1.试图用‘git push origin <branch-name>’推送自己的修改；
2.如果推送失败，则因为远程分支比你的本地更新，需要先用‘git pull’试图合并；
3.如果合并有冲突，则解决冲突，并在本地提交；
4.没有冲突或者解决掉冲突后，再用‘git push origin <branch-name>’推送就能成功。
注意：如果‘git pull’提示‘no tracking information’，则说明本地分支和远程分支的链接关系没有创建，用命令‘git branch --set-upstream-to <branch-name> origin/<branch-name>’。


查看远程库信息，使用‘git remote -v’
本地新建的分支如果不推送到远程，对其他人就是不可见
在本地创建和远程分支对应的分支，使用‘git switch -c branch-name origin/branch-name’，本地和远程分支名称最好一致


rebase操作可以把本地未push的分叉提交历史整理成直线
rebase的目的是使得我们在查看历史提交的变化时更容易，因为分叉的提交需要三方对比


命令‘git tag <tagname> <commit_id>’用于新建一个标签，指向commit_id
命令‘git tag -a <tagname> -m "xxxxx" <commit_id>’可以指定标签信息
命令‘git tag’可以查看所有标签


命令‘git push origin <tagname>’可以推送一个本地标签
命令‘git push origin --tags’可以推送全部未推送的本地标签
命令‘git tag -d <tagname>’可以删除一个本地标签
命令‘git push origin :refs/tags/<tagname>’可以删除一个远程标签

