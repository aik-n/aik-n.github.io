---
title: Hexo搭建及维护
date: 2021.10.20
author: Aik
img: /source/images/xxx.jpg
top: true
hide: false
cover: true
coverImg: /images/1.jpg
password: 
toc: false
mathjax: false
summary: 记录了Hexo如何从0进行搭建以及后续的维护工作
categories: Hexo
tags:
  - Hexo
  - git
  - node.js

---

# 基于Hexo的博客搭建及维护

本文将说明如何搭建一个自己的Hexo博客，以及后续如何对该博客进行维护。
## 基础搭建

### 准备工作

安装以下应用：
- [Git](http://git-scm.com/)
- [Node.js](https://nodejs.org/en/)

安装完成以后可以通过命令行的方式查看版本号

打开CMD

```
git --version   # 查看git版本号
node			# 查看node.js版本号
```

都能正确显示则表示可以进行下一步了。

### Hexo的安装

新建一个文件夹，后续所有操作都在此文件夹下进行。

安装淘宝的cnpm管理器，可能会提升后续的安装速度（可选），如安装失败则后续还是使用npm进行安装

```
npm -v
npm install -g cnpm --registry=http://registry.npm.taobao.org
cnpm -v
```

使用npm或者cnpm安装Hexo框架

```
npm install -g hexo-cli
hexo -v		# 查看hexo版本信息
```

初始化一个博客

```
hexo init	# 初始化博客
hexo s		# 启动本地blog服务
http://localhost:4000/ 		# 本地访问网页的地址，可以查看初始效果
```

### 通过把博客部署到Github上来进行访问

在Github上创建一个新的仓库（以自己的为例）aik-n.github.io

然后在文件夹中安装git部署插件

```
npm install --save hexo-deployer-git
```

配置文件夹中的配置文件_config.yml

```
# Deployment
	## Docs: https://hexo.io/docs/deployment.html
	deploy:
  		type: git
 		repo: https://github.com/YourGithubName/YourGithubName.github.io.git
  		branch: master
```

之后通过hexo命令将博客部署到Github的仓库中去

```
hexo clean		# 清理一下
hexo g			# 生成
hexo d			# 部署到远程Github仓库
```

即可通过https://aik-n.github.io/来访问自己的博客

## 后续维护

此时在Github上查看仓库中的文件可以发现和本地的文件并不相同，它只包含了网页的静态页面，像是主题以及文章源文件都是不在里面的。因此我们需要将源文件也上传到仓库里去，这样才能方便我们后续的维护工作。

### 创建一个分支

在Github博客的仓库中创建一个分支source,并将其设置为默认分支

在文件夹中进行以下操作：

```
git init		# 建立本地git仓库
gitgit remote add origin https://xxx@xx.git # （将本地的仓库关联到GitHub（码云）上对应的仓库，后面的https链接改成GitHub（码云）上对应的仓库的.git地址）
git add .
git commit -m"提交信息"

```



