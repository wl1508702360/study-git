# git的学习
## 一、什么是git
git是一种分布式的版本控制器

## 二、git的命令
git init    ------    # 初始化本地git仓库(创建新仓库)<br/>
git config --global user.name 'xxx'  ------  # 配置用户名<br/>
git config --global user.email 'xxx@xxx.com ------ # 配置用户邮箱<br/>
git config --list ------ # 显示当前的git配置<br/>
git status  ------  # 查看当前版本状态(是否修改)<br/>
git add file    ------  # 添加file文件到索引库中，当使用git commit时，git将根据索引库中的内容进行提交<br/>
git commit -m 'xxx' ------  # 提交