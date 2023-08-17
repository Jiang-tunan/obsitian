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
3. 解决 gitbash 乱码
	1. 打开 gitbash 执行下面命令
	   `git config --global core.quotepath false`
	2. $(git_home)/etc/bash.bashrc 文件加入下面两行
```
export LANG="zh_CN.UTF-8"
export LC_ALL="zh_CN.UTF-8"
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
5. 解决冲突
```shell
# 拉取远端文件
git pull # == git fech && git merge

# 修改冲突文件 改成自己想要的
# 提交
git add && git commigt && git push

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
```