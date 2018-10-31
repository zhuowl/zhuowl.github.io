---
layout:     post
title:      "Github Pages + Jekyll搭建独立博客教程(二)"
subtitle:   "修改模板+添加评论功能"
author:     "zhuowl"
header-img: "img/bg/bg-cat-08.jpg"
tags:
    - Git
    - 教程
---
# 前言
>在Github Pages + Jekyll搭建独立博客教程(一)中，我们已经配置好了所需要的环境，现在我们可以做真正属于自己的博客了。

---
<p id = "set-up-blog"></p>
**版权声明：欢迎分享，转载请注明此文链接。**

## 目录
1. [新建博客](#set-up-blog)
2. [选择模板](#choose-modle)
3. [修改模板](#change-modle)
4. [jekyll本地浏览](#Jekyll-serve)
5. [附加：添加评论功能](#disqus)
6. [相关链接+相关](#link)

## 新建博客

建立基于Jekyll的个人Github Pages有两条路线
>1. 拥有网页设计的基础，自学Jekyll的教程，设计完全自我基因的网页。
>1. Fork别人的已有的开源博客仓库，只要修改部分内容，就可以实现符合自己的个人博客。（fork:复制当前所在页面的仓库到自己的Github中，相当于给自己的Github开出一条fork的仓库的分支。）
<p id = "choose-modle"></p>
对于网页基础一般的，可以选择第二种方法来。（比较省心省力）
### 选择模板

Jekyll在他们的[wink页面](https://github.com/jekyll/jekyll/wiki/sites)提供了大量优秀的各种风格的博客。
横线标注的是对应博客网站的网址，而圈起**source**则是表示博客模板对应的Github、页面，也就是我们可以fork的页面。

（个人建议是可以选择是有标注中文的，这样我们在修改模板文件的时候，对方可能有中文的注释，修改起来会更加亲切。）
![博客资源](/img/in-post/post-build-a-blog/pages01.png)
>这是我参考的博客模板的[Github页面](https://github.com/Huxpro/huxblog-boilerplate),这个是博客主另外给做的一个稳定版的模板，修改起来比较方便。
<p id = "change-modle"></p>
>**[在这里预览模板 &rarr;](http://huangxuan.me/huxblog-boilerplate/)**

#### 修改模板

下面以我直接修改上面的模板为例，其他的模板修改起来应该也是大同小异的。或者你可以在作者的Readme文件中找到关于需要修改内容。
首先在模板的Github页面，点击fork。
![fork仓库](/img/in-post/post-build-a-blog/pages02.png)
回到自己的Github页面，发现已经多了仓库，名字就是我们之前fork的仓库，点击它。
![fork仓库2](/img/in-post/post-build-a-blog/pages03.png)
这时候，我们要做的第一件事就是修改仓库的名字，点击**Stetting**。
![修改仓库名1](/img/in-post/post-build-a-blog/pages04.png)
将仓库名改成例如： @mojombo 的用户站点仓库 应该被命名为 mojombo.github.io 。点击**Renmae**,仓库名就修改好了。
![修改仓库名2](/img/in-post/post-build-a-blog/pages05.png)
>注意：github.io要保持不变，这是Git官方设定的，不然会引起混乱。

打开仓库文件，那么多文件，我们需要改哪些呢。
主要是修改标注的这四个文件，绿色的标注的表示可以在本地修改比较好，也就是克隆到本地后再修改。红色的表示可以直接在Github上修改，当然也可以克隆到本地再修改。
- _post文件内存储的就是你的博客文章，文章的格式可以是markdown或者
![修改图1](/img/in-post/post-build-a-blog/jekyll01.png)
###### 修改config.yml文件
以修改config.yml文件为例，点击Github上的该文件，进入如图页面，点击**编辑工具**
```js
title: Your Blog				//你的博客网站标题
SEOTitle: 你的博客 | Your Blog 			//SEO Title就是定义了<head><title>标题</title></head>	
header-img: img/home-bg.jpg			//home页的头图，可以不修改文件名，直接在img文件中替换图片即可
email: huxpro@gmail.com				//你注册Git的邮箱
description: ""					//关于你自己的描述
keyword: ""							//可以不填
url: "http://huangxuan.me"          //你博客的地址：一般格式是 http://XXXX.github.io
					//也就是 http://+仓库名。
baseurl: "/你的博客的仓库名" 	//如果你的博客样式没有加载出来，很可能因为这个原因
```



###### 修改内容标注———其他

接下来就是把这个仓库里的内容克隆到本地，也就是自己的电脑上。点击**Clone or download**,点击弹出的剪切板按钮。
 ![本地修改](/img/in-post/post-build-a-blog/pages06.png)
在电脑上新建个文件夹，命名为英文较好（中文易出错，英文后面调试方便），我是直接命名为Blog。选择文件夹右键，选择点击**Git克隆**。
![本地修改2](/img/in-post/post-build-a-blog/pages07.png)
出现下面这样的窗口，直接点击**确定**就好。
**URL**是就是我们刚刚点击剪切板时，自动复制的。
**目录**则是我们克隆下来的仓库所在的位置。
![本地修改3](/img/in-post/post-build-a-blog/pages08.png)
正在克隆的窗口界面,等待一段时间。
![本地修改4](/img/in-post/post-build-a-blog/pages09.png)
克隆成功时，会出现成功的蓝色字样，就表示我们已经克隆成功，本地上已经有该博客的一个仓库。
![本地修改5](/img/in-post/post-build-a-blog/pages10.png)

<p id = "Jekyll-serve"></p>
如果要修改博客内的图标，如果图标命名没有问题(没有问题的意思是：命名和你fork的仓库的主人没有关系)你就可以直接替换img文件夹内对应的图片即可。
对于需要修改命名的图片名，例如avatar-XX.jpg,对于这种格式的命名方式，我们肯定是想要修改成avatar.jpg或者avatar-自己名字的缩写.jpg，就需要注意找到yml文件中对应的位置，将其修改过来。

当然如果你懒得改或者怕出错，你可以选择只在img文件中替换对应对的图片。

#### Jekyll的本地预览
在之前的教程(一)中，我们已经安装了Jekyll的本地调试需要的环境。
现在我们可以通过以下操作实现本地预览博客的效果。
快捷键**Win+R**，输入**cmd**，在终端输入命令
```
$ cd {local repository} // {local repository}替换成你的本地仓库的目录，不用输入{}
$ jekyll serve
$ jekyll serve --watch//和上面的一句是同样的用法，但是这个可以事实更新的。
```
<p id = "disqus"></p>
1.如遇到以下错误，在仓库文件 _config.yml 中加入一句 gems: [jekyll-paginate] 即可。
```js
Deprecation: You appear to have pagination turned on, but you haven't included the `jekyll-paginate` gem. Ensure you have `gems: [jekyll-paginate]` in your configuration file. 
```
如果一切顺利，你会看到**Server address: http://127.0.0.1:4000/**这样的一句话
复制这个地址（注意不要用‘Ctrl+c’来复制，这个程序是ctrl+c是会关闭的），在浏览器中打开，即可预览到博客效果。

#### 草稿
草稿是文件名中没有日期的帖子。他们是你仍然在工作但不想发布的帖子。要启动并运行草稿，请`_drafts`在站点的根目录中创建一个文件夹并创建初稿。

要使用草稿预览您的站点，请运行`jekyll serve`或`jekyll build` 使用`--drafts`开关。将为每个日期分配草稿文件的值修改时间，因此您将看到当前编辑的草稿作为最新帖子。

<p id = "link"></p>
### 附加：添加评论功能
作为一个博客，没有评论功能，就如同缺了血肉的骨架。
可以通过第三方评论系统来添加评论功能。
我用的是国外的[Disqus](https://disqus.com/)，缺点是你需要翻墙，账号不支持微博账号评论。
你也可以用国内的[畅言](http://changyan.kuaizhan.com/)等。
如何加入第三方评论功能，简单来说就是在这些评论系统中注册账号，然后获得一段Javascript代码，将代码粘贴到想要加入评论功能的页面的html文件中。
### 其他+相关链接
- [jekyll的模板链接](https://github.com/jekyll/jekyll/wiki/sites)
- [本博客参考的模板的GitHub页面](https://github.com/Huxpro/huxblog-boilerplate)
- [用自己的域名的替换博客域名](http://playingfingers.com/2016/03/26/build-a-blog/#section-13)

有疑问的欢迎在下方的评论处和我交流：）

---

