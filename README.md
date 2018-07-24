## 分布式版本与集中式版本区别
+ 集中式版本控制系统，版本库是集中存放在中央服务器的
+ 分布式版本控制系统根本没有“中央服务器”，每个人的电脑上都是一个完整的版本库，分布式版本控制系统通常也有一台充当“中央服务器”的电脑，但这个服务器的作用仅仅是用来方便“交换”大家的修改，没有它大家也一样干活，只是交换修改不方便而已。

## git 起源
* linus大神用c语言两周写成

## git 配置
* git config --global user.name "Your Name"
* git config --global user.email "email@example.com"

## 常用命令
```
git init
git add
git commit
git status
git diff(--cached)
git log
git reflog
git reset --hard commit-id
```
* git add->暂存区，commit-> master分支(默认)
* git管理的是修改，不是文件。比如对同一个文件进行两次修改，只在第一次修改之后进行add操作，然后commit。第二次修改的内容并没有被提交。

## 撤销修改
* 场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令git checkout -- file。

* 场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令git reset HEAD <file>，就回到了场景1，第二步按场景1操作。

* 场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，git reset --hard commit-id，不过前提是没有推送到远程库。

## 远程库
	* 自己搭建
	* 使用github
	  创建、上传公钥、关联、推送

## 分支：
* 查看分支：git branch
* 创建分支：git branch <name>
* 切换分支：git checkout <name>
* 创建+切换分支：git checkout -b <name>
* 合并某分支到当前分支：git merge <name>
	合并分支时，加上--no-ff参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而fast forward合并就看不出来曾经做过合并。
* 删除分支：git branch -d <name>
	如果要丢弃一个没有被合并过的分支，可以通过git branch -D <name>强行删除。

## 现场保存
* 修复bug时，我们会通过创建新的bug分支进行修复，然后合并，最后删除；
* 当手头工作没有完成时，先把工作现场git stash一下，然后去修复bug，修复后，git stash list查看列表，再git stash pop，回到工作现场。

## 远程库

* 查看远程库信息，使用git remote -v；
* 本地新建的分支如果不推送到远程，对其他人就是不可见的；
* 从本地推送分支，使用git push origin branch-name，如果推送失败，先用git pull抓取远程的新提交；
* 在本地创建和远程分支对应的分支，使用git checkout -b branch-name origin/branch-name，本地和远程分支的名称最好一致；
* 建立本地分支和远程分支的关联，使用git branch --set-upstream branch-name origin/branch-name；
* 从远程抓取分支，使用git pull，如果有冲突，要先处理冲突。

  *rebase操作可以把本地未push的分叉提交历史整理成直线；
rebase的目的是使得我们在查看历史提交的变化时更容易，因为分叉的提交需要三方对比。*

## 标签

**标签总是和某个commit挂钩。如果这个commit既出现在master分支，又出现在dev分支，那么在这两个分支上都可以看到这个标签。**

* 命令git tag <tagname>用于新建一个标签，默认为HEAD，也可以指定一个commit id；
* 命令git tag -a <tagname> -m "blablabla..."可以指定标签信息；
* 命令git tag可以查看所有标签。
* 命令git push origin <tagname>可以推送一个本地标签；
* 命令git push origin --tags可以推送全部未推送过的本地标签；
* 命令git tag -d <tagname>可以删除一个本地标签；
* 命令git push origin :refs/tags/<tagname>可以删除一个远程标签。

## gitignore
* 忽略某些文件时，需要编写.gitignore；
* .gitignore文件本身要放到版本库里，并且可以对.gitignore做版本管理！

## 配置别名

* 设置查看日志别名
  git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"

* 配置Git的时候，加上--global是针对当前用户起作用的，如果不加，那只针对当前的仓库起作用。
* 每个仓库的Git配置文件都放在.git/config文件中：
而当前用户的Git配置文件放在用户主目录下的一个隐藏文件.gitconfig中：

## git 使用

* 首先，可以试图用git push origin <branch-name>推送自己的修改；
* 如果推送失败，则因为远程分支比你的本地更新，需要先用git pull试图合并；
* 如果合并有冲突，则解决冲突，并在本地提交；
  没有冲突或者解决掉冲突后，再用git push origin <branch-name>推送就能成功！
* 如果git pull提示no tracking information，则说明本地分支和远程分支的链接关系没有创建，用命令git branch --set-upstream-to <branch-name> origin/<branch-name>。
**当Git无法自动合并分支时，就必须首先解决冲突。解决冲突后，再提交，合并完成。
解决冲突就是把Git合并失败的文件手动编辑为我们希望的内容，再提交。
用git log --graph命令可以看到分支合并图。**

## 学习资源
* Git教程[廖雪峰]
https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000
* 动图理解git
http://git-school.github.io/visualizing-git/#free
* 闯关学习git
https://learngitbranching.js.org/
* git命令
https://services.github.com/on-demand/resources/cheatsheets/

