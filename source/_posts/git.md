---
title: git使用心得
date: 2022-03-28
description: git用法
tag: web, github
author: holobo
---

# github
  代码修改成功后，需要push到github的操作如下：
## 一、 cd Develop/holobo 进入目标文件夹
## 二、显示并进行分支操作
  _git branch_
```
git branch                       # 显示本地分支
git branch --contains 50089      # 显示包含提交50089的分支
git branch -a                    # 显示所有分支
git branch -r                    # 显示所有原创分支
git branch --merged              # 显示所有已合并到当前分支的分支
git branch --no-merged           # 显示所有未合并到当前分支的分支
git branch -m master master_copy # 本地分支改名
git show-branch                  # 图示当前分支历史
git show-branch --all            # 图示所有分支历史
```
  _git checkout_
```
git checkout -b master_copy          # 从当前分支创建新分支master_copy并检出
git checkout -b master master_copy   # 上面的完整版
git checkout features/performance    # 检出已存在的features/performance分支
git checkout --track hotfixes/BJVEP933   # 检出远程分支hotfixes/BJVEP933并创建本地跟踪分支
git checkout v2.0                        # 检出版本v2.0
git checkout -b devel origin/develop     # 从远程分支develop创建新本地分支devel并检出
git checkout -- README       # 检出head版本的README文件（可用于修改错误回退）
```
  _git diff_
```
git diff                       # 显示所有未添加至index的变更
git diff --cached              # 显示所有已添加index但还未commit的变更
git diff HEAD^                 # 比较与上一个版本的差异
git diff HEAD -- ./lib         # 比较与HEAD版本lib目录的差异
git diff origin/master..master # 比较远程分支master上有本地分支master上没有的
git diff origin/master..master --stat      # 只显示差异的文件，不显示具体内容
```
  _git log\show_
```
git log                        # 显示提交日志
git log -1                     # 显示1行日志 -n为n行
git log --stat                 # 显示提交日志及相关变动文件
git log -p -m
git show dfb02                 # 可只用commitid的前几位
git show HEAD                  # 显示HEAD提交日志
git show HEAD^                 # 显示HEAD的父（上一个版本）的提交日志 ^^为上两个版本 ^5为上5个版本
git show v2.0                  # 显示v2.0的日志及详细内容
git log v2.0                   # 显示v2.0的日志
```
## 三、添加改动
  _git add_
```
git add xyz                    # 添加xyz文件至index
git add .                      # 增加当前子目录下所有更改过的文件至index
```
## 四、查看状态是否添加成功
 _git status_
 ```
 git status                    # 查看当前版本状态（是否修改）
 ```
## 五、申明改动，添加名称
  _git commit_
```
git commit -m 'xxx'            # 提交
git commit --amend -m 'xxx'    # 合并上一次提交（用于反复修改）
git commit -am 'xxx'           # 将add和commit合为一步
```
## 六、重新查看status，随后push
  _git push_
```
git push --set-upstream origin 分支名称
git push origin master                # 将当前分支push到远程master分支
git push origin :hotfixes/BJVEP933    # 删除远程仓库的hotfixes/BJVEP933分支
git push --tags                       # 把所有tag推送到远程仓库
```
## 七、从github仓库里回拉文件
  _git pull_
```
git pull origin master           # 获取远程分支master并merge到当前分支
```
## 八、放入暂存区，以栈堆的形式，先进后出，后进先出的方式存放。
  _git stash_
```
git stash                        # 暂存当前修改，将所有至为HEAD状态
git stash list                   # 查看所有暂存
git stash show -p stash@{0}      # 参考第一次暂存
git stash apply stash@{0}        # 应用第一次暂存
git stash pop                    # 释放存储
```
## 九、特别注意，一般工作首先新建test分支进行改动，最后提交也是test，待test审核通过后，本地进行pull，成功后删除test，保留原主项目。
