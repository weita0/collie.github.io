---
title: "雨果"
date: 2022-06-04T17:50:49+08:00
draft: false
---

## 写在前面

这篇文章要讲的，不是写出了《巴黎圣母院》、《悲惨世界》以及《九三年》的法国作家维克托雨果，也不是马丁斯科塞斯执导的同名电影，也并非科幻小说届的奥斯卡——雨果奖。本文所要介绍的，是一个名叫雨果的，用于生成静态网站的工具。只需要非常简单的一些步骤，你就能搭建出一个任何人都能够访问的静态网站（博客当然也算在内）。

## 快速实现

首先确保你有一个Github账号，并且会使用一些基本的git命令，电脑上也装有git，如果你具备条件，所有这些步骤大概仅需二十分钟。

在你的电脑上安装Hugo，在MacOS上，可以像我一样方便地使用`brew install hugo`来安装。

安装完成后，执行`hugo new site [projname]`命令，这个命令会为你的项目生成一个目录。

`cd [projname]`进入项目目录。

`git init` 初始化git。

`git submodule add https://github.com/theNewDynamic/gohugo-theme-ananke.git themes/ananke` 为你的网站添加一个主题，通过git submodule的方式。

打开一个文本编辑器，在`config.toml`文件下添加一行，`theme = "ananke"`。

`hugo new posts/first.md`这个命令会为你创建一篇文章草稿。打开这个文件可以看到

```md
---
title: "First"
date: 2022-06-05T16:06:50+08:00
draft: true
---
```

`title`是你这篇文章的标题，默认的标题就是你的文件名去掉中划线。

`draft`表示文章是否是草稿状态，`draft: true`表示这是篇草稿，不会对外展示出来

试着在这个文件下面随便写点什么

`hugo`

这个命令会构建你的网站

编辑`config.toml`，增加一行`baseURL = 'localhost:1313/'`，当然也可以是别的端口号。

`hugo server -D`

在本地启动一个服务，通过`localhost:1313`，就可以看到你的网站了。
