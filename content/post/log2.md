---
title: "Hugo|博客装修日记"
date: 2024-03-07T20:57:13+11:00
lastmod: 2024-04-08T21:58:18+11:00
draft: false
description: 
tags: [hugo]
categories: [hugo]
toc: true
hidden: 
Summary: "解决不了问题就解决提出问题的东西"
image: "/images/default.jpg"
---

# <font color=#417D7A>修改，从入门到重新投胎</font>

## <font color=#417D7A>RSS订阅</font>
略一研究，不是很想使用，想必也没人会订阅，而且我写了会发长毛象！博客自带该功能，我直接取消了。检查之后发现about页面里还有，打开<code>about.xml</code>删除相关语法。  
不过之前在其他人的博客看到了订阅功能并且能够一月一发送邮件，觉得还蛮好玩的，暂时订阅了观察一阵子！

## <font color=#417D7A>给评论区增加表情包</font>
看安装方式添加emoji的方法也不同，我的之前所述css等都写在`comment.html`里，直接修改config无效我也不知道为什么，可能因为没添加相关语法吧。这次我也直接在`comment.html`里修改了。  
在`serverURL`这一行之后、`]`之前添加  
```
emoji: [
    'url',
    ]
```
即可，朋友分享了blob和小豆泥表情包，所以我的是：
```
emoji: [
    'https://cdn.jsdelivr.net/gh/norevi/blob-emoji-for-waline@2.0/blobs-png',
    'https://cdn.jsdelivr.net/gh/Saidosi/azuki-emoji-for-waline@1.0/azukisan',
    'https://cdn.jsdelivr.net/gh/norevi/blob-emoji-for-waline@2.0/blobs-gif',
     ],
```
## <font color=#417D7A>修改评论区样式-darkmode</font>
看不懂！失败！放弃！

## <font color=#417D7A>blockquote重叠</font>
之前为了让代码块显色修改了blockquote，可能改错了但确实显背景色了！接着我发现了一个问题：引用块比较近的地方重叠了。排查之后删除了style.css里blockquote这段里的`height = 2px`，恢复正常。  
这个代码块我感觉是我设置错误，如果有人知道怎么让代码块显示背景色请告诉我。我在highlight pre等加上了background-color之后是代码单行有背景色，我想要引用模块整个显示背景色。总之暂时这么整了。  

# <font color=#417D7A>3.14-更换主题至NewBee</font>
解决不了问题就解决提出问题的东西！之前的mini主题很简洁我蛮喜欢但鉴于我完全不懂写码，很多地方都解决不了，所以精挑细选寻觅到了一个新主题[NewBee](https://github.com/xioyito/NewBee),这次我学聪明了，先看主题更新时间，最近一次是2024年，想必作者还在维护，看到伊说有问题可以去issue提，又发现伊三周前还回答了别人的问题，感觉作者目前为止都有在关注该主题。而且本主题功能也多，各方面我都比较喜欢，于是堂堂更换！  
~~因为不知道怎么更换总之下载下来修改config没成功于是我直接备份内容删博重来了~~  

## <font color=#417D7A>更换waline评论系统</font>
搞不定，直接问了作者，请见[本issue](https://github.com/xioyito/NewBee/issues/30)。其余步骤同上一篇文章。

## <font color=#417D7A>启用H5</font>
主题自带该渲染功能，但没启用。修改config文件下最底部的
```
    # enable the following code if there are html statements in your md file
    # 如果md文件中有html语句，请启用以下代码

    [markup.goldmark]
        [markup.goldmark.renderer]
            unsafe = true
```
删掉代码部分的`#`即可，加上#后会变成注释。

## <font color=#417D7A>添加轮播图</font>
部分参考[《Hugo | 在文章中插入轮播图片》](https://mantyke.icu/posts/2021/cf2cf0fb/)，在`shortcodes`文件夹下新建`imgloop.html`文件，
```
{{ if .Site.Params.enableimgloop }}
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/Swiper/3.4.2/css/swiper.min.css">
    <!-- Swiper -->
    <style>
        .swiper-slide img {
            width: 100%; /* 图片宽度自适应容器 */
            height: auto; /* 图片高度自适应宽度 */
            margin: 0; /* 可选：去除图片的默认 margin */
        }
    </style>
    <div class="swiper-container">
        <div class="swiper-wrapper">
            {{$itItems := split (.Get 0) ","}}
            {{range $itItems }}
            <div class="swiper-slide">
                <img src="{{.}}" alt="">
            </div>
            {{end}}
        </div>
        <!-- Add Pagination -->
        <div class="swiper-pagination"></div>
    </div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/Swiper/3.4.2/js/swiper.min.js"></script>
     <!-- Initialize Swiper -->
     <script>
        var swiper = new Swiper('.swiper-container', {
            pagination: '.swiper-pagination',
            paginationClickable: true,
            //自动调节高度
            autoHeight: true,
            //键盘左右方向键控制
            keyboardControl : true,
            //鼠标滑轮控制
            mousewheelControl : true,
            //自动切换
            //autoplay : 5000,
            //懒加载
            lazyLoading : true,
            lazyLoadingInPrevNext : true,
            //无限循环
            loop : true,
        });
    </script>
{{ end }}
```

修改css，在`/public/css/shortcodes.css`最末尾添加：
```
/* 轮播图 */

/* 在此处添加到你的CSS样式表中 */

.swiper-container {
    max-width: 500px; /* 让容器宽度自适应 */
    height: auto; /* 设置轮播容器的最大高度 */
    margin: 2em auto; /* 可选：调整轮播容器的上下边距 */
    overflow: hidden; /* 可选：隐藏超出容器的部分 */
}

.swiper-slide img {
    width: 500px; /* 图片宽度自适应容器 */ /* 图片固定500px宽度 */
    height: auto; /* 图片高度自适应宽度 */
    margin: 0; /* 可选：去除图片的默认 margin */
}
```

## <font color=#417D7A>修改页尾网站信息·新</font>
这个主题已启用卜算子进行流量统计（这玩意儿开着就是让我知道没人看……），anyway鉴于它写在footer的copyright下了，这会儿不好直接false整个copyright，因为试了一下发现会把流量统计也关闭。尝试之前修改法发现没成功，新抄一段，代码来自[《增加博客运行时间和阅读统计》](https://www.10101.io/2018/09/16/Blog_2)
在`© {{ .Site.Params.footer.from }}-{{ now.Format "2006" }} <a href="{{ .Site.Author.link }}">{{ .Site.Author.name }}</a>`之后增加`星球已自转 <SPAN id=span_dt_dt></SPAN>`,然后在这个div下增加
```
<SCRIPT language=javascript>
function show_date_time(){
window.setTimeout("show_date_time()", 1000);
 BirthDay=new Date("04/08/2022");//日期自己修改
today=new Date();
timeold=(today.getTime()-BirthDay.getTime());
sectimeold=timeold/1000
secondsold=Math.floor(sectimeold);
msPerDay=24*60*60*1000
e_daysold=timeold/msPerDay
daysold=Math.floor(e_daysold);
span_dt_dt.innerHTML=""+daysold+"天";
}
show_date_time();
</SCRIPT>
```

**文章总篇数修改方式不变~**

## <font color=#417D7A>隐藏文章</font>
之前为了测试把两年前的读书观影记录摆上来了，越看越觉得傻*，决定隐藏文章。方法：在文章抬头部分加入`hidden: true`即可

## <font color=#417D7A>折叠</font>
在shortcodes新建`detail.html`，写入：
```
<details>
  <summary>{{ (.Get 0) | markdownify }}</summary>
  {{ .Inner | markdownify }}
</details>
```
短代码是：

> {< detail "这里是折叠提示词" >}  
需要隐藏的内容  
{< /detail >}   
/* 需要多打一对花括号 */
</code></pre>

效果：  

{{< detail "这里是折叠提示词" >}}
需要隐藏的内容
{{< /detail >}}

<br>

# <font color=#417D7A>04.08更新：求助作者堂堂成功！</font>

## <font color=#417D7A>新增相册页面</font>

这里我遇到的问题是，新增页面后tag+图片和最顶部的导航栏重叠，F12检查半天都不成功，想办法找到了作者，给作者发了邮件，今日伊回复邮件，解决办法是：  
> 将style.css中.hero的margin-top: 60px移除, 然后给body{}添加padding-top: 60px;

依样修改后堂堂成功！
新增方式这里不说了，请见[《小白hugo博客装修笔记（1）》-添加相册功能](https://www.blain.top/p/renovation/#%E6%B7%BB%E5%8A%A0%E7%9B%B8%E5%86%8C%E5%8A%9F%E8%83%BD)

## <font color=#417D7A>新增Artitalk说说页面</font>

同上也没有成功，和上面一个问题一起给作者发邮件了，作者新写了一篇文章，[《创建新的页面》](https://xioyito.top/posts/%E5%88%9B%E5%BB%BA%E6%96%B0%E7%9A%84%E9%A1%B5%E9%9D%A2/)