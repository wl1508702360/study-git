# git的学习
## 一、什么是git
git是一种分布式的版本控制系统

## 二、git的命令(常用)

git init    &emsp;&emsp;# 初始化本地git仓库(创建新仓库)
<br/>

git config --list   &emsp;&emsp;# 显示当前的git配置

git config --global user.name 'xxx' &emsp;&emsp;# 配置提交者名称

git config --global user.email 'xxx@xxx.com' &emsp;&emsp;# 配置提交者邮箱

git config -e [--global] &emsp;&emsp; # 编辑git[global]配置
<br/>

git status  &emsp;&emsp; # 查看当前版本状态(是否修改)

git log     &emsp;&emsp; # 显示当前分支的版本信息

git log --stat  # 显示提交历史，以及每次提交发生变更的文件

git log -S [keywords] # 根据关键词搜索相关信息

git reflog  # 显示当前分支最近的几次操作
<br/>

git add [file]  &emsp;&emsp; # 添加文件到暂存库中，当使用git commit时，git将根据暂存库中的内容进行提交

git add [dir]   &emsp;&emsp; # 添加目录包括其子目录到暂存区

git add .       &emsp;&emsp; # 添加当前目录下的所有文件到暂存区
<br/>

git rm [file]   &emsp;&emsp; # 删除工作区中的文件[文件还存在于缓存区]

git rm --cache [file] &emsp;&emsp; # 停止追踪指定文件

git mv [original-name] [final-name]  &emsp;&emsp; # 修改文件的名称
<br/>

git commit -v   &emsp;&emsp; # 提交时显示所有不同的信息

git commit -m 'message' &emsp;&emsp; # 提交文件到仓库[-m后面添加对提交内容的说明]

git commit -a &emsp;&emsp; # 提交工作区自上次commit后的所有变化到仓库中

git commit --amend -m 'message' &emsp;&emsp; # 重新提交一次, 替代前次提交
<br/>

git branch  &emsp;&emsp;&emsp;&emsp; # 列出所有本地的分支

git branch -r  &emsp;&emsp;&emsp;&emsp; # 列出所有远程分支

git branch -a  &emsp;&emsp;&emsp;&emsp; # 列出所有分支[本地+远程]

git branch -v  &emsp;&emsp;&emsp;&emsp; # 查看各个分支最后一个提交对象的信息

git branch [branch-name]    # 新建分支，依然停留在当前分支上

git branch -d [branch-name] # 删除指定分支

git branch -D [branch-name] &emsp;&emsp; # 强制删除指定分支

git branch -m master master_name &emsp; # 本地分支改名

git branch --merge &emsp;&emsp;&emsp; # 显示所有已合并到当前分支上的分支

git branch --no-merge &emsp;&emsp;&emsp; # 显示所有未合并到当前分支上的分支 
<br/>

git checkout [branch-name] &emsp;&emsp; # 切换到指定分支

git checkout -b [branch-name] &emsp;&emsp; # 新建分支，并切换到新建的分支上

git checkout - &emsp;&emsp;&emsp;&emsp; # 切换到上一个分支上
<br/>

git merge [branch-name] &emsp;&emsp;&emsp;# 合并指定分支到当前分支上
<br/>

git remote add origin '远程仓库' &emsp;&emsp; # 添加远程仓库到本地并命名为origin

git push [-u] origin master &emsp;&emsp;&emsp; # 将当前分支push到远程master分支上[-u => --set-upstream] ==> 建立追踪关系

git push origin --delete [branch-name] &emsp;&emsp; # 删除远程分支
