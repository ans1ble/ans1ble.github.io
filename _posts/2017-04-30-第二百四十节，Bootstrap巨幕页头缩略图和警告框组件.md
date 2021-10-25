---
layout: post
title: " 第二百四十节，Bootstrap巨幕页头缩略图和警告框组件 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**Bootstrap巨幕页头缩略图和警告框组件**



**学习要点：**

**1.巨幕组件**

**2.页头组件**

**3.缩略图组件**

**4.警告框组件**



**本节课我们主要学习一下 Bootstrap 的四个组件功能：巨幕组件、页头组件、缩略图组 件和警告框组件。**



**一．巨幕组件**

**巨幕组件主要是展示网站的关键性区域。**

**在固定的范围内，有圆角， **整个 **巨幕以 **最大宽度为1140px显示********



**container样式class类，写在 <div>里，设置固定布局div最大宽度为1140px(Bootstrap)**  
 **jumbotron样式class类，写在 <div>里，设置巨幕组件div样式,展示网站的关键性区域(Bootstrap)**

[code]

    <div class="container">
        <div class="jumbotron">
            <h2>网站标题</h2>
            <p>这是一个学习性的网站！</p>
            <p><a href="#" class="btn btn-default">更多内容</a></p>
        </div>
    </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170430184203428-424195751.png)





**100%全屏，没有圆角， 巨幕最外层以100%宽度显示，巨幕内区域以 ** ** ** **最大宽度为1140px显示【最流行做法】**********

[code]

     <div class="jumbotron">
        <div class="container">
            <h2>网站标题</h2>
            <p>这是一个学习性的网站！</p>
            <p><a href="#" class="btn btn-default">更多内容</a></p>
        </div>
    </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170430184955381-788661373.png)





**二．页头组件**

**增加一些空间**

**page-header样式class类，写在页头区域元素里，设置页头区域样式(Bootstrap)**

[code]

     <div class="page-header">
        <h1>大标题
            <small>小标题</small>
        </h1>
    </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170430185614069-626287550.png)





**三．缩略图组件**

**缩略图配合响应式**

**thumbnail样式class类，写在 <img>外层<div>元素里，设置响应式图片区域(Bootstrap)**

[code]

    <div class="container">                                 <!--布局固定宽度样式，最大宽度1140-->
        <div class="row">                                   <!--设置一行响应式删格行，为12列删格-->
            <div class="col-xs-6 col-md-3 col-sm-4">        <!--col-xs-6(手机)表示屏幕小于768所占6列删格，也就是一行的一半，就会显示两列图片-->
                <div class=" **thumbnail** ">
                    <img src="img/pic.png" alt="">
                </div>
            </div>
            <div class="col-xs-6 col-md-3 col-sm-4">        <!--col-md-3(中等屏幕)表示屏幕大于或等于992所占3列删格，也就是显示4列图片-->
                <div class=" **thumbnail** ">
                    <img src="img/pic.png" alt="">
                </div>
            </div>
            <div class="col-xs-6 col-md-3 col-sm-4">        <!--col-sm-4(平板)表示屏幕大于或等于768所占4列删格，也就是显示3列图片-->
                <div class=" **thumbnail** ">
                    <img src="img/pic.png" alt="">
                </div>
            </div>
            <div class="col-xs-6 col-md-3 col-sm-4">
                <div class=" **thumbnail** ">
                    <img src="img/pic.png" alt="">
                </div>
            </div>
        </div>
    </div>
[/code]

**屏幕大于或等于992**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170430201409350-1876157831.png)**  
**屏幕大于或等于768**

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170430201451350-575281721.png)  
**屏幕小于768**

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170430201522475-1264561665.png)





**响应式微缩图，图文并茂自定义内容**

**caption样式class类，写在响应式图片区域
<div>里面与img同级的<div>元素里，设置响应式图片区域里的图文内容样式(Bootstrap)**

[code]

    <div class="container">
        <div class="row">
            <div class="col-xs-6 col-md-3 col-sm-4">
                <div class="thumbnail">
                    <img src="img/pic.png" alt="">
                    <div class="caption">
                        <h3>图文并茂</h3>
                        <p>这是一个图片结合文字的缩略图</p>
                        <p><a href="#" class="btn btn-default">进入</a></p>
                    </div>
                </div>
            </div>
            <div class="col-xs-6 col-md-3 col-sm-4">
                <div class="thumbnail">
                    <img src="img/pic.png" alt="">
                    <div class="caption">
                        <h3>图文并茂</h3>
                        <p>这是一个图片结合文字的缩略图</p>
                        <p><a href="#" class="btn btn-default">进入</a></p>
                    </div>
                </div>
            </div>
            <div class="col-xs-6 col-md-3 col-sm-4">
                <div class="thumbnail">
                    <img src="img/pic.png" alt="">
                    <div class="caption">
                        <h3>图文并茂</h3>
                        <p>这是一个图片结合文字的缩略图</p>
                        <p><a href="#" class="btn btn-default">进入</a></p>
                    </div>
                </div>
            </div>
            <div class="col-xs-6 col-md-3 col-sm-4">
                <div class="thumbnail">
                    <img src="img/pic.png" alt="">
                    <div class="caption">
                        <h3>图文并茂</h3>
                        <p>这是一个图片结合文字的缩略图</p>
                        <p><a href="#" class="btn btn-default">进入</a></p>
                    </div>
                </div>
            </div>
        </div>
    </div>
[/code]

**屏幕大于或等于992**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170430204137006-168491865.png)**  
**屏幕大于或等于768**

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170430204233756-1697667874.png)  
**屏幕小于768**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170430204307397-1475582339.png)**







**四．警告框组件**

**警告框组件是一组预定义消息。**

**alert样式class类，写在 <div>元素里，声明一个警告信息框(Bootstrap)**  
 **alert-success样式class类，写在 <div>元素里，设置警告信息框绿色(Bootstrap)**  
 **alert-info样式class类，写在 <div>元素里，设置警告信息框蓝色(Bootstrap)**  
 **alert-warning样式class类，写在 <div>元素里，设置警告信息框橙色(Bootstrap)**  
 **alert-danger样式class类，写在 <div>元素里，设置警告信息框红色(Bootstrap)**

[code]

    <div class="alert alert-success">Bootstrap</div>
    <div class="alert alert-info">Bootstrap</div>
    <div class="alert alert-warning">Bootstrap</div>
    <div class="alert alert-danger">Bootstrap</div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170430205319100-2136715226.png)





**带关闭的警告框**

**close样式class类，写在警告信息框里的 <button>元素里，给警告信息框设置一个按钮关闭样式(Bootstrap)**  
 **data-dismiss="alert"事件，写在警告信息框里的 <button>元素里，点击按钮关闭警告信息框(Bootstrap)**

[code]

    <div class="alert alert-success">
        Bootstrap
        <button type="button" class="close" data-dismiss="alert">
            <span>&times;</span>
        </button>
    </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170430210106022-709339183.png)





**警告框自动适配的超链接**

**alert-link样式class类，写在警告信息框里的 <a>元素里，设置警告框里的超链接样式，自动适配警告框(Bootstrap)**

[code]

    <div class="alert alert-success">
        Bootstrap，请到官网 <a href="#" class="alert-link">下载</a>
        <button type="button" class="close" data-dismiss="alert">
            <span>&times;</span>
        </button>
    </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170430210618819-1077007183.png)



