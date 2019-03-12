
---
layout: post
title: " 第八十四节，css布局小技巧及font-awesome图标使用 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---


**css布局小技巧** **及font-awesome图标使用**

**图片鼠标放上去遮罩效果，显示文字**

**![](https://images2015.cnblogs.com/blog/955761/201610/955761-20161022184124513-1869862025.png)**

**当鼠标放上去时**

**![](https://images2015.cnblogs.com/blog/955761/201610/955761-20161022184232295-1233371015.png)**

[code]

     /*最外层div*/
    .a{
        width: 384px;
        height: 240px;
        background-color: #ff4e37;
        position: relative;
    }
    /*插入图片的div*/
    .b{
        width: 384px;
        height: 240px;
        background-color: #ff4e37;
        overflow: hidden;
    }
    /*遮罩层div*/
    .c{
        width: 384px;
        height: 240px;
        background-color: #010008;
        opacity: 0;
        overflow: hidden;
        position: absolute;
        left: 0px;
        top: 0px;
        right: 0px;
        bottom: 0px;
    }
    /*鼠标放上去效果*/
    div .c:hover{
        background-color: #010008;
        opacity: 0.5;
        color: #FFFFFF;
        font-size: 40px;
        font-weight: bold;
        text-align: center;
        line-height: 240px;
    }
    
    
    <div class="a">
        <div class="b">
            <img src="53d.jpg">
        </div>
        <div class="c">
            <samp>美女图片</samp>
        </div>
    </div>
[/code]



**css绘制尖角效果**

**在网页中，有很多地方会用到尖角，尖角可以是图片的，也可以用css来绘制**

**用一个div来绘制尖角**

[code]

    .a {
        /*设置边框*/
        border-top: 30px solid red;
        border-right: 30px solid black;
        border-bottom: 30px solid green;
        border-left: 30px solid blue;
        /*将区块转换成内联块*/
        display: inline-block;
    }
    
    <div class="a"></div>
[/code]

**效果：![](https://images2015.cnblogs.com/blog/955761/201610/955761-20161022193512685-1281803225.png)
**颜色可以根据自己的需要调整****



****将其他不需要的3个尖角颜色改成透明的，一个尖角就形成了****

[code]

    .a {
        /*设置边框*/
        border-top: 30px solid transparent;
        border-right: 30px solid transparent;
        border-bottom: 30px solid transparent;
        border-left: 30px solid blue;
        /*将区块转换成内联块*/
        display: inline-block;
    }
    
    <div class="a"></div>
[/code]

**效果：**![](https://images2015.cnblogs.com/blog/955761/201610/955761-20161022194214279-1776158352.png)



**另一种效果**

[code]

    .a {
        /*设置边框*/
        border-top: 30px solid transparent;
        border-right: 30px solid transparent;
        border-bottom: 0px solid transparent;
        border-left: 30px solid blue;
        /*将区块转换成内联块*/
        display: inline-block;
    }
    
    <div class="a"></div>
[/code]

**
效果：![](https://images2015.cnblogs.com/blog/955761/201610/955761-20161022194659670-1190027589.png)**





**还可以结合伪类选择器:hover来设置鼠标动作尖角**

[code]

    .af {
        width: 100px;
        height: 50px;
        background-color: #ff563a;
    }
    .a{
        /*设置边框*/
        border-top: 10px solid green;
        border-right: 10px solid transparent;
        border-bottom: 10px solid transparent;
        border-left: 10px solid transparent;
        /*将区块转换成内联块*/
        display: inline-block;
        margin-top: 20px;
        margin-left: 10px;
    }
    .a:hover{
        /*设置边框*/
        border-top: 10px solid transparent;
        border-right: 10px solid transparent;
        border-bottom: 10px solid green;
        border-left: 10px solid transparent;
        /*将区块转换成内联块*/
        display: inline-block;
        margin-top: 10px;
        margin-left: 10px;
    }
    
    <div class="af">
        <div class="a"></div>
    </div>
[/code]

**效果：
**![](https://images2015.cnblogs.com/blog/955761/201610/955761-20161022202633138-193854041.png)
**![](https://images2015.cnblogs.com/blog/955761/201610/955761-20161022202646045-367888000.png)鼠标没放上去时尖角向下，鼠标放上去尖角向上******





**font-awesome图标使用**

****font-awesome图标是一个css的插件包，是一个以字体文件方式集成的图标，首先要下载插件包****

****中文网站<http://fontawesome.dashgame.com/>****

****英文网站<http://fontawesome.io/icons/>****

****下载好后解压，会得到如下文件****

****![](https://images2015.cnblogs.com/blog/955761/201610/955761-20161023075445982-1411257269.png)****



**将font-awesome-4.6.3  文件夹放入html工程目录里**

**然后在html页面引入 **font-awesome-4.6.3  文件夹里的css样式****

[code]

    <link rel="stylesheet" type="text/css" href="font-awesome-4.6.3/css/font-awesome.css"/>
[/code]

**在要使用的元素标签class="fa fa-图标名称"，如：class="fa fa-envelope-o"**

[code]

     <div>
        <p><span class="fa fa-envelope-o"></span>邮件</p>
    </div>
[/code]

**这样图标就展现出来了，如果想改变颜色，可以自定义一个css文件来改变**

[code]

     p .fa-envelope-o{
        color: #ff1029;
    }
[/code]

**效果：![](https://images2015.cnblogs.com/blog/955761/201610/955761-20161023092839795-949697657.png)**



**更多说明查看官方文档，一下是官方说明截图**

**![](https://images2015.cnblogs.com/blog/955761/201610/955761-20161023093624967-814633104.png)**

