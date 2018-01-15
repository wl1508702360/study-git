# git的学习
## 一、什么是git
git是一种分布式的版本控制系统

## 二、git的命令(常用)

git init    &emsp;&emsp;# 初始化本地git仓库(创建新仓库)<br/>

git config --list   &emsp;&emsp;# 显示当前的git配置<br/>

git config --global user.name 'xxx' &emsp;&emsp;# 配置提交者名称<br/>

git config --global user.email 'xxx@xxx.com' &emsp;&emsp;# 配置提交者邮箱<br/>

git config -e [--global] &emsp;&emsp; # 编辑git[global]配置<br/>

git status  &emsp;&emsp; # 查看当前版本状态(是否修改)<br/>

git log     &emsp;&emsp; # 显示当前分支的版本信息<br/>

git add [file]  &emsp;&emsp; # 添加文件到索引库库中，当使用git commit时，git将根据索引库中的内容进行提交<br/>

git add [dir]   &emsp;&emsp; # 添加目录包括其子目录到暂存区<br/>

git add .       &emsp;&emsp; # 添加当前目录下的所有文件到暂存区<br/>

git rm [file]   &emsp;&emsp; # 删除工作区中的文件[文件还存在于缓存区]<br/>

git rm --cache [file] &emsp;&emsp; # 停止追踪指定文件<br/>

git mv [original-name] [final-name]  &emsp;&emsp; # 修改文件的名称<br/>

git commit -v   &emsp;&emsp; # 提交时显示所有不同的信息<br/>

git commit -m 'message' &emsp;&emsp; # 提交文件到仓库[-m后面添加对提交内容的说明]<br/>

git commit -a &emsp;&emsp; # 提交工作区自上次commit后的所有变化到仓库中<br/>

git commit --amend -m 'message' &emsp;&emsp; # 重新提交一次, 替代前次提交<br/>

git remote add origin '远程仓库' &emsp;&emsp; # 添加远程仓库到本地并命名为origin

git push [-u] origin master &emsp;&emsp; # 将当前分支push到远程master分支上[-u => --set-upstream] ==> 设置分支