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
 git log -p -- src/zabbix_server/poller/poller.c# 查看单个文件详细的修改
 git log --oneline -- path/to/your/file # 查看文件的简洁修改记录
 # 查看文件在特定时间范围内的修改记录
 git log --since="2023-01-01" --until="2023-06-01" -- path/to/your/file
 # 查看文件的某个特定提交的详细内容
 git show COMMIT_HASH -- path/to/your/file
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
# 忽略提交文件
1. 在仓库根目录创建文件`.gitignore`
2. 添加内容到 `.gitignore` 中
```bash
# 如果想忽略位于根目录下的 text.txt 文件
/text.txt

# 而如果你想忽略一个位于根目录下的 test 目录中的 text.txt 文件
/test/text.txt

test/text.txt

# 如果想忽略所有具有特定名称的文件，你需要写出该文件的字面名称。
# 如果你想忽略任何 text.txt 文件，你可以在 .gitignore中添加以下内容
#在这种情况下，你不需要提供特定文件的完整路径。这种模式将忽略位于项目中任何地方的具有该特定名称的所有文件。
text.txt

# 要忽略整个目录及其所有内容，你需要包括目录的名称，并在最后加上斜线 /：
# 这个命令将忽略位于你的项目中任何地方的名为 test 的目录（包括目录中的其他文件和其他子目录

test/

# 需要注意的是，如果你只写一个文件的名字或者只写目录的名字而不写斜线 `/`，那么这个模式将同时匹配任何带有这个名字的文件或目录
# 匹配任何名字带有 test 的文件和目录
test

# 如果你想忽略任何以特定单词开头的文件或目录怎么办
# 例如，你想忽略所有名称以 img 开头的文件和目录。要做到这一点，你需要指定你想忽略的名称，后面跟着 * 通配符选择器，像这样：
img*
# 这个命令将忽略所有名字以 `img` 开头的文件和目录。

# 但是，如果你想忽略任何以特定单词结尾的文件或目录呢？
# 如果你想忽略所有以特定文件扩展名结尾的文件，你需要使用 * 通配符选择器，后面跟你想忽略的文件扩展名
# 例如，如果你想忽略所有以 .md 文件扩展名结尾的 markdown 文件，你可以在你的 .gitignore 文件中添加以下内容：
*.md

# 这个模式将匹配位于项目中任何地方的以 `.md` 为扩展名的任何文件。

# 前面，你看到了如何忽略所有以特定后缀结尾的文件。当你想做一个例外，而有一个后缀的文件你不想忽略的时候，这个模式会忽略所有以 `.md` 结尾的文件，但你不希望 Git 忽略一个 `README.md` 文件。要做到这一点，你需要使用带有感叹号的否定模式，即 `!`，来排除一个本来会被忽略的文件：
# 忽略所有 .md 文件
.md
# 不忽略 README.md 文件
!README.md

# 在 `.gitignore` 文件中使用这两种模式，所有以 `.md` 结尾的文件都会被忽略，除了 `README.md` 文件。

# 需要记住的是，如果你忽略了整个目录，这个模式就不起作用。

# 例如，你忽略了所有的 test 目录：
test/

# 假设在一个 test 文件夹内，你有一个文件，`example.md`，你不想忽略它。你不能像这样在一个被忽略的目录内排除一个文件：

# 忽略所有名字带有 test 的目录
test/
# 试图在一个被忽略的目录内排除一个文件是行不通的
!test/example.md
```

### 如何忽略以前提交的文件

当你创建一个新的仓库时，最好的做法是创建一个 `.gitignore` 文件，包含所有你想忽略的文件和不同的文件模式--在提交之前。
Git 只能忽略尚未提交到仓库的未被追踪的文件。
如果你过去已经提交了一个文件，但希望没有提交，会发生什么？
比如你不小心提交了一个存储环境变量的 `.env` 文件。
你首先需要更新 `.gitignore` 文件以包括 `.env` 文件：

```bash
# 给 .gitignore 添加 .env 文件
echo ".env" >> .gitignore
```

现在，你需要告诉 Git 不要追踪这个文件，把它从索引中删除：

```bash
git rm --cached .env
git rm --cached -r cmake-build-debug
```

`git rm` 命令，连同 `--cached` 选项，从版本库中删除文件，但不删除实际的文件。这意味着该文件仍然在你的本地系统和工作目录中作为一个被忽略的文件。

`git status` 会显示该文件已不在版本库中，而输入 `ls` 命令会显示该文件存在于你的本地文件系统中。

如果你想从版本库和你的本地系统中删除该文件，省略 `--cached` 选项。

接下来，用 `git add` 命令将 `.gitignore` 添加到暂存区：

```bash
git add .gitignore
```

最后，用 `git commit` 命令提交 `.gitignore` 文件：

```bash
git commit -m "update ignored files"
```