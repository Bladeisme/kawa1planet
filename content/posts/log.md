---
title: Hugo|从Hexo迁移到Hugo
date: 2024-03-07T00:03:24+11:00
draft: false
description: 
tags: [hugo]
categories: [hugo]
toc: true
hidden: 
Summary: "建站日记"
image: "/images/default.jpg"
---

<font color=#417D7A>搬家！</font>

# <font color=#417D7A>建博</font>

之前首页蛮多朋友开始自建博客，看了之后觉得蛮有趣的于是我也跟风捣鼓了一个，用的hexo，网上教程很多而且非常详细。当时想应该不会玩很久吧，没想到也两年了。2022年4月8日本博勉强开始运转，内容还不算很多，但hexo的更新列表越来越长、长到我每次更新都觉得是在报错了。于是今年决定也用hugo啦。  
建站参考的塔塔的[《一起动手搭建个人博客吧》](https://mantyke.icu/posts/2021/hugo-build-blog/)一文。中间因为各种原因炸了8次吧，最后换用本主题勉力动起来了，当时心情：你就在此地不要走动，我去睡个觉。  

选用的是[mini主题](https://github.com/nodejh/hugo-theme-mini)，看它比较旧，上一次更新是好多年前，有点担心，果不其然出了问题，tag页和category页虽然显示正常，但无法点击跳转文章，并且实际上hugo server之后localhost:1313也无法显示。目前为止这个问题还没解决，查看主题issue也发现其他人遇到了一样的情况并且很不幸，也没有人回答有效的解决方式。这点加入list。 

# <font color=#417D7A>装修</font>

此时此刻又发现了惊天大问题，我的博客根目录下没有`asset`文件夹也没有`static`和`layouts`，只有public。我从`themes/mini`里复制了一个layouts文件夹到根目录下进行修改。  

## <font color=#417D7A>修改整体配色</font>

改CSS比较简单，但因为我根目录下无`style.css`，我是直接在`themes/mini/static/css`里改的，理论上似乎不能动主题文件夹但……  
背景改成灰色，整体色改为绿色。  
这有一个简便的修改方式：打开博客网页，按F12，可以查看每一部分的css，它会具体到`style.css`的某一行，还可以直接在上面修改、调整、预览  
![photo](https://raw.githubusercontent.com/Bladeisme/blog-img/master/QQ截图20240307154459.png '_no')

## <font color=#417D7A>改头像与网站ico</font>

这一步也比较简单，直接替换images文件夹下的图即可。可以搜一个将文件转换成ico格式的在线转换网站，很方便。  

## <font color=#417D7A>增加about页</font>

其实本主题导航栏里就有「关于」，但点进去404，谷歌一番后发现大家给的添加about页的教程都一样，就是直接在根目录的content文件夹里新建一个`about.md`，打开这个文件，在抬头部分写上：`menu: "main"`  
config.toml里写入：

```[menu]
 [[menu.main]]
    name = "About"
    pageRef = "/about"
    weight = 10
```

我依样画葫芦建立该文件并写好后发现，它竟然出现在了list页，并且被计入文章总数了！翻了一遍目录，想到about页应该和categories&tags是一样的格式，遂把`about.md`移到了/about文件夹下，再更新，完成！

## <font color=#417D7A>增加站点运行时间与全站总字数&总篇数</font>

运行时间代码参考知乎这篇[《Hugo博客如何添加网站运行时间？》](https://www.zhihu.com/question/614820608)。  
踩的坑：  
因为本主题自带copyright，我在config将copyright改成了「卡哇1星球自转中」，因此修改后无反应。于是在config中将copyright设置为false。server后发现自定义的copyright是没有了，变成了默认模式！打开footer尝试研究代码，只看懂了if/else，我灵机一动，这不就是「如果A则，否则B」的意思吗，于是将这一整块代码全部删除，把上文里的代码放到`<footer></footer>`之间。  
之后还想添加站点总字数和总篇数，~~抄太多了想不起来抄自哪里了（抱歉！）~~。  
我使用的代码：

```
  {{$scratch := newScratch}}
  {{ range (where .Site.Pages "Kind" "page" )}}
      {{$scratch.Add "total" .WordCount}}
  {{ end }}
  ```
  看不懂放在哪里，遂放在`<footer id="footer">`下一行。
  接下来是：
  ```
  {{ $articleCount := len .Site.RegularPages }}
  {{ $totalWordCount := 0 }}
  {{ range .Site.Pages }}
  {{ $totalWordCount = add $totalWordCount .WordCount }}
  {{ end }}
  ```
  在`< div>卡哇1星球自转 < span id="days">0< /span>< /div>`这一行后加入
```
< div>已生产 {{ $articleCount }} 篇文章，共 {{ $totalWordCount }} 字< /div>
  /* 去掉空格 */
```

## <font color=#417D7A>增加评论区并修改</font> 


mini主题自带评论功能，但是用的是disqus，我想用waline，于是先按[waline的文档](https://waline.js.org/guide/get-started/#leancloud-%E8%AE%BE%E7%BD%AE-%E6%95%B0%E6%8D%AE%E5%BA%93)注册并部署。这里有几个坑：  
1. 使用国际版LeanCloud，我在hexo时便已注册过国际版，这步这次略过。但是好像使用国内版本会出问题，具体我也不清楚，总之建议用国际版。  
2. `serverURL`是vercel部署的waline地址。
3. 作为管理员注册waline时填的地址也是上面这个，不是自己博客的地址。不过写错了也没关系可以修改。  

~~虽然waline给了手把手教程但还是每一步都会踩雷我们纯小白是这样的~~  
修改waline头像参考[本篇](https://innerso.prvcy.page/posts/configure-waline/),在vercel的环境变量中添加：`key=GRAVATAR_STR`，`value=https://cravatar.cn/avatar/{{mail|md5}}?d=monsterid`
邮箱接收评论提醒：没成功，sign。  
评论区CSS样式：  
我因为没有asset等文件，直接写在`comment.html`文件里了。  

```waline
close
  .waline-container {
      background-color: transparent;
      border-radius: var(--card-border-radius);
      box-shadow: var(--shadow-l1);
      padding: 2%; /*缩小边距*/

  }
  .waline-container .vcount {
      color: var(--card-text-color-main);
  }

  :root{
    /* 主题色 */
    --waline-font-size: 1rem ;
    --waline-theme-color: #154c47; /* 主题色，按钮颜色 */
    --waline-active-color: #f04853c4;
    --waline-color: #154c47;
    --waline-bg-color: transparent; /* 设置背景透明，官网CSS文件里无这一条我自己添加的 */
    --waline-bgcolor-light: #c8c8c8;
    --waline-border-color: #154c47; /* 边框线颜色 */
    --waline-disable-bgcolor: #FAF9F7;
    --waline-avatar-size:5rem !important;
    --waline-m-avatar-size:calc(var(--waline-avatar-size)*9/13) !important; 
    --waline-badge-color:rgba(5, 150, 148, 0.425) ;
    --waline-badge-font-size: 0.45em ;
    --waline-info-bgcolor: #f8f8f8 ;
    --waline-info-color:#999 ;
    --waline-info-font-size: 0.625rem ;
    --waline-border: 1px solid var(--waline-border-color);
    --waline-avatar-radius: 50%; /* 0就是正方形，可以自由设置头像圆角 */
  }
  .comment-waline{
    /*
    margin-top: 10px;
    position:relative;
    float: none;
    display: inline;
    padding: 10px;
    */
    background-color: transparent;
    margin-top: 18px;
    padding-top: 25px;
    padding-bottom: 40px;
    padding-left: 40px;
    padding-right: 40px;
    font-weight: 300;
    line-height: 1.8;

    /*
    border-left: 1px solid rgba(0,0,0,0.1);
    border-right: 1px solid rgba(0,0,0,0.1);
    */
  }
  .comment-underline {
    display: inline-block;
    margin-top: 10px;
    margin-bottom: 0px;
    width: 50px;
    border-bottom: 3px solid #f0485388;
  ```


## <font color=#417D7A>修改目录样式</font> 

mini自带的目录显示在文章上方，而且比较丑。找了很多教程修改都不成功，最后绝望想起以前hexo用的主题也有目录，想研究下hexo那个主题怎么写的，没想到该主题竟然被搬到hugo来了！于是立刻复制粘贴了对方的`toc.html`。  
[maupassant-hugo](https://github.com/flysnow-org/maupassant-hugo),这个主题也挺不错的，功能齐全。  
替换掉我的toc.html文件后开始修改样式，发现css样式写在toc.html里了，于是直接在上面修改：  
- 修改`background-color`删除背景；`
- `margin-left</code>修改左右位置；`
- `< div class="post-toc" style="position: fixed; top: 100px;">`，top是指到浏览器上方的距离。  
- 最后发现目录位置是固定的，这样一来文章下拉后就看不到目录了，感觉失去意义，于是把`position`改成了`fixed`。  

<font color=#417D7A>3.14更新：研究发现除了fixed之外还有relative，感觉应该是相对的意思，但修改后不久就换了主题，所以还没有测试过效果。</font>



暂时先修改到这里。