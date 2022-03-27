## git 简介
### 分布式代码管理工具，分布式版本控制系统

## git 常用指令
### git init （创建本地git仓库）
### git add （把文件添加到仓库）
- 实际上就是把文件修改添加到暂存区
### git commit -m （把文件提交到仓库）
- 把暂存区的所有内容提交到当前分支
- 每次修改，如果不用git add到暂存区，那就不会加入到commit中
### git status （查看仓库当前状态）
### git diff （仓库文件被修改了什么）
### git log (查看历史记录)
#### --pretty=oneline 精简信息
#### --graph （看到分支合并图）
### git reset （版本回退）
#### --hard 
	+ HEAD^上个版本，HEAD^^上上版本，以此类推，HEAD~100
	+ commitId 
	+ <file> 把文件在暂存区的修改撤销掉（unstage）
### git reflog （记录每一条指令）
### git switch （切换分支，新）
#### -c （创建并切换到新的分支）
### git checkout （切换分支，旧）
#### -- fileName 如-- readme.txt
- 没有 -- 会变成切换到另一个分支
#### -b （创建并切换至新分支）
### git rm （用于删除一个文件）
### git branch （查看当前分支）
#### -d（删除指定分支）
### git merge （合并指定分支到当前分支）
### git stash （储藏代码）
#### list （查看储藏）
#### apply （弹出储藏）
#### drop （删除储藏）
#### pop (apply+drop)