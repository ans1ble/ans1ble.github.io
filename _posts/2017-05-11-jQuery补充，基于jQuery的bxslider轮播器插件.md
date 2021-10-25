---
layout: post
title: " jQuery补充，基于jQuery的bxslider轮播器插件 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**基于jQuery的bxslider轮播器插件**

**![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170511230834457-2052548331.png)**

**html**

[code]

     <!DOCTYPE html>
    <html lang="zh-cn">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1,maximum-scale=1, user-scalable=no">
        <title>bxslider介绍</title>
        <!--引入bxslider样式文件-->
        <link rel="stylesheet" href="bxslider/jquery.bxslider.min.css">
    </head>
    <body>
    <!--普通轮播图-->
    <ul class="bxslider">
        <li><img src="http://placehold.it/350x150&text=FooBar1"/></li>
        <li><img src="http://placehold.it/350x150&text=FooBar2"/></li>
        <li><img src="http://placehold.it/350x150&text=FooBar3"/></li>
    </ul>
    <!--横向旋转木马轮播-->
    <div class="slider1">
        <div class="slide"><img src="http://placehold.it/350x150&text=FooBar1"></div>
        <div class="slide"><img src="http://placehold.it/350x150&text=FooBar2"></div>
        <div class="slide"><img src="http://placehold.it/350x150&text=FooBar3"></div>
        <div class="slide"><img src="http://placehold.it/350x150&text=FooBar4"></div>
        <div class="slide"><img src="http://placehold.it/350x150&text=FooBar5"></div>
        <div class="slide"><img src="http://placehold.it/350x150&text=FooBar6"></div>
        <div class="slide"><img src="http://placehold.it/350x150&text=FooBar7"></div>
        <div class="slide"><img src="http://placehold.it/350x150&text=FooBar8"></div>
        <div class="slide"><img src="http://placehold.it/350x150&text=FooBar9"></div>
    </div>
    <!--纵向旋转木马轮播-->
    <div class="slider8">
      <div class="slide"><img src="http://placehold.it/300x100&text=FooBar1"></div>
      <div class="slide"><img src="http://placehold.it/300x100&text=FooBar2"></div>
      <div class="slide"><img src="http://placehold.it/300x100&text=FooBar3"></div>
      <div class="slide"><img src="http://placehold.it/300x100&text=FooBar4"></div>
      <div class="slide"><img src="http://placehold.it/300x100&text=FooBar5"></div>
      <div class="slide"><img src="http://placehold.it/300x100&text=FooBar6"></div>
      <div class="slide"><img src="http://placehold.it/300x100&text=FooBar7"></div>
      <div class="slide"><img src="http://placehold.it/300x100&text=FooBar8"></div>
      <div class="slide"><img src="http://placehold.it/300x100&text=FooBar9"></div>
      <div class="slide"><img src="http://placehold.it/300x100&text=FooBar10"></div>
    </div>
    <!--引入jquery文件-->
    <script src="jquery/jquery.min.js"></script>
    <!--引入bxslider里的js-->
    <script src="bxslider/jquery.bxslider.min.js"></script>
    <script src="ceshi.js"></script>
    </body>
    </html>
[/code]

**js**



[code]

    /**
     * Created by admin on 2017/5/2.
     */
    $(function () {
        //<!--普通轮播图-->
        $('.bxslider').bxSlider({auto: true, autoControls: true});
    
        //<!--横向旋转木马轮播-->
        $('.slider1').bxSlider({auto: true, slideWidth: 200, minSlides: 2, maxSlides: 3, slideMargin: 10});
    
        //<!--纵向旋转木马轮播-->
        $('.slider8').bxSlider({
            mode: 'vertical',
            slideWidth: 300,
            minSlides: 2,
            slideMargin: 10
        });
    });
[/code]





**官方网站：http://bxslider.com/**



