---
layout:     post
title:      "Github Pages + Jekyll搭建独立博客教程"
subtitle:   ""
author:     "zhuowl"
header-img: "img/post-bg-js-version.jpg"
tags:
    - Git
    - 建站
    - 教程
---
# 前言
>拥有自己的一个独立博客是多么令人激动呀。

经过了各种关于利用git搭建独立博客的教程，自己慢慢尝试了两天多，终于弄出了一个属于自己的独立博客。虽然网络上已经挺多关于如何利用git建博客的教程，但是我还是想要写一篇教程来整理以下自己关于建立博客的这一过程，也让和我一样想要建立个人博客的人有个参考。

---
**版权声明：欢迎分享，转载请注明此文链接。**
http://zhuowl.github.io/2017/10/21/build-a-blog/



## 目录


1. [关于Github Pages + Jekyll](# github-pages---jektll-is-what)
2. [注册GitHub](# github)
3. [环境安装](# setup)
4. [建立个人的GitHub Pages](# github-pages)




## 关于Github Pages + Jekyll

### 什么是Git & [GitHub](https://github.com/) &[Github Pages](https://pages.github.com/)
Git是一种分布式版本控制系统，由大名鼎鼎的Linux操作系统创建人Linus Torvalds编写，当时的目的是用来管理Linux内核的源码。
[Github](https://github.com/)是全球知名的使用Git系统的一个免费远程仓库（Repository），倡导开源理念，若要将自己的代码仓库私有则需付费。
[Github Pages](https://pages.github.com/)是面向用户、组织和项目开放的公共静态页面搭建托管服 务，站点可以被免费托管在 Github 上，你可以选择使用 Github Pages 默 认提供的域名 github.io 或者自定义域名来发布站点。Github Pages 支持 自动利用 Jekyll 生成站点，也同样支持纯 HTML 文档，将你的 Jekyll 站 点托管在 Github Pages 上是一个不错的选择。

#### 利用Git建立的博客的两种方法
>- 建立一个专门的版本库，来管理自己的博客。
- 在项目中建立一个命名为gh-pages的分支（主要可以用来专门展示该项目）。

  因为我的主要目的是建立一个属于自己的独立博客，在上面写些自己的内容，所以我选择了第一种方法.

### 什么是[Jekyll](http://jekyll.com.cn/)
Jekyll 是一个简单的博客形态的静态站点生产机器。它有一个模版目录，其中包含原始文本格式的文档，通过Markdown（或者 Textile） 以及 Liquid 转化成一个完整的可发布的静态网站，你可以发布在任何你喜爱的服务器上。Jekyll 也可以运行在 GitHub Page 上，也就是说，你可以使用 GitHub 的服务来搭建你的项目页面、博客或者网站，而且是完全免费的。
### Github pages+Jekyll

Github Pages + Jekyll方案的**优点**：
>- Github可以免费托管源文件，其特色的版本化管理，修改博客更加安全和方便。
- Github Pages + Jekyll的结合可以自动编译符合Jekyll规范的网站
- 其支持[markdown](https://sspai.com/post/25137)，可以编写出自己喜欢的并且排版优美的文章。
- 对于计算机的专业的同学来说，拥有属于自己的技术博客也是一个很好的点。

Github Pages + Jekyll方案的**不足**：
>- 需要学一些基础的git命令。
- 由于Jekyll生成的是静态网页，想要加入动态的功能，例如评论功能（下文解决），需要用到第三方的服务。
- 想要完全制作属于自己的博客主题需要懂一些网页制作的知识。

## 注册GitHub
在[Github的官方网址](https://github.com/)注册账户，记住自己的用户名，后面会有用到。
>如果已经有了自己的GitHub账号可以忽略这一步。

刚进去GitHub的官方网址，就会看到如下图的界面。
按顺序填写图中的信息，再点击**Sign up for GitHUb**,会进入下一页面，同时你的邮箱中会收到确认账号的邮件，在邮箱中确认，就会直接进入了你的Git账号页面。
![注册账号01](/img/in-post/post-build-a-blog/git01.png)

## 环境安装
>本文的安装都是在Windows系统下进行。

#### Git相关环境的安装
>如果之前已经安装了Git，可以忽略这一步。

在[Git的官网网址](https://git-scm.com/)点击下载安装包
![下载Git](/img/in-post/post-build-a-blog/git-setup.png)
选择对应的安装版本，因为我的电脑是64位的，所以选择了64位的版本。
![下载Git02](/img/in-post/post-build-a-blog/git-setup02.png)
双击下载得到的Git安装包文件。
Git的安装路径可以换成自己想要的路径，保证自己能够记住这个路径，而且尽量不要有中文（就怕中文万一有什么问题。）
对于Git的安装选项，我都是直接默认就好，有其他需要的可以按着自己的需求来。

也可以参考这篇文章可以参考这篇[ github入门到上传本地项目](http://www.cnblogs.com/specter45/p/github.html)，上面有将Git安装时的每个选项的意义的内容。
![Git安装](/img/in-post/post-build-a-blog/git-setup03.png)
直到最后install,等待一段时间，Git就安装完成了。

#### Git的图形客户端 ——TortoiseGit的安装
>对于Git的使用，我个人觉得先在安装Git安装完成后，体验一番用命令行来控制Git的各种行为后，再来用[TortoiseGit](https://tortoisegit.org/)这种图形客户端来实现Git的功能。这样对于Git的工作流程会有更加清晰的认识，而使用图形客户端能够是我们在使用Git的时候更加方便。

>关于如何使用命令行可以参考刚刚推荐的这篇[ github入门到上传本地项目](http://www.cnblogs.com/specter45/p/github.html)
>里面也有很详细的关于如何使用命令行来实现版本控制。

在[TortoiseGit的官网网址](https://tortoisegit.org/)中下载TortoiseGit。
![下载tortoiseGit](/img/in-post/post-build-a-blog/git-setup05.png)
同样也是进入了下载页面，下载对应版本的TortoiseGit，在这个页面，我们也可以顺便下载下它对应的中文简体的语言包。（当然你觉得自己的英文水平足够好，不需要语言包，也可以不用下载）
![下载tortoiseGit02](/img/in-post/post-build-a-blog/git-setup06.png)
同样的双击下载好的安装包文件，一切按照默认选项。
安装完后双击下载好的语言包，一切按照默认选项，安装完成后，随便选择计算机中的一个文件夹右击出现下图。

是不是很奇怪，我不是已经装好了语言包吗，为什么还是显示为英文。这是因为我们还没有修改语言设置。如图进入**Settings**设置，

![修改语言设置](/img/in-post/post-build-a-blog/git-setup07.png)
如图在**General**中，设置**Language**为**简体中文**，点击选择**应用**，再次右击就会发现语言已经转换成中文了。
![修改](/img/in-post/post-build-a-blog/git-setup08.png)
这时候，选择里面的**Git**，**配置源**可以按照自己的需求选择，**名称**，**Email**和**签名密匙ID**就是我们注册Git的账号名称和邮箱以及密码。
![补上账号信息](/img/in-post/post-build-a-blog/git-setup09.png)




#### Jekyll的本地调试的环境的安装
>为了使在本地也可以看到我们博客的效果。如果没有安装，我们每次修改了一些内容都需要重复的推送到本地master，再上传，再在我们的博客地址上看到最终效果，十分的麻烦。



## 建立个人的GitHub Pages

### 建立博客的版本库
在github的账号页面，选择右上角的左键点击+，弹出子菜单，选择其中的**new repository **(新的版本库)
![注册账号02](/img/in-post/post-build-a-blog/git02.png)
















---

