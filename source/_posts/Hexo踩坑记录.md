---
title: Hexo踩坑记录
date: 2021.10.20
author: Aik
img: /source/images/xxx.jpg
top: true
hide: false
cover: true
coverImg: /images/1.jpg
password: 
toc: true
mathjax: true
summary: 记录了Hexo使用中遇到的一些问题
categories: Hexo
tags:
  - Hexo
  - Git
  - node.js
---

**hexo使用theme出现``“ {% extends ‘_layout.swig‘ %} {% import ‘_macro/post.swig‘ as post_template %}“``问题**

原因是hexo在5.0之后把swig给删除了需要自己手动安装

```java
 npm i hexo-renderer-swig
```

**hexo出现以下报错**

```
INFO  Validating config
INFO  Start processing
FATAL {
  err: Template render error: (unknown path)
    Error: template names must be a string: undefined
      at Object._prettifyError (D:\DataSource\blog\node_modules\nunjucks\src\lib.js:36:11)
      at D:\DataSource\blog\node_modules\nunjucks\src\environment.js:563:19

```

多半是因为markdown文件中有大括号，要么不用，要么转义字符&#123和&#125