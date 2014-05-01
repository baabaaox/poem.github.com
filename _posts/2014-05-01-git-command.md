---
layout: post
title: git常用命令
---

在这篇文章里面我会记录各种git用法，可能你每次打开这篇文章看到的内容都不一样，对！我会不停的编辑。<!-- more -->

#### 创建

    git init

#### 状态

    git status
    git status -s

#### 添加

    git add *
    git add .
    git add -i

#### 缓存

    git reset HEAD *
    git reset HEAD .
    git rm -r --cached .
    git checkout file

#### Change Remote

    git remote set-url origin git@github.com:poem/poem.github.com.git

#### Add Tag

    git tag 1.0.0 a2fej230fe

#### Remove Tag

    git tag -d 1.0.0
    git push origin :refs/tags/1.0.0

#### 追加

    git commit --amend
