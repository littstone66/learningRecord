# Git学习笔记

## 命令：

1. `git init` 初始一个git仓库
2. `git add` 把文件添加到暂存区
3. `git commit -m '提交描述信息'` 把所有暂存区的文件提交到本地仓库

## 版本回退相关

1. `git log` 查看提交记录
2. `git reset --hard 'commit id号'` 使用`commit id`号将版本回退到指定版本
3. `git reflog` 查看所有提交的记录（可以看到所有的提交`commit id号`），即使当前窗口关闭了也可以回退到指定版本

## 查看修改

1. `git diff` 查看文件所改动的内容

## 撤销修改

1. `git checkout ./ -- 文件名` 放弃工作区的内容，将文件的状态回退到最近一次提交的内容
   1. 如果修改的文件并没有存到暂存区，此命令是将文件的状态回退到上一个commit之前
   2. 如果修改的文件已经add了，并且也做了修改，那么此命令会将文件的状态回退到add状态未修改前

## 分支

1. `git branch dev` 创建名为dev的分支
2. `git checkout dev` 切换到名为dev的分支
3. `git branch` 查看所有的分支
4. `git merge dev` 在master分支上合并dev分支
5. `git branch -d dev` 删除dev分支