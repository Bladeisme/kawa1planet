---
title: "捣鼓|如何解包renpy游戏"
description: 
slug: unrenpy
tag: [随机电波,捣鼓]
categories: [随机电波]
date: 2026-05-05T22:52:53+08:00
image: "/images/default.jpg"
math: 
license: 
hidden: false
comments: true
draft: false
---

# <font color=#417D7A>Records| 如何解包renpy游戏</font>

工作需要，学习一下如何解包renpy引擎制作的游戏，这个引擎做AVG比较多，解包出来适合扒剧本。  
倒是不难，分为1.配置环境，2.下载需要的软件，3.解包，这三个步骤。  

## 1.配置环境
需要python 3，这一步解包的软件里有写可以用pip安装，没太懂是不是一定需要。  
python下的官网最新版，安装完后cmd用`python --version`查询版本；pip好像同时下载下来了，用`pip --version`检查版本。  
后续发现我是直接从github下载的似乎不需要pip，不过没关系，能跑起来就行。  

## 2.下载软件
需要的比较多了，工作电脑上没有安装VSCode，所以先下载了VSCode。  
其他需要的：rpaExtract（用于解包游戏的rpa文件），unrpyc（用于解包rpaExtract解包出来的rpyc文件）。  
rpaExtract：https://iwanplays.itch.io/rpaex  
unrpyc：https://github.com/CensoredUsername/unrpyc  

## 3.解包
### 3.1 查找解包文件
下载完后，可以新建一个文件夹，将rpaExtract（粉色的exe）与需要解包的游戏文件放到一起。  
查找游戏文件：  
找到游戏本地文件，文件夹下有game文件夹的话一般就放在这里。寻找file size很大的后缀为rpa的文件，一般就是这个。  
### 3.2 rpa→rpyc
将该rpa文件复制到rpaExtract所在文件夹，然后**将其拖到rpaExtreact图标上**，rpaExtract会自动解压。  
我一开始是打开了rpaExtract，写命令让它解压，但一开始运行就闪退，后来发现只要直接拖拽就好了啊！还一直看不懂它写的You have to drag-and-drop one or more .rpa file(s) on the file for it to work是什么意思，原来真是字面意思……  
rpaExtract解包完的文件会自动出现在根目录。我解包完后出现了chapter、character等文件夹，可以根据自己所需查找不同文件夹并再次解压。  
### 3.3 unrpyc
在unrpyc文件根目录右键cmd，输入`py -3 unrpyc.py "需要解包的rpyc文件地址" "解包后文件存放地址"`  
注：1.输入`py -3 unrpyc.py`后可以直接将文件拖入cmd窗口，会自动生成需要解包文件的地址；第二个地址可以不输入，不输入则解包后文件会出现在原rpyc文件所在位置。
unren给的readme里的用法是：`python unrpyc.py file1.rpyc file2.rpyc`或者`python unrpyc.py folder/xxxx`，但我使用了这串代码没有反应，所以还是用了`py -3 unrpyc.py`  

如图：  
![](https://raw.githubusercontent.com/Bladeisme/blog-img/master/AgAABmvVub0_xHTRr8VJ5ZgkGCBmPQ0l.png)

解包出来的文件为rpy格式，用VSCode直接打开就可以阅读啦！

::: tip 引用标题
unrpyc指令在其他文件根目录下打开cmd时无法运行，只能在unrpyc文件根目录下运行，个人情况是这样。
:::