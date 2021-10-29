---
title: Git踩坑记录
date: 2021.10.29
author: Aik
img: /source/images/xxx.jpg
top: true
hide: false
cover: true
coverImg: /images/1.jpg
password: 
toc: true
mathjax: true
summary: 记录了Git使用过程中遇到的一些问题
categories: Git
tags:
  - Git
---

# Git踩坑记录

### .gitgnore文件

.gitignore只能忽略掉那些原来没有被追踪（track）的文件，所以如果有一些文件提交到了git仓库当中，接受了git追踪,那么直接修改.gitignore是无效的。

比如一些配置文件，本地还要，直接删除仓库中的文件，也就删除了跟踪，提交上去后再配置gitignore就生效了

先执行git rm --cached package.json，然后提交上去，后面这个文件的改动就会被忽略了,可能需要 -r

```
git rm --cached public/ -r
```

