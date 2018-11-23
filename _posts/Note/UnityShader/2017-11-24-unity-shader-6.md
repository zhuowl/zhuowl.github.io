---

layout:     post

title:      " 学习笔记：Unity中的基础光照"

subtitle:   "《UnityShader入门精要》第6章"

author:     "zhuowl"

header-img: "img/bg/bg-cat-09.jpg"

tags:

    - 《UnityShader入门精要》
    -  笔记
    -  Shader

---
[toc]
# 1各种射
## 1.1辐射度
![辐射度](/img/in-post/book-note/unity-shader/6/clipboard-1.png)
## 1.2散射
![辐射度](/img/in-post/book-note/unity-shader/6/clipboard-2.png)
散射：
- 散到内部：
   - 折射和透射
- 散到外部：
   - 反射
   
## 1.3反射
**高光（specular）反射**：表示物体表面如何反射光线  
**漫反射（diffuse）**:表示有多少光线会被折射、吸收和散射出物体表面

用`出射度（exitance）`描述出射光线的数量和方向。
辐射度和出射度是满足线性关系的，他们之间的比值 就是材质的漫反射和高光反射属性

--------------------------------------------------------------------------------
# 2着色
**着色（Shading）**:根据 材质属性（如漫反射属性）、光源信息（如光源的方向、辐照
度），按照一定的`公式`去计算沿着某个观察方向的出射度的过程。
公式也就是光照模型（Lighting Modle）

**BRDF（Bidirection Reflectance Distribution Function）**：用来在已经给出了给定入射光线的方向和辐照度后，其可以给出在某个出射方向上的光照能量分布

--------------------------------------------------------------------------------

# 3光照模型
![辐射度](/img/in-post/book-note/unity-shader/6/clipboard-3.png)

光和对象的互相作用称为 `光照模型`（主要有：光照的属性和对象材质的属性）  


**基础光照模型**：**`表面颜色`**=`自发光`+`环境光`+`漫反射`+`高光`  
**标准光照模型**:只关心 `直接光照（direct light）`，也就是那些直接从光源发射出来照射到物体表面后，经过物体表面的一次反射直接进入摄像机的光线。是把进入摄像机的光线分为4部分（每部分使用一种方法计算其贡献度）  

## 3.1自发光
**自发光（emissive）**:用于描述当给定一个方向时，一个表面本身会向该方向发射多少辐射量。  
- （没有使用全局光照（global illumination）技术，只是本身看起来亮，不会影响照亮周围环境）  
-  **`自发光`**=`材质的自发光颜色`  

## 3.2高光反射
**高光反射（specular）**：用于描述当光线从光源照射到模型表面时，该表面会在`完全镜面反射方向`散射多少辐射量  
-  （这里是一种经验模型）  
-  **`反射方向`**=2*（`法线`·`光源方向`）*`法线`-`光源方向`
    
### 3.3.1 Phong模型：
**`高光反射`**=（`光的颜色`·`材质的高光反射系数`）*(max(0,`视角方向`·`反射方向`))的`材质的光泽度的次方`
![辐射度](/img/in-post/book-note/unity-shader/6/clipboard-4.png)

### 3.3.1 Blinn模型：
- **`h`**=(`视角方向`+`光源方向`)/((`视角方向`+`光源方向`)的模长)
- **`高光反射`**=（`光的颜色`·`材质的高光`）*max（0，`法线`·`h`）的材质的光泽度的次方


## 3.4漫反射
 **漫反射（ diffuse）**：用于描述当光线从光源照射到模型表面时，该表面会向每个方向散射多少辐射量  
	  **`漫反射`**=`光的颜色`·`材质的漫反射颜色`*max（0，`法线`·`光源方向`)
## 3.5环境光
- ** 环境光（ambient）**：用于描述其他所有间接光照（在标准光照模型中，通常是一个全局变量）
 	  **`环境光`**=`全局变量`
![辐射度](/img/in-post/book-note/unity-shader/6/clipboard-5.png)

## 3.6 补充
间接光照：光线在个物体的反射，最后进入摄像机。

----
# 4光照

## 4.1 逐顶点光照
**逐顶点光照（per-vertex lighting）**：在顶点着色器中计算光照模型  
**GroundShading（高洛德着色）**：在每个顶点上计算光照，然后在渲染图元内部进行线性插值，最后出现像素颜色（导致图元内部像素颜色总是低于顶点处的最高颜色值，某些情况下会产生明显的棱角现象）

## 4.2 逐像素光照
**逐像素光照（per-pixel lighting）**：在片元着色器中计算光照模型   

**Phong 着色(Phong shading)**:在面片之间对顶点法线进行插值  
- 也被称为Pong插值或法线插值着色技术
- 不同于之前的Pong光照模型 

# 5  Blinn-Phong光照模型的局限性

  1. 很多物理现象用Blinn-Phong模型表现出来，如 `菲涅尔反射（Fresnel reflection）`
  2. **Blinn-Phong模型**是`各项同性（isotropic）`的，也就是当我们固定视角和光源方向旋转这个表面时，反射不会发生任何改变。（但是有些表面是存在 `各向异性（anisotropic）`反射性质的，例如拉丝金属，毛发等）
![辐射度](/img/in-post/book-note/unity-shader/6/clipboard-7.png)  
# 6  Lambert 

## 6.1 Half Lambert(半兰伯特光照模型)
**  Half Lambert(半兰伯特光照模型)**：改善模型的背光区域全黑，失去模型细节表现的问题  
公式：`漫反射颜色`=（`光的颜色`·`材质的颜色`）*（α*(`法线`·`光源方向`)+β）  
- 没有用max来防止法线n和光源方向l的点积为0，α和β的值均为0.5（大多数情况）  
- 可以把n·l的范围从[-1,1]映射到[0,1]  
- 注意：Half Lambert光照模型是没有任何物理依据的，只是一个视觉加强技术 
![辐射度](/img/in-post/book-note/unity-shader/6/clipboard-6.png)

## 6.2 Lambert定律
Lambert定律：在平面某点漫反射的光强(辐射度)与该反射点的法向量n和入射光角度θ的cosθ成正比



--------------------------------------------------------------------------------








