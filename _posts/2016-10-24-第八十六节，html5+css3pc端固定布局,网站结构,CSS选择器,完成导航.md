---
layout: post
title: " 第八十六节，html5+css3pc端固定布局,网站结构,CSS选择器,完成导航 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**html5+css3pc端固定布局,网站结构,CSS选择器,完成导航**



**页面采用1280的最低宽度设计，去掉滚动条为1263像素。**

**项目是PC端的固定布局，会采用像素(px)单位。**



****网站结构 ** **语义********

**在没有任何思路的情况下，可以参考大量同类型的网站，了解一下大致结构。我们将要做的网站是一个旅行社的企业网站。经过大量参考，首页上，我们选择了最基本的四个模块。**

**四个基本模块：nav 导航、header头部、section首页主体、footer尾部**

[code]

     <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>瓢城旅行社</title>
    </head>
    <body>
    
    <!--导航-->
    <nav></nav>
    
    <!--头部-->
    <header></header>
    
    <!--主体-->
    <section></section>
    
    <!--尾部-->
    <footer></footer>
    
    </body>
    </html>
[/code]



****CSS选择器****

**我们这个旅行社的网站属于中小型网站，通用样式采用元素定义型；顶层的布局元素可以使用id定义型；其他标签一律class定义型。**  
  

****完成导航****

****![](https://images2015.cnblogs.com/blog/955761/201610/955761-20161025093055906-1043503038.png)****



**HTML代码**

[code]

     <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>瓢城旅行社</title>
        <link rel="stylesheet" href="css/index.css">
    </head>
    <body>
    <!--导航-->
    <nav class="dao-hang">
        <div class="dao-hang2">
            <h1 class="log">瓢城旅行社</h1>
            <ul>
                <li class="dao-hang-lie-biao"><a href="index.html">首页</a></li>
                <li class="dao-hang-lie-biao"><a href="#">旅游资讯</a></li>
                <li class="dao-hang-lie-biao"><a href="#">机票订购</a></li>
                <li class="dao-hang-lie-biao"><a href="#">风景欣赏</a></li>
                <li class="dao-hang-lie-biao"><a href="#">公司简介</a></li>
            </ul>
        </div>
    </nav>
    
    <!--头部-->
    <header>header</header>
    
    <!--主体-->
    <section>section</section>
    
    <!--尾部-->
    <footer>footer</footer>
    
    </body>
    </html>
[/code]

**css代码**

[code]

     @charset "utf-8";
    /*通用样式*/
    *{
        margin: 0;
        padding: 0;
    }
    ul{
        list-style-type: none;
    }
    a{
        text-decoration: none;
    }
    /*通用样式结束*/
    
    /*导航区域*/
    .dao-hang{
        width: 100%;
        height: 70px;
        background-color: #333;
        color: azure;
    }
    .dao-hang .dao-hang2{
        width: 1263px;
        height: 70px;
        margin: 0 auto;
    }
    .dao-hang .dao-hang2 .log{
        width: 240px;
        height: 70px;
        float: left;
        background-image: url("../img/logo.png");
        text-indent:-9999px;
    }
    .dao-hang .dao-hang2 ul{
        float: right;
    }
    .dao-hang .dao-hang2 .dao-hang-lie-biao{
        width: 120px;
        height: 70px;
        float: left;
        text-align: center;
        line-height: 70px;
    }
    .dao-hang .dao-hang2 .dao-hang-lie-biao a{
        display: block;
        width: 120px;
        height: 70px;
        color: azure;
    }
    .dao-hang .dao-hang2 .dao-hang-lie-biao a:hover{
        background-color: #ff4d51;
    }
    /*导航区域结束*/
[/code]



**总结**

**1.以前我们布局都是用div，html5更着重语义，用语义标签替换以前的div,我们采用的语义标签，nav
导航、header头部、section首页主体、footer尾部**

**2.如果是页面大部分标签都要用到的css样式，可以写在开头通用样式如：**

[code]

     /*通用样式*/
    *{
        margin: 0;
        padding: 0;
    }
    ul{
        list-style-type: none;
    }
    a{
        text-decoration: none;
    }
    /*通用样式结束*/
[/code]

去除所有元素的内外边距，去除所ul的小圆点，去除所有a标签的下划线



**
3.备注：LOGO采用的是h1标签，一般为了让搜索引擎更好的抓取关键字，我们建议一个页面只有一个h1，而且是最重要的关键词放在里面。在首页上，最重要的关键词就是旅行社的名称。当然，如果在其他页面，比如新闻网站的单个新闻，最重要的应该是新闻标题，网站的名称就其次了。
**

