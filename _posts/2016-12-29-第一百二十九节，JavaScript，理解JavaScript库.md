---
layout: post
title: " 第一百二十九节，JavaScript，理解JavaScript库 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**JavaScript，理解JavaScript库**



**学习要点：**

**1.项目介绍**

**2.理解JavaScript库**

**3.创建基础库**



**从本章，我们来用之前的基础知识来写一个项目，用以巩固之前所学。那么，每个项目为了提高开发效率，我们需要创建一个库来存放大量的重复调用的代码。而在这里，我们需要理解一些知识。**



**一．** **项目介绍**

**在现在流行的网站中，大量使用前端的Web应用，估计就是博客系统了。博客系统目前主要分为两种，一种是博客，一种是微博(一句话博客)。**

**不管在博客和微博，都采用的大量的JavaScript特效，有图片广告、下拉菜单、表单验证、弹窗、轮播器等等一系列。那么我们就创建一个项目，把上面各种应用较多的效果编写出来。**



**二．理解JavaScript** **库**

**什么是JavaScript库？说白了，就是把各种常用的代码片段，组织起来放在一个js文件里，组成一个包，这个包就是JavaScript库。现如今有太多优秀的开源JavaScript库，比如：jQuery、Prototype、Dojo、Extjs等等。这些JavaScript库已经把最常用的代码进行了有效的封装，以方便我们开发，从而提高效率。**

**当然，这里我们就不去探讨这些开源JavaScript库，那样就太容易了一点。我们这里需要探讨的是自己创建一个JavaScript库，虽然自己创建的可能没有那些开源JavaScript库功能强大，但在提升自己JavaScript开发能力，有很大帮助。**



**三．** **创建基础库**

**我们可以创建一个库，这是一个基础库，名字就叫做base.js。我们准备在里面编写最常用的代码，然后不断的扩展封装。**

**在最常用的代码中，最最常用的，也许就是获取节点方法。这里我们可以编写如下代码：**

**封装库代码：**

[code]

     /**
     *feng_zhuang_ku_1.0版本，js封装库，2016/12/29日：林贵秀
     **/
    
    /**
     *定义封装库对象
     **/
    var feng_zhuang_ku = {
        /**------------------------------------------------获取元素标签开始--------------------------------------------**/
        /**
         * huo_qu_id()方法,通过id获取元素标签，参数是id值，返回元素对象
         **/
        huo_qu_id: function (id) {
            return document.getElementById(id);
        },
        /**
         * huo_qu_name_zhi()方法，通过元素name值获取指定元素，参数是元素name值，返回元素相同name值对象集合，一般获取表单
         **/
        huo_qu_name_zhi: function (name) {
            return document.getElementsByName(name);
        },
        /**
         * huo_qu_name()方法，通过标签名称获取相同标签名的元素，参数是标签名称，返回对象集合
         **/
        huo_qu_name: function (tag) {
            return document.getElementsByTagName(tag);
        }
        /**------------------------------------------------获取元素标签结束--------------------------------------------**/
    };
[/code]

**前台调用代码**

[code]

     //前台调用代码
    window.onload = function (){
        alert(feng_zhuang_ku.huo_qu_id('li').innerHTML);
        alert(feng_zhuang_ku.huo_qu_name_zhi('j')[0].innerHTML);
        alert(feng_zhuang_ku.huo_qu_name('div')[2].innerHTML);
    };
[/code]

**PS：本项目为了更好的兼容性，我们采用UTF-8，在Notepad++上设置默认为UTF-8即可。此项目不是为了做一个博客或者微博，而是将里面的各种效果拿出来模仿编写。**

