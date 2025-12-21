---
title: "Bladeworkshop|PS小技巧"
slug: pslog1
date: 2024-08-16T19:23:14+10:00
lastmod:
description: 柔光、做旧、描线、抠透明物体
tag: [Design]
categories: [同人工坊]
toc: true
image: "/images/default2.jpg"
---

# <font color=#417D7A>Bladeworkshop|PS小技巧</font>
给自己记录点PS技巧，毕竟不用就会忘，每次都是重新学习。

> warning  
> 要点：转换为智能对象&图层蒙版

## <font color=#417D7A>柔光</font><br>
- <font color=#2F86A6>Ctrl+J</font> 将底图复制一层，为<font color=#29ADB2>图层1</font>；  
- <font color=#2F86A6>选择-色彩范围</font>选取背景高光部分，Ctrl+J复制为新图层，为<font color=#29ADB2>背景高光</font>，新建图层蒙版稍微调整下；  
- 将<font color=#29ADB2>背景高光</font>转换为智能对象后，应用<font color=#2F86A6>高斯模糊</font>，数值可以大点，调整图层模式与透明度/填充。视情况复制该图层为<font color=#29ADB2>背景高光2</font>再次调整；也可以添点其他模糊，比如<font color=#2F86A6>模糊画廊-场景模糊or光圈模糊</font>，看心情。  
- 将<font color=#29ADB2>图层1</font>转换为智能对象，应用<font color=#2F86A6>高斯模糊</font>，数值较小，将该照片的整体清晰度稍稍调低；  
- 可选项：继续对<font color=#29ADB2>图层1</font>执行<font color=#2F86A6>蒙尘与划痕</font>，然后<font color=#2F86A6>添加杂色</font>，再次降低清晰度。
- 适当<font color=#2F86A6>新建调整图层（饱和度、色阶等）</font>，利用<font color=#2F86A6>创建剪贴蒙版</font>对每一图层进行调整。
### <font color=#417D7A>做旧</font><br>

在上述柔光基础上：
- <font color=#2F86A6>新建色相/饱和度调整图层</font>，降低饱和度；
- <font color=#2F86A6>新建照片滤镜or色相/饱和度or可选颜色</font>，将颜色调黄一点；
- 找个免费课上用纹理素材，拖进去，命名为<font color=#29ADB2>纹理</font>，转换为智能对象，新建色阶调整图层，适当调整数值。  

以下分别为最终效果图、原图、过程图*3：

{{< imgloop "https://raw.githubusercontent.com/Bladeisme/blog-img/master/final.jpg,https://raw.githubusercontent.com/Bladeisme/blog-img/master/first.jpg,https://raw.githubusercontent.com/Bladeisme/blog-img/master/step1.png,https://raw.githubusercontent.com/Bladeisme/blog-img/master/step2.png,https://raw.githubusercontent.com/Bladeisme/blog-img/master/step3.png," >}}  

## <font color=#417D7A>描线？</font><br>
有段时间挺喜欢用的，但步骤非常随机。

- <font color=#2F86A6>Ctrl+J</font> 将底图复制一层，为<font color=#29ADB2>图层1</font>（此处改名为滤镜库了）；  
- 对<font color=#29ADB2>图层1</font>执行转换为智能对象（操作时又忘了），<font color=#2F86A6>ctru+u</font>，饱和度拉到最左，调整为黑白，执行<font color=#2F86A6>滤镜库</font>常用的是：<font color=#2F86A6>图章、影印、撕边</font>。各种都可以试一下；  
- 对该图层执行<font color=#2F86A6>滤镜库-艺术效果-干笔画or调色刀or绘画涂抹</font>，同样步骤非常随机，目的是简化图；  
- 对该图层执行<font color=#2F86A6>滤镜库-海报边缘</font>
（彩色图情况下比较好用，黑白则约等于没用）；  
- 调整图层模式，利用<font color=#2F86A6>渐变映射or可选颜色</font>
等调色。

总而言之滤镜库是个好东西，非常喜欢。还喜欢用它来加噪点，即<font color=#2F86A6>照片颗粒</font>。

以下分别为原图、黑白图层、调色后的最终效果图：

{{< imgloop "https://raw.githubusercontent.com/Bladeisme/blog-img/master/nattu-adnan-Ai2TRdvI6gM-unsplash.jpg,https://raw.githubusercontent.com/Bladeisme/blog-img/master/blackandwhite.png,https://raw.githubusercontent.com/Bladeisme/blog-img/master/step.png" >}}  

## <font color=#417D7A>抠透明物体：冰块/钻石等</font><br>

白色背景情况下：

- <font color=#2F86A6>Ctrl+J</font> 将底图复制一层，为<font color=#29ADB2>图层1</font>；  
- <font color=#2F86A6>Ctrl+A</font>全选，<font color=#2F86A6>Ctrl+C复制</font>，添加蒙版</font>，<font color=#2F86A6>Alt+点击蒙版</font>进入蒙版（全白的），<font color=#2F86A6>Ctrl+V复制</font>
- <font color=#2F86A6>Ctrl+I</font> 反向（蒙版主体为黑色，冰块为浅色）；假设本身底图为黑色则不需要执行该步骤；
- - 蒙版：蒙版里只有黑白两色，<font color=#29ADB2>白色为显示（选中），黑色不显示（不选中）</font>；  
- <font color=#2F86A6>Ctrl+点击蒙版</font>，选中白色部分；
- <font color=#2F86A6>Ctrl+C复制</font>；
- <font color=#2F86A6>新建图层</font>，<font color=#2F86A6>Ctrl+V粘贴</font>，对选区填充白色。

