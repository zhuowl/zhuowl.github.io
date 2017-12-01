---



layout:     post



title:      "学习笔记+教程：DirectX3D9.0游戏编程环境配置"



subtitle:   "DirectX3D9.0游戏编程基础的相关环境安装"



author:     "zhuowl"



header-img: "img/bg/bg-cat-01.jpg"



tags:



    - 《DirectX3D9.0游戏编程基础》

    -  笔记

    - Shader



---
[toc]
# 1软件安装



## 1.1 安装DirectX9.0  

[DirectX9.0下载网址](https://www.microsoft.com/en-us/download/details.aspx?id=8109)下载DirectX9.0    

得到名为`directx_Jun2010_redist.exe`文件，双击该文件。
![安装DX9](/img/in-post/book-note/DirectX-9.0-Base/environment-set-up/clipboard-2.png)
点击yes。
![安装DX9](/img/in-post/book-note/DirectX-9.0-Base/environment-set-up/clipboard-3.png)
点击Browse选择解压的路径（最好新建一个文件夹，例命名为DX9，因为解压出来的内容较多,需要在一个文件夹内）  

在解压出来的文件中找到`DXSETUP.exe`文件，双击该文件。出现安装界面，按流程安装即可。
![安装DX9](/img/in-post/book-note/DirectX-9.0-Base/environment-set-up/clipboard-4.png)


## 1.2 安装DirectX9.0  SDK

SDK（Software Development Kit，软件开发工具包）		
[官方下载地址](https://www.microsoft.com/en-us/download/details.aspx?id=6812)			

我的安装目录如下（要记住该路径，后面配置环境时需要）：	
![安装DX9](/img/in-post/book-note/DirectX-9.0-Base/environment-set-up/clipboard-5.png)

## 1.2.1解决问题Error Code: S1023
下载安装时如果出现如下问题：

>Setup failed. Errors were encountered during installation of redistributable packages. 
>Please close all open programs and try running setup again. If problems persist, contact DirectX >Developer Support.
>Error Code: S1023

**解决办法**为：   
- 在路径为（`C:\Users\\AppData\Local\Temp`）中找到一个名为Microsoft Visual C++ 2010 x64 Redistributable Setup_20110608_xxx.html ##的文件。

- 双击该文件，如果能找到下面这一段话：
>Installation Blockers:     
>A newer version of Microsoft Visual C++ 2010 Redistributable has been detected on the machine.      Final Result: Installation failed with error code: (0x000013EC), "A StopBlock was hit or a System      Requirement was not met." (Elapsed time: 0 00:00:00).

那就需要在你的控制面板中删除下面这个文件   
`Microsoft Visual C++ 2010 x86/x64 redistributable - 10.0.(number over 30319)`
>(删除x84或者x64,我的电脑是64位的，我删除x86后才可以成功安装)		

- 删除上面的文件后，再次安装SDK文件就可以成功安装了。  
参考[解决问题的的网址](https://stackoverflow.com/questions/4102259/directx-sdk-june-2010-installation-problems-error-code-s1023)

# 2 配置环境
按照书中所说，打开VS，选择`工具`->`选项`
![安装DX9](/img/in-post/book-note/DirectX-9.0-Base/environment-set-up/clipboard-6.png)
![安装DX9](/img/in-post/book-note/DirectX-9.0-Base/environment-set-up/clipboard-7.png)
发现在vs2015的版本中，按照上述的方法找到的VC++目录已经被弃用了，根据提示，在->`项目`->`属性`中找到了VC++目录。
所以需要先新建一个项目：  
注意是win32的项目，项目名字自定义（如下标记步骤）  
![安装DX9](/img/in-post/book-note/DirectX-9.0-Base/environment-set-up/clipboard-8.png)
![安装DX9](/img/in-post/book-note/DirectX-9.0-Base/environment-set-up/clipboard-10.png)

像之前所说，在->`项目`->`属性`中找到了VC++目录  
![找vc++目录](/img/in-post/book-note/DirectX-9.0-Base/environment-set-up/clipboard-11.png)
![安装DX9](/img/in-post/book-note/DirectX-9.0-Base/environment-set-up/clipboard-12.png)
## 2.1 修改包含目录
选择`包含目录`，在其下标中，选择`编辑`（如图的步骤）
![安装DX9](/img/in-post/book-note/DirectX-9.0-Base/environment-set-up/clipboard-13.png)
找到SDK的安装路径，选择`include`文件夹，点击确定。
![安装DX9](/img/in-post/book-note/DirectX-9.0-Base/environment-set-up/clipboard-14.png)

## 2.2 修改库目录
同样是，选择`库目录`,在其下标中，选择编辑。		
还是之前的SDK的安装路径，选择->Lib-文件夹下的`x86`文件，点击确定。	

## 2.3 链接库文件

将库文件  
d3d9.lib  
d3dx9.lib  
dxguid.lib  
winmm.lib  
comctl32.lib  
链接到自己的工程中。
>（winmm.lib并不是DirectX库文件，是Windows多媒体库文件，主要用到其中的定时功能）

在项目->属性->链接器中，
![安装DX9](/img/in-post/book-note/DirectX-9.0-Base/environment-set-up/clipboard-15.png)

输入库文件  
d3d9.lib  
d3dx9.lib  
dxguid.lib  
winmm.lib  
comctl32.lib 。不要忘记点击`确定`

>仍有个问题：我的 d3dx9.lib一直找不到(但是目前好像发现没有什么问题)  

# 3 测试项目

在SDK的安装路径中`D:\Program Files (x86)\Microsoft DirectX SDK (June2010)\Samples\C++\Direct3D\Tutorials\Tut01_CreateDevice`文件内的cpp复制到工程文件内的源文件内。

按`f5`运行出现如下的窗口，则表示环境配置OK。
![安装DX9](/img/in-post/book-note/DirectX-9.0-Base/environment-set-up/clipboard-16.png)