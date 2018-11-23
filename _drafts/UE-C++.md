---

layout:     post

title:      " UE4：Error LNK2019 and LNK2001 无法解析的外部符号 "

subtitle:   ""

author:     "zhuowl"

header-img: "img/bg/bg-cat-02.jpg"

tags:

    - UE4
    - C++

---


在写虚幻的C++时，遇到关于`LNK2019` 和`LNK2001` 的报错，找了蛮久之后发现原来是因为没有在`build.cs`文件中加入对应的模块。

举例几个例子：

1. 在C++中有用到`NavigationPath`的，需要在`build.cs`里加上"NavigationSystem" 模块。

   ```c++
   PublicDependencyModuleNames.AddRange(new string[] { "Core", "CoreUObject", "Engine", "InputCore", "NavigationSystem"});
   ```

2. 用到关于RHI和Shader之类的，需要加上"RHI","RenderCore","ShaderCore"这三个模块。

```C++
PublicDependencyModuleNames.AddRange(new string[] { "Core", "CoreUObject", "Engine", "InputCore", "RHI", "RenderCore", "ShaderCore" });
```







