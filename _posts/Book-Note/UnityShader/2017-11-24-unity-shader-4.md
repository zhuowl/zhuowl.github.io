---

layout:     post

title:      " 学习笔记：学习Shader所需的数学基础"

subtitle:   "《UnityShader入门精要》第4章"

author:     "zhuowl"

header-img: "img/bg/bg-cat-09.jpg"

tags:

    - 《UnityShader入门精要》
    -  笔记
    -  Shader

---


# 各种空间

- **模型空间（Object Space）**:也叫  Modle Space ,局部空间（local space）
	- 模型空间的原点和坐标轴通常是由美术人员在建模软件中确立好的

- **世界空间（World space）**：是一个特殊的坐标系，建立了我们最关心的最大的空间  
  	- 可以被用于描述 绝对位置（在世界坐标系中的位置）

- **观察空间（view Space）**：也叫作 摄像机空间（Camera Space）
	- 和屏幕空间不同 观察空间是三维的 而屏幕空间是二维的
    - 观察变换 （View transform）：把顶点坐标从世界坐标变换 变换到观察空间中 

- **裁剪空间（Clip space）**也被称为 齐次裁剪空间
	- 用于变换的矩阵被称为 “裁剪矩阵”（clip matrix）,也被称为 投影矩阵（projection matrix）
	- 目标：能够方便地对渲染图元进行裁剪	(由视椎体决定)
	- 视锥体由6个视锥平面组成，分为2种：正交投影，透视投影
	![裁剪空间](/img/in-post/book-note/unity-shader/4/clipboard-2.png)
    ![裁剪空间](/img/in-post/book-note/unity-shader/4/clipboard-3.png)
    ![裁剪空间](/img/in-post/book-note/unity-shader/4/clipboard-4.png)
   
   下图是渲染流水线中顶点的空间变换
  ![裁剪空间](/img/in-post/book-note/unity-shader/4/clipboard-5.png)
## 零散的一些内容
![点积](/img/in-post/book-note/unity-shader/4/clipboard-1.png)
  
**齐次坐标**：把原来的三维矢量转换成四维矢量  
约定的缩放顺序：是先缩放，再旋转，最后平移  

对于线性变换（缩放 和 旋转），只需要3X3就可以  
存在平移变换，就用4X4的矩阵  
Cg中用行优先的方法  


