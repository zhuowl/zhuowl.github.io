---

layout:     post

title:      " 渲染流水线——学习笔记"

subtitle:   "《UnityShader入门精要》第2章"

author:     "zhuowl"

header-img: "img/bg/bg-cat-09.jpg"

tags:

    - 《UnityShader入门精要》
    -  笔记
    -  Shader

---

# 1 三个阶段
- 应用阶段（Application Stage）
- 几何阶段（Geometry Stage）
- 光栅化阶段（Rasterizer Stage）

![渲染流水线](/img/in-post/book-note/unity-shader/2/clipboard-1.png)
## 1.1 应用阶段：
  1. 准备好场景数据
  2. Culling剔除不可见部分
  3. 设置模型的渲染状态
## 1.2 几何阶段：
把顶点坐标变换到屏幕空间中
## 1.3 光栅化阶段：
产生屏幕上的像素


--------------------------------------------------------------------------------
# 2 渲染数据的流程
## 2.1 渲染流程
![渲染数据的流程](/img/in-post/book-note/unity-shader/2/clipboard-2.png)
渲染数据从
HDD（硬盘，Hard Disk Drive）中  
加载到==>  
RAM(系统内存，Random Access Memory)  
网格 纹理等数据  
加载到==>  
VRAM（显存，Video Random Access Memory）  
>显卡对显存访问快，大部分显卡不支持直接访问内存
![渲染数据的流程](/img/in-post/book-note/unity-shader/2/clipboard-3.png)

## 2.2渲染状态
**渲染状态**定义场景中的网格用的是 什么纹理 是否开启混合  
用的顶点着色器（Vertex Shader） 
片元着色器（Fragment）
光源属性 材质
![渲染管线](/img/in-post/book-note/unity-shader/2/clipboard-4.png)



--------------------------------------------------------------------------------
# 3 GPU流水线
![Gpu流水线](/img/in-post/book-note/unity-shader/2/clipboard-5.png)
- **顶点着色器（Vertex Shader）**：顶点的空间变换，顶点着色
- **曲面细分着色器（Tessellation Shader）**：细分图元
- **几何着色器（Geometry）**：逐图元的着色操作/产生更多的图元
- **裁剪（Clipping）**:将不再摄像机视野的顶点裁剪掉（可自定义裁剪平面才配置裁剪区域）/指令控制裁剪三角图元的正面或者背面  
- **片元着色器(Fragment Shader)**:用于射线逐片元（per-Fragment）的着色操作

![坐标变换](/img/in-post/book-note/unity-shader/2/clipboard-6.png)

```cpp
o.pos=UnityObjectToClipPos(v.vertx);
```
这句话的功能就是 把顶点坐标转换到齐次裁剪坐标系下,再由硬件做透视除法，得到归一化的设备坐标
![设备坐标](/img/in-post/book-note/unity-shader/2/clipboard-7.png)
设备坐标（NDC，Normalized Device Coordinate）

## 3.1 裁剪
![裁剪过程](/img/in-post/book-note/unity-shader/2/clipboard-8.png)


![图像坐标](/img/in-post/book-note/unity-shader/2/clipboard-9.png)
>图像有时是倒转的，可能是这两个之间的坐标差异造成的，要小心

## 3.2 三角形遍历
**三角形遍历（Triangle Traversal）：**找到那些像素被三角网格覆盖（被覆盖的像素-> 片元Fragment），也被称为 扫描变换（Scan Conversion）  
![三角形遍历](/img/in-post/book-note/unity-shader/2/clipboard-10.png)

## 3.3 片元着色器
![片元着色器](/img/in-post/book-note/unity-shader/2/clipboard-11.png)
一个片元不是真正意义上的像素 而是包含了很多的状态的集合
这些状态用于计算每个像素的最终颜色
(状态有：屏幕坐标、深度信息，法线，纹理坐标等)

 **片元着色器（Fragment Shader）**，在DirectX中被称为 像素着色器（Pixel Shader）  
局限：只可以影响单个片元

**逐片元操作**（Per-Fragment Operation）是OpenGL
也可以被称为 输出合并阶段（Output-Merger）在DirectX中
![片元着色器](/img/in-post/book-note/unity-shader/2/clipboard-12.png)
# 4一些名词及相关过程
- Early-Z技术;把深度测试提前
- 双重缓存(Double Buffering):为了避免看到正在进行光栅化的图元。
- 后置缓存（Back Buffer）；对场景的渲染是在幕后发生
- 缓存（Front Buffer）：显示在屏幕上的图像
![片元着色器](/img/in-post/book-note/unity-shader/2/clipboard-14.png)
![片元着色器](/img/in-post/book-note/unity-shader/2/clipboard-14.png)
![片元着色器](/img/in-post/book-note/unity-shader/2/clipboard-16.png)










-
