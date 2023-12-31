---
date:
    created: 2022-02-05
    updated: 2023-12-31
slug: git
authors: [linkchen]
categories: [Misc, Updating]
tags: [Git, Misc, Updating]
comments: true
---

# Git 笔记

[官方文档](https://git-scm.com/docs)，[菜鸟教程](https://www.runoob.com/git/git-tutorial.html)

-   working directory 工作区
-   staging area 暂存区
-   repository 版本库

<!-- more -->

![staging area](https://git-scm.com/images/about/index1@2x.png)

## 创建仓库

1. `git init` 当前目录
2. `git init dir` 指定目录

## 克隆仓库

1. `git clone url` 默认目录名为仓库名
2. `git clone url dir` 克隆到指定目录
3. `git clone -b branchname url` 克隆指定分支，没有`-b`默认克隆 master 分支

## 设置提交代码时的用户信息

1. `git config --global user.name "username"` 用户名
2. `git config --global user.email email@xxx.com` 邮箱

## 分支管理

1. `git branch` 列出分支
2. `git branch branchname` 创建分支
3. `git branch -d branchname` 删除分支
4. `git checkout branchname` 切换指定分支
5. `git checkout -b branchname` 创新分支并立即切换
6. `git merge branchname` 合并分支到当前分支

## 提交与修改

1. `git status` 查看当前的状态，显示有变更的文件
2. `git status -s` 简短输出
3. `git diff` 比较文件的不同，即暂存区和工作区的差异
4. `git diff filename` 指定文件
5. `git log` 查看提交历史
6. `git log --online` 简短输出
7. `git blame filename` 以列表形式查看指定文件的历史修改记录
8. `git add .` 添加所有文件到暂存区
9. `git commit -m "message"` 将暂存区内容提交到本地仓库中
10. `git commit -am "message"` 首先 add 所有修改的文件，再提交，新创建的文件不会被添加
11. `git reset --mixed commitID` 默认回退模式，可以不填`--mixed`，回退版本库，回退暂存区，保留工作区
12. `git reset --soft commitID` 只回退版本库，commit 的信息
13. `git reset --soft commitID` 回退所有信息，工作区源码也会回退

## 远程仓库

1. `git remote` 查看远程仓库
2. `git remote -v` verbose 显示更多信息
3. `git remote show remotename` 显示指定远程仓库的信息
4. `git remote add remotename url` 添加远程仓库
5. `git push remotename` 推送当前分支到远程仓库
