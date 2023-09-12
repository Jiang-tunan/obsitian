# 一、工作流程图
![[git流程图.png]]
___
# 二 基本配置
1. 设置用户名和邮箱
	1. 设置用户名
	   `git config --global user.name "你的名字"`
	2. 设置邮箱
	   `git config --global user.email "你的邮箱"`
2. 为常用指令配置别名
```shell
# 在用户目录下创建 .bashrc 文件
touch ~/.bashrc
# 打开 .bashrc 文件
vim ~./bashrc
# 键入以下内容 多条指令间用 && 连接
alias 你设置的命令名='原指令'
alias ct='cd /home && touch demo.txt'
# 保存退出后在终端输入
source ~/.bashrc
```
# 三 基础操作指令
1. 初始化仓库
   `git init`
2. 工作区->暂存区
```shell
git add filename #添加单个文件
git add . # 添加所有文件到暂存区
``` 
3. 暂存区->本地仓库
`git commit -m "记录说明文本"`
4. 查看日志
```shell
 git log  # 查看日志
 git log --all # 显示所有分支
 git log --pretty=online # 将提交信息显示为一行
 git log --abbrev-commit # 是输出的 commitid 更加简短
 git log --graph # 以图形形式显示
 git reflog # 查看已删除的记录
 git log --all --pretty=oneline --abbrev-commit --graph
```
5. 查看状态
`git status`
6. 版本回退
```shell
git reset --hard commitID

# 撤销 commit
git reset HEAD~1

# 撤销 push
git revert <commit-SHA>
```
7. 添加忽略管理内容
```shell
# 项目更目录创建 .gitignore 文件
touch .gitignore 
# 在./gitignore文件中添加忽略项
```
8. 分支操作
```shell
# 查看分支
git branch

# 创建分支
git branch feaname

# 切换分支
git checkout feaname

# 创建 && 切换分支
git checkout -b feaname

# 合并分支 将 feaname 合并到当前分支
git merge feaname

# 删除分支
git branch -d feaname
git branch -D feaname # 强制删除

# 修改分支名
git branch -m newname
```
9. 查看文件变化
```shell
# 为暂存或未提交与最近一次提交的不同
git diff

# 暂存区与最近一次提交
git diff --staged

#当前工作目录与指定分支或提交的差异
git diff branch_name
git diff comit_hash

# 比较两个不同分支差异
git diff branch_name1 brnach_name2
git diff commit_hash1 commit_hash2
```
10. 保存到临时的存储区
```shell
# 存工作目录中的更改 这个命令将工作目录中的所有未提交更改保存到一个新的存储堆栈中，同时可以添加一条描述性消息。
git stash save "Your stash message"

# 查看存储的堆栈列表:这个命令会列出所有存储的堆栈，每个堆栈都有一个唯一的名称，通常是 `stash@{n}`，其中 `n` 是堆栈的索引。
git stash list

# 恢复最新的存储：这个命令会将最新的存储堆栈中的更改应用到工作目录中，但不会将存储堆栈弹出。
git stash apply

# 恢复并删除最新的存储：这个命令与 `git stash apply` 类似，但它会将存储堆栈中的更改应用到工作目录后，将该存储堆栈从列表中删除。
git stash pop

# 恢复特定的存储：这个命令允许你从存储堆栈中选择一个特定的存储并将其应用到工作目录中，其中 `n` 是存储堆栈的索引。
git stash apply stash@{n}

# 删除存储堆栈：如果你不再需要特定的存储堆栈，可以使用此命令将其从列表中删除。
git stash drop stash@{n}

# 清除所有存储堆栈：这个命令会删除所有存储堆栈，慎用，因为它会永久删除所有保存的更改。
git stash clear
```
# 远程仓库
1. 生成 ssh 公钥
`ssh-keygen -t rea`
2. 添加远程仓库
```
git remote add origin 地址

```
3. 推送仓库
```shell
# 推送到指定分支
git push origin 本地分支名:远程分支名

# 建立本地和远程的关联
git push --set-upstream origin 远程分支名

# 查看关联关系
git branch -vv
```
4. 获取远程仓库
`git clone 地址`
5. 抓取和拉取
```shell
# 
git fetch
git merge 分支名
git pull
```
6. 解决冲突
```shell
# 拉取远端文件
git pull # == git fech && git merge

# 修改冲突文件 改成自己想要的
# 提交
git add && git commigt && git push

```
7. 常用操作
```shell
# 查看绑定的分支
git branch -vv

# 查看当前分支与远程建立连接分支的差异
git diff origin/branch_name..local_branch_name

# 清理远程仓库i不存在的分支
git remote prune origin

# 查看远程仓库所有分支
git remote show origin

# 获取远程仓库指定分支最新的更改
git fetch origin branch_name

# 撤销 add 操作
git restore --staged .
```
# 常见问题
1. 换行符问题
```shell
# windows 设置
#提交时转换为LF，检出时转换为CRLF
git config --global core.autocrlf true

# linux
#提交时转换为LF，检出时不转换
git config --global core.autocrlf input

#提交检出均不转换
git config --global core.autocrlf false

# 将两个没有共同历史的分支合并起来
git pull origin main --allow-unrelated-histories
```
2. 解决 gitbash 中文乱码
	1. 打开 gitbash 执行下面命令
	   `git config --global core.quotepath false`
	2. $(git_home)/etc/bash.bashrc 文件加入下面两行
```
export LANG="zh_CN.UTF-8"
export LC_ALL="zh_CN.UTF-8"
```