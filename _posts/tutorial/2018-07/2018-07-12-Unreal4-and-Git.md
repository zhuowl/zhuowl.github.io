---
layout:     post
title:      "用Git版本管理Unreal4工程"
subtitle:   "Git， Unreal4"
author:     "zhuowl"
header-img: "img/bg/bg-cat-08.jpg"
tags:
    - Unreal4
    - Git
    - 教程
---
# 前言
之前就有一直在用Git来管理自己的工程，后来也想用来管理自己Unreal4的工程，结果发现自己直接在文件夹中用Git来上传到服务器上一直会失败……查了资料发现，是因为部分文件太大。去Unreal4的官方文档查了发现官方可以自带用Git进行版本管理的内容，但是由于本人记忆力太查了（每次弄完之后，时间一久就会忘记），所以想着自己整理一遍，可以不用每次忘记了都去看文档。

---
**版权声明：欢迎分享，转载请注明此文链接。**

## 目录
1. [Git相关软件安装](#Git-setup)
2. [工程本地版本控制](#in-pc)
3. [推送到版本管理服务器上](#submit)
4. [异地版本管理](#in-other-pc)
5. [总结](#all)

## Git相关软件安装

软件安装：安装好Git 和TortoiseGit

> 关于这两个软件如何安装，我之前也写过一点教程，[Git和TortoiseGit的安装教程](https://zhuowl.github.io/2017/10/24/build-a-blog-1/)在这可以参考一下
> （p(#￣▽￣#)o）

<p id = "Git-setup"></p>


确认自己已经安装好Git，知道Git的安装目录在哪里，然后知道其中的`git.exe`的位置
我的通常都是D:\Program Files\Git\bin\git.exe（仅作参考）

## 工程本地版本控制
<p id = "in-pc"></p>
![打开本地的版本控制](/img/in-post/tourial/post-Unreal-Git/01.png)
选择版本控制为'Git'，输入之前找的Git的路径，再接受设置(Accept Settings)。过一会出现相关信息，选择用Git初始化工程(Initialize peoject with Git)。右下角会出来表示正在把文件加入到版本管理中，等一会。
![选择版本控制为'Git'](/img/in-post/tourial/post-Unreal-Git/02.png)

![工程本地版本控制03](/img/in-post/tourial/post-Unreal-Git/03.png)
![工程本地版本控制03](/img/in-post/tourial/post-Unreal-Git/04.png)
再次点击Accept Settings就可以了。

![工程本地版本控制03](/img/in-post/tourial/post-Unreal-Git/05.png)

这是时候我们就发现版本管理的图标变成绿色了（这时候我们只是在本地建立了自己的版本库，我们还需要在把版本库传到服务器上）。![工程本地版本控制03](/img/in-post/tourial/post-Unreal-Git/06.png)

我们打开工程文件夹，发现里面多了一个gitignore文本文档(这是因为工程里有些文件是不需要上传的，而通常这些文件的大小也超出了上传的大小限制，所以在之前的操作中，引擎会自己生成忽略文件，你也可以自己手动建gitignore文件)。

![工程本地版本控制03](/img/in-post/tourial/post-Unreal-Git/07.png)

我把忽略文件的内容粘贴在下面：
（Binaries
DerivedDataCache
Intermediate
Saved
.vscode
.vs
*.VC.db
*.opensdf
*.opendb
*.sdf
*.sln
*.suo
*.xcodeproj
*.xcworkspace）

![工程本地版本控制03](/img/in-post/tourial/post-Unreal-Git/08.png)

## 推送到版本管理服务器上
<p id = "submit"></p>
接下来就是把工程推到版本管理的服务器上，我常用的有BitBucket和GitHub,在上面你需要自己建立一个respository, 我建议最好repository的名字和工程名字一样，不一样可能会出问题（我没试过不名字不一样的）

差点忘记一个点：`在推送的时候需要把工程关掉！！`

选择工程文件夹，右键（按照如下图选择），TortoiseGit是使用Git的好帮手：),最后选择推送。

![工程本地版本控制03](/img/in-post/tourial/post-Unreal-Git/09.png)

在“其他URL框”中粘贴上repository的中对应的粘贴版的中的内容。 

![工程本地版本控制03](/img/in-post/tourial/post-Unreal-Git/10.png)

### 更新工程时
每次在工程里修改文件或者新增加文件时，文件上会出现如下图标（在推送前需要提交（submit）到本地的版本库，否则修改的内容是不会被传到服务器上的版本库里）
![工程本地版本控制03](/img/in-post/tourial/post-Unreal-Git/11.png)
接着会需要描述一下要提交的内容，然后选择OK即可。然后新增文件上的图标则会消失。
![工程本地版本控制03](/img/in-post/tourial/post-Unreal-Git/12.png)
后面的操作与之前相同，关闭工程，然后再工程文件位置用小乌龟推送到服务器上的repository里。在服务器中的仓库里就可以看到你刚更新的内容。

## 异地版本管理
<p id = "in-other-pc"></p>
电脑上没有工程时选择克隆：在服务器上复制URL地址，然后在文件夹中选择Git克隆，粘贴对应的URL地址。克隆完成后，打开工程。将工程的sourceControl打开选择为Git，粘贴git.exe的安装路径，然后确认（这些步骤都和前面类似）。

电脑上已经有工程，需要从服务器上更新的，就选择拉取。
接下来提交和推送都是同理。
## 总结
<p id = "all"></p>
总之用Git来控制Unreal的工程的原理实际上和其他的没有什么大区别，在使用过程中，就是分清本地版本库和服务器上的版本库，然后在这两者之间注意提交、推送等内容的本质含义。

有疑问的欢迎在下方的评论处和我交流：）

---

