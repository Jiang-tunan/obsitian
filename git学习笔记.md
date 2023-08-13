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
alias "你设置的命令名称"="原指令"
alias "ct"="cd /home && touch demo.txt
```
3. 解决 gitbash 乱码
	1. 打开 gitbash 执行下面命令
	   `git config --global core.quotepath false`
	2. $(git_home)/etc/bash.bashrc 文件加入下面两行
```
export LANG="zh_CN.UTF-8"
export LC_ALL="zh_CN.UTF-8"
```
